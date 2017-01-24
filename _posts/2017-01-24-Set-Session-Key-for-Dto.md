---
layout: post
title: 'How to set a dto session key when calling WCF proxy'
description: Handle all DTOs by setting a session key before sending to WCF host using expression lambda
comments: true
--- 

The power of the following method is avoid to implement the WCF contract client in the client side and duplicate the code for each call.
Using Reflections and Expression Lambda to handle each message before send it. 
The follwing code has 3 steps specified by regions :
+ Update the DTO.
+ Initilialize the proxy if the channel is in status Faulted.
+ Invoke the contract operation

{% highlight csharp %}
public static Task<RequestResponse> SendRequestAsync(Expression<Func<IUiContract, Task<RequestResponse>>> expression)
        {
            #region Set Session Key

            var call = expression.Body as MethodCallExpression;
            if (call != null)
            {
                var argument = call.Arguments[0];
                if (argument != null)
                {
                    LambdaExpression lambda = Expression.Lambda(argument, expression.Parameters);
                    Delegate d = lambda.Compile();
                    var dto = d.DynamicInvoke(new object[1]) as RequestDTO;
                    if (dto != null)
                    {
                        dto.SessionKey = ClientSession.GetSessionKey();
                    }
                }
            }

            #endregion

            #region Initialize Proxy if Faulted

            // ReSharper disable once PossibleNullReferenceException
            if ((Instance._proxy as ICommunicationObject).State == CommunicationState.Faulted)
                Instance.InitializeProxy();

            #endregion

            var func = expression.Compile();
            return func.Invoke(Instance._proxy);
        }
{% endhighlight %}

## Call the method from another class code: 

{% highlight csharp %}
  ServiceClient.SendRequestAsync(contract => contract.AddUserAsync(dto));
{% endhighlight %}

