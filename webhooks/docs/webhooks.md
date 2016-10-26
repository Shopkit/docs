# Shopkit Webhooks
Webhooks allow you to build or set up integrations which subscribe to certain events on Shopkit stores.

The webhooks can be used to integrate with third-party services, for example invoicing systems, CRM services or even create notifications and alerts. **[You're only limited by your imagination](https://www.youtube.com/watch?v=B1Kb0WAZ43M)**.

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

| Name                  | Description                                                 |
|-----------------------|-------------------------------------------------------------|
| `order_canceled`      | When an order status is changed to `canceled`               |
| `order_deleted`       | When an order is deleted                                    |
| `order_created`       | When an order is created                                    |
| `order_updated`       | When an order is updated *(any change is made to an order)* |
| `order_paid`          | When an order is set to `paid`                              |
| `order_sent`          | When an order status is changed to `sent`                   |
| `order_change_status` | When an order status is changed                             |
| `order_invoice`       | When an order invoice is requested                          |

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
Content-Length: 1800
X-Shopkit-Event: order_created
```

```json
{
    "order": {
        "id": 1337,
        "total": 92.84,
        "subtotal": 77.32,
        "product_tax": 16.01,
        "total_tax": 16.01,
        "discount": 7.73,
        "shipping": {
            "value": 7.25,
            "tax": 0,
            "tax_percent": 0,
            "discount": 0,
            "discount_percent": 0
        },
        "coupon_code": "bajevolp",
        "created_at": "2014-11-19T00:44:19+00:00",
        "update_at": "2014-11-26T15:30:00+00:00",
        "sent_at": null,
        "paid_at": null,
        "currency": "EUR",
        "payment": {
            "type": "Multibanco",
            "data": {
                "entity": 88888,
                "reference": 888888888,
                "value": 92.84
            }
        },
        "status": 5,
        "status_alias": "waiting_confirmation",
        "paid": false,
        "is_new": true,
        "invoice_url": null,
        "weight": 0,
        "observations": "",
        "custom_field": "",
        "coupon": {
            "code": "bajevolp",
            "type": "percent",
            "value": 10
        },
        "note": "",
        "client_note": "",
        "shipment_method": "Transportadora",
        "client": {
            "name": "Shopkit",
            "email": "info@shopk.it",
            "address": "Centro de Empresas Inovadoras\nAvª do Empresário, 1, S1.08\n",
            "postcode": "6000-767",
            "town": "Castelo Branco",
            "country": "Portugal - Continental",
            "country_code": "PRT",
            "phone": "969057993",
            "fiscal_id": ""
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
                "image":{
                    "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/4778681bb73229d7d038c077c741b7bd.jpg",
                    "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/4778681bb73229d7d038c077c741b7bd.jpg",
                    "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/4778681bb73229d7d038c077c741b7bd.jpg"
                }
            }
        ]
    }
}
```


### Testing

We provide a tool for testing payloads. It's located in the Webhooks section (under the Account settings menu).

This will post a dummy payload to your URL, so you don't need to simulate order events in your store to develop, test and debug.

<small class="last-modified">Last Modified 2016-10-26T17:04:59+01:00</small>
