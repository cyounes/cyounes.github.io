---
published: true
title: Display License Keys Section License Manager for WooCommerce
description: >-
  A quick fix for the problem of empty page when clicking on License Keys
  Section in my account page.
comments: true
categories:
  - Tutorials
tags:
  - PHP
  - WordPress
fullview: true
---
I am working on a website built in WordPress to sell license keys with Woocommerce. I found a plugin that allows managing license keys easily and fully integrated with Woocommerce named "[License Manager for WooCommerce](https://wordpress.org/support/plugin/license-manager-for-woocommerce/ "License Manager for WooCommerce")".

This plugin is just perfect, allowed me to manage the customers license keys, generate and display the license keys in the order page. 

However, the main problem I encountered was with the **License Keys** Section in **Woocommerce My Account page**. No license is displayed in the list after assignation to an order. 

After hours of searching in the plugin’s code, if found that the function selecting the licenses from database to display in page "**License Keys**" was filtering postmeta data by key `lmfwc_order_complete`.

{% highlight php %}
$query = "
            SELECT
                DISTINCT(pm1.post_id) AS orderId
            FROM
                {$wpdb->postmeta} AS pm1
            INNER JOIN
                {$wpdb->postmeta} AS pm2
                ON 1=1
                   AND pm1.post_id = pm2.post_id
            WHERE
                1=1
                AND pm1.meta_key = 'lmfwc_order_complete'
                AND pm1.meta_value = '1'
                AND pm2.meta_key = '_customer_user'
                AND pm2.meta_value = '{$userId}'
        ;";
{% endhighlight %}

The key `lmfwc_order_complete` is inserted on database only when the license is generated automatically by the License Generator.

This was not my case as I’m using an offline software to generate the license keys and importing them or manually fulfilling the form to add new key.

When manually entering a key by fulfilling the form or importing from files/clipboard the meta key `lmfwc_order_complete` was not inserted in database. 

## The workaround: 

In order to make it happen, and display the license keys in correctly, I had to edit the plugin code manually and do a call to function `update_post_meta($orderId, 'lmfwc_order_complete', 1)` to set the order as complete from the function `insertImportedLicenseKeys` just before return statement in the class Controller. 

```
Path to file: /public_html/wp-content/plugins/license-manager-for-woocommerce/includes/integrations/woocommerce/Controller.php 
```

{% highlight php %}
public function insertImportedLicenseKeys(
        $licenseKeys,
        $status,
        $orderId,
        $productId,
        $userId,
        $validFor,
        $timesActivatedMax
    ) {
        $result                 = array();
        $cleanLicenseKeys       = array();
        $cleanStatus            = $status            ? absint($status)            : null;
        $cleanOrderId           = $orderId           ? absint($orderId)           : null;
        $cleanProductId         = $productId         ? absint($productId)         : null;
        $cleanUserId            = $userId            ? absint($userId)            : null;
        $cleanValidFor          = $validFor          ? absint($validFor)          : null;
        $cleanTimesActivatedMax = $timesActivatedMax ? absint($timesActivatedMax) : null;

        if (!is_array($licenseKeys)) {
            throw new Exception('License Keys must be an array');
        }

        if (!$cleanStatus) {
            throw new Exception('Status enumerator is missing');
        }

        if (!in_array($cleanStatus, LicenseStatus::$status)) {
            throw new Exception('Status enumerator is invalid');
        }

        foreach ($licenseKeys as $licenseKey) {
            array_push($cleanLicenseKeys, sanitize_text_field($licenseKey));
        }

        $result['added']  = 0;
        $result['failed'] = 0;

        // Add the keys to the database table.
        foreach ($cleanLicenseKeys as $licenseKey) {
            $license = LicenseResourceRepository::instance()->insert(
                array(
                    'order_id'            => $cleanOrderId,
                    'product_id'          => $cleanProductId,
                    'user_id'             => $cleanUserId,
                    'license_key'         => apply_filters('lmfwc_encrypt', $licenseKey),
                    'hash'                => apply_filters('lmfwc_hash', $licenseKey),
                    'valid_for'           => $cleanValidFor,
                    'source'              => LicenseSource::IMPORT,
                    'status'              => $cleanStatus,
                    'times_activated_max' => $cleanTimesActivatedMax,
                )
            );

            if ($license) {
                $result['added']++;
            }

            else {
                $result['failed']++;
            }
        }
		
		update_post_meta($cleanOrderId, 'lmfwc_order_complete', 1);

        return $result;
    }
    {% endhighlight %}
    
    
    > This change worked on plugin version **2.2.2** 







