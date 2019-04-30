---
layout: post
title: 'Prism: View Model Locator => Custom Convention'
description: How to implement a custom ViewModelLocator Convention to load view models from other separated assemblies without having the same namespace
comments: true
categories: [Development, Tutorials]
tags: [C#, PRISM]
fullview: true
--- 

<img src="https://avatars3.githubusercontent.com/u/10503161?v=3" style="width:80px; float: left; margin: 15px;" /> I was working on a modular/composite application using [Prism][1] and [MEF][2]. 
One of the most issues i encountered, was using the Prism ViewModelLocator to bind the view context to the right view model instance. 
After googling, I had to write my own convention basing on Prism default convention. the new custom convention allows me to bind view models not necessary having the same namespace as the view namespace. also makes it possible to bind these view models event if are in another separated assembly. 

{% highlight xml %}
	mvvm:ViewModelLocator.AutoWireViewModel="True"
{% endhighlight %}


I started by creating an interface named *IMvvmTypeLocator* : 

{% highlight csharp %}
public interface IMvvmTypeLocator
{
	/// <summary>
	/// Gets the type of the view model from view type.
	/// </summary>
	/// <param name="viewType">Type of the view.</param>
	/// <returns>The view model type if located; otherwise null</returns>
	Type GetViewModelTypeFromViewType(Type viewType);
}
{% endhighlight %}

The interface above has initially 3 methods, i will focus-on and share only the first one (**GetViewModelTypeFromViewType(Type viewType)**) to acheive my goal. <del>the 2 other methods are helpful for me to do the same but to locate the view type from a gived view model type or a given view name.</del>

### Implement the interface : 

I created a class to implement the interface IMvvmTypeLocator, this class has the **AggregateCatalog** as constructor argument. 
> Note that we are going to create a custom convention to locate the target view models in all registered assembly catalogs 

#### What the method GetViewModelTypeFromViewType does ? 
This method starts by applying the default PRISM convention (**GetDefaultViewModelTypeFromViewType** method) to locate the target view model, if no view model located, then apply the custom one.

##### 1st step: 
+ Get the loaded assemblies from the aggregate catalog: 
    + All the assemblies added to the aggregate catalog in the BootStrapper. 

##### 2nd step: 
+ Locate all non-abstracte classes inheriting from BindableBase class of PRISM (supposed to be a view models).

##### 3rd step: 
+ The type name ends with the extension 'ViewModel' 
+ If the view type name ends with the extesnion 'View':
    + Locate the type name without the extension 'ViewModel' equals to the view type name without the extension 'View'.
+ If the view type name doesn't end with the extension 'View':
    + Locate the type name without the extension 'ViewModel' equals the view type name. 

#### Example: 
If you added the assembly MyAssembly1.dll (contains the view models inside whatever their namespaces) to the assembly catalog. This custom convention will search inside this assembly for the target view model. 
If your view named **Main**View or **Main**:
The convention will look for all the non-abstract classes ineheriting from BindableBase class, and named **Main**ViewModel. 

## Source: 

{% highlight csharp %}
public class MvvmTypeLocator: IMvvmTypeLocator
{
	/// <summary>
	/// The aggregate catalog
	/// </summary>
	private AggregateCatalog AggregateCatalog { get; set; }

	public MvvmTypeLocator(AggregateCatalog aggregateCatalog)
	{
		this.AggregateCatalog = aggregateCatalog;
	}

	public Type GetViewModelTypeFromViewType(Type sourceType)
	{
		// The default prism view model type resolver as Priority 
		Type targetType = this.GetDefaultViewModelTypeFromViewType(sourceType);
		if (targetType != null)
		{
			return targetType;
		}

		// Get assembly catalogs
		var assemblyCatalogs = this.AggregateCatalog.Catalogs.Where(c => c is AssemblyCatalog);

		// Get all exported types inherit from BindableBase prism class
		var bindableBases =
			assemblyCatalogs.Select(
				c =>
				((AssemblyCatalog)c).Assembly.GetExportedTypes()
					.Where(t => !t.IsAbstract && t.IsSubclassOf(typeof(BindableBase)))
					.Select(t => t)).SelectMany(b =>
					{
						var types = b as IList<Type> ?? b.ToList();
						return types;
					}).Distinct();

		// Get the type where the delegate is applied
		var customConvention = new Func<Type, bool>(
			(Type t) =>
			{
				const string TargetTypeSuffix = "ViewModel";
				var isTypeWithTargetTypeSuffix = t.Name.EndsWith(TargetTypeSuffix);
				return (isTypeWithTargetTypeSuffix)
					   && ((sourceType.Name.EndsWith("View") && sourceType.Name + "Model" == t.Name)
						   || (sourceType.Name + "ViewModel" == t.Name));
			});

		var resolvedTargetType = bindableBases.FirstOrDefault(customConvention);
		return resolvedTargetType;
	}


	private Type GetDefaultViewModelTypeFromViewType(Type viewType)
	{
		var viewName = viewType.FullName;
		viewName = viewName.Replace(".Views.", ".ViewModels.");
		var viewAssemblyName = viewType.GetTypeInfo().Assembly.FullName;
		var suffix = viewName.EndsWith("View") ? "Model" : "ViewModel";
		var viewModelName = String.Format(
			CultureInfo.InvariantCulture,
			"{0}{1}, {2}",
			viewName,
			suffix,
			viewAssemblyName);
		return Type.GetType(viewModelName);
	}
}   

{% endhighlight %}

### Use the custom convention

To use the custom convention, I created a new instance of IMvvmTypeLocator on the application BootStrapper. then i overrided the method ConfigureViewModelLocator. 

##### 1st step:
Create field in the bootstrapper : 

{% highlight csharp %}
private IMvvmTypeLocator mvvmTypeLocator;
{% endhighlight %}

##### 2nd step: 
Create new instance of the class MvvmTypeLocator once the AggregateCatalog is configured: 

{% highlight csharp %}

 protected override void ConfigureAggregateCatalog()
        {
            base.ConfigureAggregateCatalog();
            this.AggregateCatalog.Catalogs.Add(new AssemblyCatalog(Assembly.GetExecutingAssembly()));
			// Here i add the assembly containing all my view models. 
            this.AggregateCatalog.Catalogs.Add(new AssemblyCatalog(typeof(MainViewModel).Assembly));
			
			// Create the new instnace of MvvmTypeLocator.
            this.mvvmTypeLocator = new MvvmTypeLocator(this.AggregateCatalog);
        }
{% endhighlight %}

##### 3rd step: 

Apply the new convention to the ViewModelLocatorProvider: 

{% highlight csharp %}

protected override void ConfigureViewModelLocator()
        {
            base.ConfigureViewModelLocator();

            ViewModelLocationProvider.SetDefaultViewTypeToViewModelTypeResolver(
                viewType => this.mvvmTypeLocator.GetViewModelTypeFromViewType(viewType));
        }
		
{% endhighlight %}


> Note that you are responsible of the view model naming, because this convention will allow the view model locator returning the first found occurence, then ensure that this view model type name is unique.


[1]: https://github.com/PrismLibrary/Prism
[2]: https://msdn.microsoft.com/en-us/library/dd460648(v=vs.110).aspx
