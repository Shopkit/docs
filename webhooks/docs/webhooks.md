# Shopkit Webhooks
Webhooks allow you to build or set up integrations which subscribe to certain events on Shopkit stores.

The webhooks can be used to integrate with third-party services, for example invoicing systems, CRM services or even create notifications and alerts. **[You're only limited by your imagination](https://www.youtube.com/watch?v=1LAAzzXl5Y8)**.

If you find a bug or something worth fixing, create an issue or a pull request on the **[Github repo](https://github.com/Shopkit/docs)**.

### Workflow

When one of the events is triggered, we'll send a HTTP POST payload to the webhook's configured URL.

We expect a `2xx` status code when requesting your URL.

<div class="callout callout-warning">
    Failed requests will be retried <strong>5 times</strong> in <strong>1 hour</strong> intervals.
    After 5 retries, the webhook will be suspended.
</div>

### Creating a webhook

1. Login into your store.
2. Navigate to the Webhooks section under the Account settings > Developers.
3. Create a webhook by inserting the url and select an event.

<div class="callout callout-info">
    Alternatively, you can create and delete webhooks through the <a href="https://shopk.it/developers/api#webhooks"><strong>Shopkit API</strong></a>.
</div>

### Events

When configuring a webhook, you can choose which events you would like to receive payloads for:

| Name                     | Description                                                 |
|--------------------------|-------------------------------------------------------------|
| `order_canceled`         | When an order status is changed to `canceled`               |
| `order_payment_failed`   | When an order payment failes (expired, canceled, other)     |
| `order_change_payment`   | When an order payment method is changed                     |
| `order_delivered`        | When an order status is changed to `delivered`              |
| `order_shipping`         | When an order shipping is requested                         |
| `order_returned`         | When an order status is changed to `returned`               |
| `order_invoice`          | When an order invoice is requested                          |
| `order_change_status`    | When an order status is changed                             |
| `order_sent`             | When an order status is changed to `sent`                   |
| `order_paid`             | When an order is set to `paid`                              |
| `order_updated`          | When an order is updated *(any change is made to an order)* |
| `order_created`          | When an order is created                                    |
| `order_deleted`          | When an order is deleted                                    |
| `client_updated`         | When an client is updated                                   |
| `client_deleted`         | When an client is deleted                                   |
| `client_created`         | When an client is created                                   |


### Payloads

All webhooks deliver the payload in `application/json` as the body of the HTTP POST request.

#### Headers

The HTTP requests to your webhook's URL will contain a special header `X-Shopkit-Event`, with the name of the event that was triggered.

We also send the `User-Agent` for all requests as `Shopkit-Webhook`.

#### Example

```bash
POST /payload HTTP/1.1

Host: localhost
User-Agent: Shopkit-Webhook
Content-Type: application/json
X-Shopkit-Event: order_updated
X-Webhook-Signature: 6d5a75b42956154a7da8843f56c272428fd43967be1a5474821940b377d061fe
Content-Length: 3484
```

```json
{
    "order": {
        "id": 1337,
        "hash": "a77e38d0b16ba62f32361331774324904278edcf",
        "total": 157.03,
        "subtotal": 148.64,
        "product_tax": 16.0052,
        "total_tax": 16.0052,
        "discount": 14.864,
        "shipping": {
            "value": 7.25,
            "tax": 0,
            "tax_percent": "",
            "discount": 0,
            "discount_percent": 0
        },
        "created_at": "2017-05-17T10:45:05+01:00",
        "update_at": "2017-12-06T17:18:41+00:00",
        "sent_at": "2017-05-17T11:23:21+01:00",
        "paid_at": "2017-05-17T11:23:21+01:00",
        "currency": "EUR",
        "status": 3,
        "status_alias": "sent",
        "status_description": "Sent",
        "paid": true,
        "is_new": false,
        "invoice_url": "https://www.invoiceservice.com/invoice_permalink/",
        "weight": 0,
        "observations": "",
        "note": "",
        "client_note": "",
        "custom_field": "",
        "tracking_code": "",
        "tracking_url": "",
        "shipping_url": "",
        "coupon": {
            "code": "bajevolp",
            "type": "percent",
            "value": 10
        },
        "payment": {
            "data": {
                "entity": 88888,
                "reference": 888888888,
                "value": 157.03
            },
            "title": "Multibanco",
            "method": "multibanco",
            "type": "multibanco",
            "gateway": "gateway"
        },
        "shipment_method": "Transportadora",
        "permalink": "https://parallax.shopk.it/order/a77e38d0b16ba62f32361331774324904278edcf",
        "client": {
            "name": "Shopkit",
            "email": "info@shopk.it",
            "fiscal_id": "999999990",
            "company": "Shopkit",
            "is_registered": false,
            "delivery": {
                "name": "Shopkit",
                "phone": "969057993",
                "address": "Centro de Empresas Inovadoras\nAvª do Empresário",
                "address_extra": "1, S1.08",
                "country": "Portugal - Continental",
                "country_code": "PRT",
                "country_code_alpha_2": "PT",
                "zip_code": "6000-767",
                "city": "Castelo Branco"
            },
            "billing": {
                "name": "Shopkit",
                "phone": "969057993",
                "address": "Centro de Empresas Inovadoras\nAvª do Empresário",
                "address_extra": "1, S1.08",
                "country": "Portugal - Continental",
                "country_code": "PRT",
                "country_code_alpha_2": "PT",
                "zip_code": "6000-767",
                "city": "Castelo Branco"
            },
        },
        "products": [
            {
                "id": 44753,
                "title": "Shelving Tree with Birds",
                "option": "Azul / Small",
                "reference": "STHFBF7574",
                "price": 77.32,
                "tax": 23,
                "quantity": 1,
                "discount": 7.732,
                "subtotal": 85.59324,
                "discount_percent": 10,
                "weight": 0,
                "url": "https://parallax.shopk.it/product/shelving-tree-with-birds",
                "description_short": "This is a tree decal that is created to work with standard 24\" wall shelves that you&#8230;",
                "image": {
                    "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/4778681bb73229d7d038c077c741b7bd.jpg",
                    "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/4778681bb73229d7d038c077c741b7bd.jpg",
                    "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/4778681bb73229d7d038c077c741b7bd.jpg"
                }
            },
            {
                "id": 44752,
                "title": "Hanging Succulent Planter",
                "option": null,
                "reference": "",
                "price": 71.32,
                "tax": 0,
                "quantity": 1,
                "discount": 7.132,
                "subtotal": 64.188,
                "discount_percent": 10,
                "weight": 0,
                "url": "https://parallax.shopk.it/product/hanging-succulent-planter",
                "description_short": "This stoneware planter/pot has been hand made by me from earthy textured, speckled clay&#8230;",
                "image": {
                    "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/eacc633fe509af083776db911a5f02b9.jpg",
                    "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/eacc633fe509af083776db911a5f02b9.jpg",
                    "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/eacc633fe509af083776db911a5f02b9.jpg"
                }
            }
        ]
    }
}
```


### Verifying webhooks

In order to ensure the webhook you received is legit, we suggest you verify its signature. To do that, create an HMAC signed using the SHA256 hash algorithm, using your application’s client_secret and the body of the webhook request as keys, and make sure it matches the webhook’s X-Webhook-Signature header.

```php
hash_hmac('sha256', payload, client_secret);
```

### Testing

We provide a tool for testing payloads. It's located in the Webhooks section (under the Account settings menu).

This will post a dummy payload to your URL, so you don't need to simulate order events in your store to develop, test and debug.

<small class="last-modified">Last Modified 2019-07-12T10:38:11+01:00</small>
