FORMAT: 1A
HOST: https://api.shopk.it/v1

# Shopkit API
Welcome to the **Shopkit** REST API documentation.

For now there are only a few available methods. We will add more over time.

If you have a suggestion, find a bug or something worth fixing, create an issue or a pull request on the **[Github repo](https://github.com/Shopkit/docs)**.

<small class="last-modified">Last Modified 2021-09-06T09:15:58+01:00</small>

### API Status
<div class="api-status" style="display:none;">
    <h6>-</h6>
    <div class="metrics">Response time: <strong><span class="response_time">-</span>ms</strong></div>
</div>

### Authentication
You must first create a new API key from your store administration area:

1. Login into your store.
2. Navigate to the API section under the Account settings > Developers.
3. Create a new API key

**Do not share your API keys with other users or store them in insecure places.**

All requests to the API must be authenticated with an API key in one of two ways:

1. In the URL as the `X-API-KEY` parameter:

```http
https://api.shopk.it/v1/?X-API-KEY=f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c
```

2. In the HTTP Authorization header:

```http
X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c
```

### Endpoints
All API requests are made to https://api.shopk.it/ and all requests are served over **HTTPS**. The current version is **v1**.

### Schema
The API only supports JSON. <small class="text-light">(2005 called and wants its XML back)</small>.

All timestamps are returned in ISO 8601 format: `YYYY-MM-DDTHH:MM:SS±HH:MM`.

### HTTP Verbs
Where possible, the API strives to use appropriate HTTP verbs for each action.

<div class="well">

Verb | Description
---- | -----------
`GET` | Used for retrieving resources.
`POST` | Used for creating resources.
`PUT` | Used for updating resources, or performing custom actions.
`DELETE` | Used for deleting resources.

</div>

### Rate Limiting
You can make up to **3600** requests per hour.

### Pagination
Requests that return multiple items will be paginated to **25** items by default.

You can specify further pages with the `page` parameter. For some resources, you can also set a custom page size up to **50** with the `limit` parameter.

```json
{
   "paging" : {
      "previous" : "https://api.shopk.it/v1/product?limit=50&page=1",
      "next" : "https://api.shopk.it/v1/product?limit=50&page=3"
   }
}
```

Note that omitting the `page` parameter will return the first page.

Note that for technical reasons not all endpoints respect the `limit` parameter.

#### Total count
All resources with pagination have the total count of items added as an header `X-Total-Count`.

```http
X-Total-Count: 1000
```


### Errors
There are 3 possible types of client errors on API calls: **400**, **401** and **404**.

An error will return JSON in the following format:

```json
{
  "message" : "Bad request"
}
```

### Making a request
If you are sending data to the API, you need to make sure you correctly set the `Content-Type` header.

This is a simple example on how to update an order:

```bash
curl -X PUT 'https://api.shopk.it/v1/order/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c' \
-H 'Content-Type: application/json' \
-d '{"paid":true, "status_alias":"sent"}'
```

Response: `200 OK`

```json
{
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
        "tax_percent": null,
        "discount": 0,
        "discount_percent": 0
    },
    "created_at": "2017-05-17T10:45:05+01:00",
    "update_at": "2017-12-06T17:18:41+00:00",
    "sent_at": "2017-05-17T11:23:21+01:00",
    "paid_at": "2017-05-17T11:23:21+01:00",
    "currency": "EUR",
    "payment": {
        "type": "multibanco",
        "data": {
            "entity": 88888,
            "reference": 888888888,
            "value": 157.03
        },
        "description": "Multibanco"
    },
    "status": 3,
    "status_alias": "sent",
    "status_description": "Sent",
    "paid": true,
    "is_new": false,
    "invoice_url": "https://www.invoiceservice.com/invoice_permalink/",
    "weight": 0,
    "observations": null,
    "note": null,
    "client_note": null,
    "custom_field": null,
    "tracking_code": null,
    "tracking_url": "",
    "shipping_url": null,
    "coupon": {
        "code": "bajevolp",
        "type": "percent",
        "value": 10
    },
    "shipment_method": "Transportadora",
    "permalink": "https://parallax.shopk.it/order/a77e38d0b16ba62f32361331774324904278edcf",
    "client": {
        "name": "Shopkit",
        "email": "info@shopk.it",
        "fiscal_id": null,
        "company": "Shopkit",
        "is_registered": false,
        "delivery": {
            "name": "Shopkit",
            "phone": "969057993",
            "address": "Centro de Empresas Inovadoras\\nAvª do Empresário",
            "address_extra": "1, S1.08",
            "country": "Portugal - Continental",
            "country_code": "PRT",
            "zip_code": "6000-767",
            "city": "Castelo Branco"
        },
        "billing": {
            "name": "Shopkit",
            "phone": "969057993",
            "address": "Centro de Empresas Inovadoras\\nAvª do Empresário",
            "address_extra": "1, S1.08",
            "country": "Portugal - Continental",
            "country_code": "PRT",
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
                "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/4778681bb73229d7d038c077c741b7bd.jpg",
                "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/4778681bb73229d7d038c077c741b7bd.jpg",
                "full": "https://cdn.shopk.it/usercontent/parallax/media/images/4778681bb73229d7d038c077c741b7bd.jpg"
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
                "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/eacc633fe509af083776db911a5f02b9.jpg",
                "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/eacc633fe509af083776db911a5f02b9.jpg",
                "full": "https://cdn.shopk.it/usercontent/parallax/media/images/eacc633fe509af083776db911a5f02b9.jpg"
            }
        }
    ]
}
```


### Resources

# Group Store

## GET store [/store]

### GET store [GET]
Get store info. **No parameters**

```bash
curl -X GET 'https://api.shopk.it/v1/store' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Response 200 (application/json)

    + Body

            {
                "username": "parallax",
                "name": "Parallax",
                "logo": null,
                "description": "A Shopkit é um serviço que te permite criar a tua loja online de forma fácil, prática e adequada ao teu tipo de negócio. O processo é simples e rápido. Em 5 minutos estás pronto para começar a vender os teus produtos online.",
                "notice": "Portes grátis para encomendas superiores a 59€",
                "facebook": "https://www.facebook.com/shopkit",
                "twitter": "https://twitter.com/shopkit_pt",
                "instagram": "https://www.instagram.com/shopk.it/",
                "pinterest": null,
                "show_email": false,
                "enable_shipping_methods": true,
                "email": "info@shopk.it",
                "phone": null,
                "cellphone": "(+351) 969 057 993",
                "address": "Avª do Empresário, 1, S1.08\n6000-767 Castelo Branco",
                "basecolor": "#db0a5b",
                "favicon": null,
                "latitude": "39.818466068593935",
                "longitude": "-7.491968556808545",
                "currency": "EUR",
                "footer_info": "Os produtos listados são apenas de apresentação e não se encontram à venda.",
                "page_title": "Parallax",
                "meta_description": "A Shopkit é um serviço que te permite criar a tua loja on-line de forma fácil, prática e adequada ao teu tipo de negócio. O processo é simpl",
                "meta_tags": null,
                "basecolor_contrast": "#FFFFFF",
                "secondarycolor": null,
                "secondarycolor_contrast": "#FFFFFF",
                "settings": {
                    "cart": {
                        "users_registration": "optional",
                        "field_company": "optional",
                        "field_fiscal_id": "optional",
                        "field_delivery_phone": "optional",
                        "field_billing_phone": "optional",
                        "page_terms": {
                            "id": "10713",
                            "title": "Termos e condições",
                            "url": "https://parallax.shopk.it/page/termos-e-condicoes",
                            "handle": "termos-e-condicoes"
                        },
                        "page_privacy": {
                            "id": "10714",
                            "title": "Politica de Privacidade",
                            "url": "https://parallax.shopk.it/page/politica-de-privacidade",
                            "handle": "politica-de-privacidade"
                        }
                    },
                    "order": {
                        "status_cancel": null
                    },
                    "category": {
                        "default_order": "position"
                    },
                    "categories": {
                        "sorting": "position",
                        "per_page": null
                    },
                    "abandoned": {
                        "carts_automatic_notifications": false,
                        "carts_client_notification": null,
                        "carts_notification_type": null,
                        "carts_send_after": null,
                        "carts_coupon": null,
                        "carts_email_subject": "{{ cart.client_name|first_word }}, deixou produtos no seu carrinho",
                        "carts_email_lead": "Reparámos que deixou produtos no seu carrinho de compras. Finalize a encomenda para garantir os seus produtos."
                    },
                    "products": {
                        "per_page_home": null,
                        "per_page_catalog": null
                    },
                    "brands": {
                        "per_page": null
                    }
                },
                "url": "https://parallax.shopk.it/",
                "theme": "shopkit-parallax",
                "theme_origin": "shopkit-parallax",
                "navigation": {
                    "primary": [
                        {
                            "menu_text": "Home",
                            "menu_type": "menu_page",
                            "menu_url": "https://parallax.shopk.it",
                            "menu_item": "/",
                            "target_blank": false
                        },
                        {
                            "menu_text": "Sobre nós",
                            "menu_type": "menu_page",
                            "menu_url": "https://parallax.shopk.it/about",
                            "menu_item": "about",
                            "target_blank": false
                        },
                        {
                            "menu_text": "Blog",
                            "menu_type": "menu_page",
                            "menu_url": "https://parallax.shopk.it/blog",
                            "menu_item": "blog",
                            "target_blank": false
                        },
                        {
                            "menu_text": "Promoções",
                            "menu_type": "menu_page",
                            "menu_url": "https://parallax.shopk.it/sales",
                            "menu_item": "sales",
                            "target_blank": false
                        },
                        {
                            "menu_text": "Novidades",
                            "menu_type": "menu_page",
                            "menu_url": "https://parallax.shopk.it/new",
                            "menu_item": "new",
                            "target_blank": false
                        },
                        {
                            "menu_text": "Contactos",
                            "menu_type": "menu_page",
                            "menu_url": "https://parallax.shopk.it/contact",
                            "menu_item": "contact",
                            "target_blank": false
                        }
                    ],
                    "secondary": [
                        {
                            "menu_text": "Termos e condições",
                            "menu_type": "menu_page",
                            "menu_url": "https://parallax.shopk.it/page/termos-e-condicoes",
                            "menu_item": "10713",
                            "target_blank": false
                        },
                        {
                            "menu_text": "Politica de Privacidade",
                            "menu_type": "menu_page",
                            "menu_url": "https://parallax.shopk.it/page/politica-de-privacidade",
                            "menu_item": "10714",
                            "target_blank": false
                        }
                    ]
                },
                "payments": {
                    "credit_card": {
                        "active": true,
                        "message": "Instruções método de pagamento Cartão de Crédito.",
                        "description": "Pague de forma segura com cartão de crédito ou débito.",
                        "default": false,
                        "gateway": "stripe",
                        "method": "credit_card",
                        "alias": "credit_card",
                        "title": "Cartão de Crédito",
                        "image": "https://cdn.shopk.it/templates/assets/common/icons/payments/credit_card-pt.png",
                        "logo": "https://cdn.shopk.it/templates/assets/common/icons/payments/credit-card-brands.png"
                    },
                    "multibanco": {
                        "active": true,
                        "message": "Este texto é personalizável e apenas aparecerá aos clientes que seleccionarem o método de pagamento Multibanco.",
                        "description": "O método de pagamento mais utilizado pelos portugueses para pagamentos online.",
                        "default": true,
                        "gateway": "stripe",
                        "method": "multibanco",
                        "alias": "multibanco",
                        "title": "Multibanco",
                        "image": "https://cdn.shopk.it/templates/assets/common/icons/payments/multibanco-pt.png",
                        "logo": "https://cdn.shopk.it/templates/assets/common/icons/payments/multibanco-color.png"
                    },
                    "mbway": {
                        "active": true,
                        "message": "Instruções método de pagamento MB WAY.",
                        "description": "Pague de forma rápida e segura usando o seu telemóvel.",
                        "default": false,
                        "gateway": "easypay",
                        "method": "mbway",
                        "alias": "mbway",
                        "title": "MB WAY",
                        "image": "https://cdn.shopk.it/templates/assets/common/icons/payments/mbway-pt.png",
                        "logo": "https://cdn.shopk.it/templates/assets/common/icons/payments/mbway-color.png"
                    },
                    "paypal": {
                        "active": true,
                        "email": "info@shopk.it",
                        "message": "Este texto é personalizável e apenas aparecerá aos clientes que seleccionarem o método de pagamento Paypal.",
                        "description": "Pague de forma rápida e segura usando a sua conta Paypal.",
                        "default": false,
                        "gateway": "paypal",
                        "method": "paypal",
                        "alias": "paypal",
                        "title": "Paypal",
                        "image": "https://cdn.shopk.it/templates/assets/common/icons/payments/paypal-pt.png",
                        "logo": "https://cdn.shopk.it/templates/assets/common/icons/payments/paypal-color.png"
                    },
                    "bank_transfer": {
                        "active": true,
                        "message": "Este texto é personalizável e apenas aparecerá aos clientes que seleccionarem o método de pagamento Transferência Bancária.",
                        "description": "Pague por transferência bancária ou interbancária.",
                        "default": false,
                        "gateway": "manual",
                        "method": "bank_transfer",
                        "alias": "bank_transfer",
                        "title": "Transferência Bancária",
                        "image": "https://cdn.shopk.it/templates/assets/common/icons/payments/bank_transfer-pt.png"
                    },
                    "on_delivery": {
                        "active": true,
                        "value": 0,
                        "message": "Este texto é personalizável e apenas aparecerá aos clientes que seleccionarem o método de pagamento À Cobrança.",
                        "description": "Pagamento contra reembolso.",
                        "default": false,
                        "gateway": "manual",
                        "method": "on_delivery",
                        "alias": "on_delivery",
                        "title": "À Cobrança",
                        "image": "https://cdn.shopk.it/templates/assets/common/icons/payments/on_delivery-pt.png"
                    },
                    "pick_up": {
                        "active": true,
                        "message": "Este texto é personalizável e apenas aparecerá aos clientes que seleccionarem o método de pagamento Levantamento nas instalações.",
                        "description": "Levante a sua encomenda nas nossas instalações. Não paga portes de envio.",
                        "default": false,
                        "gateway": "manual",
                        "method": "pick_up",
                        "alias": "pick_up",
                        "title": "Levantamento nas instalações",
                        "image": "https://cdn.shopk.it/templates/assets/common/icons/payments/pick_up-pt.png"
                    },
                    "custom": {
                        "active": true,
                        "title": "Instruções metodo de Ppagamento personalizado",
                        "message": "Instruções método de pagamento Pagamento personalizado",
                        "description": "Define um método de pagamento personalizado por ti",
                        "default": false,
                        "gateway": "manual",
                        "method": "custom",
                        "alias": "custom",
                    }
                },
                "locations": [
                    {
                        "id": "469",
                        "title": "Morada Principal",
                        "name": "Shopkit",
                        "address": "Avenida do Empresário, 1",
                        "address_extra": "S1.19",
                        "city": "Castelo Branco",
                        "zip_code": "6000-767",
                        "country": "Portugal - Continental",
                        "country_code": "PRT",
                        "phone": "+351919873646"
                    }
                ],
                "domain": "parallax.shopk.it",
                "is_ssl": true,
                "assets": {
                    "url": "https://cdn.shopk.it/templates/assets/shopkit/parallax",
                    "images": "https://cdn.shopk.it/templates/assets/shopkit/parallax/img",
                    "css": "https://cdn.shopk.it/css/store/parallax/style.css?template=shopkit/parallax&amp;last_modified=1504786507",
                    "plugins": "https://cdn.shopk.it/templates/assets/shopkit/parallax/js/plugins.js?template=shopkit/parallax&amp;last_modified=1504786507",
                    "scripts": "https://cdn.shopk.it/templates/assets/shopkit/parallax/js/script.js?template=shopkit/parallax&amp;last_modified=1504786507"
                },
                "images_header": [
                    "https://cdn.shopk.it/usercontent/parallax/media/images/14bb24a112fafccdd36680be2b03f4ce.jpg",
                    "https://cdn.shopk.it/usercontent/parallax/media/images/c788681a62eff02c640765d3c215c920.jpg",
                    "https://cdn.shopk.it/usercontent/parallax/media/images/f669d550743b2e27a81c22812b270101.jpg"
                ],
                "featured_blocks": null,
                "dark_mode": null,
                "taxes_included": true
            }


# Group Products

## GET product [/product{?id,ids,handle,category,status,status_alias,reference,featured,new,q,page,limit}]

### GET product [GET]
Get a list of products or single product by id or handle.

```bash
curl -X GET 'https://api.shopk.it/v1/product/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'

curl -X GET 'https://api.shopk.it/v1/product/?category=1337&limit=5' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (optional, integer, `1337`) ... Product identifier
    + ids (optional, integer, `1337,7331`) ... Products identifier, comma separated
    + handle (optional, string, `rustic-bowl`) ... Product handle
    + category (optional, integer, `1337`) ... Product category identifier
    + status (optional, integer, `0`) ... Product status as an integer
        + Values
            + `0`
            + `1`
            + `2`
            + `3`
            + `4`

    + status_alias (optional, string, `all`) ... Product status as a string
        + Values
            + `all`
            + `active`
            + `hidden`
            + `out_of_stock`
            + `soon`

    + reference (optional, string, `bowl-001`) ... Product reference
    + featured (optional, boolean, `true`) ... Product featured field
        + Values
            + `true`
            + `false`

    + new (optional, boolean, `true`) ... Product new field
        + Values
            + `true`
            + `false`
    + q (optional, string, `bowl`) ... Search for products
    + page (optional, integer, `1`) ... page number
    + limit = `25` (optional, integer, `10`) ... products per page

+ Response 200 (application/json)

    + Body

            {
                "id": 212322,
                "title": "Rustic Spice Bowl Set",
                "reference": "",
                "barcode": null,
                "price": 40.73,
                "price_formatted": "40,73 €",
                "price_promo": null,
                "price_promo_formatted": null,
                "promo_show_percentage": false,
                "price_promo_percentage": null,
                "price_on_request": false,
                "created_at": "2020-11-27T15:36:57+00:00",
                "status": 1,
                "status_alias": "active",
                "position": 0,
                "shipping": 0,
                "shipping_alone": false,
                "featured": false,
                "new": true,
                "is_promotion": false,
                "description": "<p>This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay. After shaping and drying, I bisque fired them and then glazed them in contrasting shades of white and dark turquoise. Pieces then went back into the kiln and were high fired, giving them strength and durability. These bowls are ideal for spices, dukkah, oil, chopped chilli or garlic.&nbsp;<br /><br />In many of my ceramic pieces you will find slight imperfections and marks left by the handmade process. These contribute to the uniqueness and beauty of the forms and are simply part of the character of the individual piece.<br /><br />Larger size (x2) - 8cm (3\") across, 5cm (2\") deep<br />Mid size - 7cm (2.5\") across, 5cm (2\") deep<br />Small size - 5cm (2\") across, 4cm (1.5\") deep<br /><br />Please Note : These items are MADE TO ORDER and may vary slightly from the image shown. Current make time is 2-3 weeks.&nbsp;<br /><br />*food, oven and dishwasher safe<br />*not suitable for microwave</p>",
                "excerpt": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy",
                "video_url": "",
                "file": null,
                "tax": 0,
                "taxable": false,
                "reduced_rate": null,
                "meta_description": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay. After shaping and drying, I bisque fir",
                "meta_tags": "",
                "handle": "rustic-spice-bowl-set",
                "page_title": "Rustic Spice Bowl Set",
                "weight": 0,
                "hits": 0,
                "sales": 0,
                "variants_same_values": false,
                "updated_at": "2020-11-27T15:36:57+00:00",
                "description_short": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy",
                "promo": false,
                "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set",
                "add_cart_url": "https://parallax.shopk.it/cart/add/rustic-spice-bowl-set",
                "wishlist": {
                    "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set",
                    "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set"
                },
                "permalink": "https://parallax.shopk.it/product/rustic-spice-bowl-set",
                "video_embed_url": false,
                "image": {
                    "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                    "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                    "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                },
                "images": [
                    {
                        "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/f519f86-17d23f7b534bf365580989363da328d2.jpg",
                        "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/f519f86-17d23f7b534bf365580989363da328d2.jpg",
                        "full": "https://cdn.shopk.it/usercontent/parallax/media/images/f519f86-17d23f7b534bf365580989363da328d2.jpg"
                    },
                    {
                        "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/0bb2c71-7d2fe8d66dd9925ac72a3112d691f352.jpg",
                        "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/0bb2c71-7d2fe8d66dd9925ac72a3112d691f352.jpg",
                        "full": "https://cdn.shopk.it/usercontent/parallax/media/images/0bb2c71-7d2fe8d66dd9925ac72a3112d691f352.jpg"
                    },
                    {
                        "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/717897d-ff2216454ebbf8ca2727335ecacbc472.jpg",
                        "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/717897d-ff2216454ebbf8ca2727335ecacbc472.jpg",
                        "full": "https://cdn.shopk.it/usercontent/parallax/media/images/717897d-ff2216454ebbf8ca2727335ecacbc472.jpg"
                    }
                ],
                "categories": [
                    {
                        "id": 44355,
                        "parent": 0,
                        "active": true,
                        "title": "Cozinha",
                        "description": "",
                        "handle": "cozinha",
                        "url": "https://parallax.shopk.it/category/cozinha",
                        "image": []
                    }
                ],
                "brand": null,
                "tags": [],
                "options": [
                    {
                        "id": 363364,
                        "id_variant_1": 206585,
                        "id_variant_2": 206587,
                        "id_variant_3": null,
                        "title": "Small bowl / White",
                        "price": 40.73,
                        "price_formatted": "40,73 €",
                        "price_promo": null,
                        "price_promo_formatted": null,
                        "promo": false,
                        "price_promo_percentage": null,
                        "price_on_request": false,
                        "stock": 88,
                        "shipping": 0,
                        "weight": 0,
                        "reference": "",
                        "barcode": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363364",
                        "image": {
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363364",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363364"
                        }
                    },
                    {
                        "id": 363365,
                        "id_variant_1": 206585,
                        "id_variant_2": 206588,
                        "id_variant_3": null,
                        "title": "Small bowl / Dark turquoise",
                        "price": 40.73,
                        "price_formatted": "40,73 €",
                        "price_promo": null,
                        "price_promo_formatted": null,
                        "promo": false,
                        "price_promo_percentage": null,
                        "price_on_request": false,
                        "stock": 94,
                        "shipping": 0,
                        "weight": 0,
                        "reference": "",
                        "barcode": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363365",
                        "image": {
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363365",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363365"
                        }
                    },
                    {
                        "id": 363366,
                        "id_variant_1": 206586,
                        "id_variant_2": 206587,
                        "id_variant_3": null,
                        "title": "Big bowl / White",
                        "price": 45.73,
                        "price_formatted": "45,73 €",
                        "price_promo": null,
                        "price_promo_formatted": null,
                        "promo": false,
                        "price_promo_percentage": null,
                        "price_on_request": false,
                        "stock": 100,
                        "shipping": 0,
                        "weight": 0,
                        "reference": "",
                        "barcode": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363366",
                        "image": {
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363366",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363366"
                        }
                    },
                    {
                        "id": 363367,
                        "id_variant_1": 206586,
                        "id_variant_2": 206588,
                        "id_variant_3": null,
                        "title": "Big bowl / Dark turquoise",
                        "price": 45.73,
                        "price_formatted": "45,73 €",
                        "price_promo": null,
                        "price_promo_formatted": null,
                        "promo": false,
                        "price_promo_percentage": null,
                        "price_on_request": false,
                        "stock": 100,
                        "shipping": 0,
                        "weight": 0,
                        "reference": "",
                        "barcode": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363367",
                        "image": {
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363367",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363367"
                        }
                    }
                ],
                "option_groups": [
                    {
                        "id": 62775,
                        "title": "Size",
                        "options": [
                            {
                                "id": 206585,
                                "title": "Small bowl"
                            },
                            {
                                "id": 206586,
                                "title": "Big bowl"
                            }
                        ]
                    },
                    {
                        "id": 62776,
                        "title": "Color",
                        "options": [
                            {
                                "id": 206587,
                                "title": "White"
                            },
                            {
                                "id": 206588,
                                "title": "Dark turquoise"
                            }
                        ]
                    }
                ],
                "stock": {
                    "stock_enabled": true,
                    "stock_qty": 88,
                    "stock_backorder": true,
                    "stock_show": true,
                    "stock_sold_single": true,
                    "stock_notify": 10
                },
                "rating": {
                    "total_reviews": 0,
                    "average_rating": 0,
                    "max_rating": 0,
                    "min_rating": 0
                },
                "custom_fields": null,
                "tabs": null
            }

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## POST product [/product]

### POST product [POST]
Create a product.

```bash
curl -X POST 'https://api.shopk.it/v1/product/' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c' \
-H 'Content-Type: application/json' \
-d '{"title": "Rustic Spice Bowl Set", "price": 17.45, "categories": [44373]}'
```

<div class="well">

Attributes | Type | Choices | Description
---------- | ---- | ------- | -----------
**title**<br>(required) | string | | Title
**price**<br>(required) | float | | Price **Required** if not `price_on_request`
**categories**<br>(required) | array[integer] | | Array with categories identifier
**brand** | integer | | Brand identifier
**handle** | string | | Handle
**reference** | string | | SKU
**barcode** | string | | EAN, ISBN, UPC, GTIN, etc.
**price_promo** | float | | Promotion price (must be lower than price)
**promo_show_percentage** | boolean | `true` `false` | Show discount in percent
**price_on_request** | boolean | `true` `false` | Price is on request
**status** | integer | `1` `2` `3` `4` | Status: `1` (active) `2` (hidden) `3` (out of stock) `4` (soon)
**shipping** | float | | Shipping cost
**shipping_alone** | boolean | `true` `false` | Shipping alone option
**featured** | boolean | `true` `false` | Product is featured option
**new** | boolean | `true` `false` | Product is new option
**is_promotion** | boolean | `true` `false` | Product is in promotion option
**description** | string | | Description
**excerpt** | string | | Excerpt (short description)
**video_url** | string | | Video url, youtube or vimeo url
**file** | string | | File url
**tax** | float | | Tax (**deprecated** in favor of taxable)
**taxable** | boolean | | Product is taxable
**reduced_rate** | string | [choices](https://shopk.it/iva-vat-eu?lang=en#reduced-rates) | VAT reduced rate
**meta_description** | string | | Meta description
**meta_tags** | string | | Meta tags
**page_title** | string | | Product page title
**weight** | integer | | Weight (in grams)
**images** | array[string] | | Array with images url, max 10
**tags** | array[string] | | Array with tags
**stock_enabled** | boolean | `true` `false` | Enables Product stock
**stock_qty** | integer | | Units in stock (requires product stock enabled)
**stock_backorder** | boolean | `true` `false` | Allows to receice orders without units in stock (requires stock enabled)
**stock_show** | boolean | `true` `false` | Show product stock units (requires stock enabled)
**stock_sold_single** | boolean | `true` `false` | Only allow to sell 1 unit per order (requires stock enabled)
**stock_notify** | integer | | Product minium stock units (requires stock enabled)

</div>

+ Request (application/json)

        {
            "title": "Rustic Spice Bowl Set",
            "price": 17.45,
            "categories": [
                44373
            ]
        }

+ Response 201 (application/json)

    + Body

            {
                "id": 212314,
                "title": "Rustic Spice Bowl Set",
                "reference": null,
                "barcode": null,
                "price": 17.45,
                "price_formatted": "17,45 €",
                "price_promo": null,
                "price_promo_formatted": null,
                "promo_show_percentage": false,
                "price_promo_percentage": null,
                "price_on_request": false,
                "created_at": "2020-11-27T14:07:10+00:0",
                "status": 1,
                "status_alias": "active",
                "position": 0,
                "shipping": 0,
                "shipping_alone": false,
                "featured": false,
                "new": false,
                "is_promotion": false,
                "description": null,
                "excerpt": "",
                "video_url": null,
                "file": null,
                "tax": 0,
                "taxable": false,
                "reduced_rate": null,
                "meta_description": null,
                "meta_tags": null,
                "handle": "rustic-spice-bowl-set",
                "page_title": "Rustic Spice Bowl Set",
                "weight": 0,
                "hits": 0,
                "sales": 0,
                "variants_same_values": true,
                "updated_at": "2020-11-27T14:07:10+00:00",
                "description_short": "",
                "promo": false,
                "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set",
                "add_cart_url": "https://parallax.shopk.it/cart/add/rustic-spice-bowl-set",
                "wishlist": {
                    "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set",
                    "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set"
                },
                "permalink": "https://parallax.shopk.it/product/rustic-spice-bowl-set",
                "video_embed_url": false,
                "image": {
                    "thumb": "https://cdn.shopk.it/assets/store/img/no-img.jpg",
                    "square": "https://cdn.shopk.it/assets/store/img/no-img.jpg",
                    "full": "https://cdn.shopk.it/assets/store/img/no-img.jpg"
                },
                "images": [],
                "categories": [
                    {
                        "id": 44373,
                        "parent": 0,
                        "active": true,
                        "title": "Cozinha",
                        "description": "",
                        "handle": "cozinha",
                        "url": "https://parallax.shopk.it/category/cozinha",
                        "image": []
                    }
                ],
                "brand": null,
                "tags": [],
                "options": [],
                "option_groups": [],
                "stock": {
                    "stock_enabled": false
                },
                "rating": {
                    "total_reviews": 0,
                    "average_rating": 0,
                    "max_rating": 0,
                    "min_rating": 0
                },
                "custom_fields": null,
                "tabs": null
            }

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## PUT product [/product/{id}]

### PUT product [PUT]
Update a product.

```bash
curl -X POST 'https://api.shopk.it/v1/product/' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c' \
-H 'Content-Type: application/json' \
-d'{"reference": "SWB-001", "featured": true}'
```

<div class="well">

Attributes | Type | Choices | Description
---------- | ---- | ------- | -----------
**title** | string | | Title
**price** | float | | Price
**categories** | array[integer] | | Array with categories identifier
**brand** | integer | | Brand identifier
**handle** | string | | Handle
**reference** | string | | SKU
**barcode** | string | | EAN, ISBN, UPC, GTIN, etc.
**price_promo** | float | | Promotion price (must be lower than price)
**promo_show_percentage** | boolean | `true` `false` | Show discount in percent
**price_on_request** | boolean | `true` `false` | Price is on request
**status** | integer | `1` `2` `3` `4` | Status: `1` (active) `2` (hidden) `3` (out of stock) `4` (soon)
**shipping** | float | | Shipping cost
**shipping_alone** | boolean | `true` `false` | Shipping alone option
**featured** | boolean | `true` `false` | Product is featured option
**new** | boolean | `true` `false` | Product is new option
**is_promotion** | boolean | `true` `false` | Product is in promotion option
**description** | string | | Description
**excerpt** | string | | Excerpt (short description)
**video_url** | string | | Video url, youtube or vimeo url
**file** | string | | File url
**tax** | float | | Tax (**deprecated** in favor of taxable)
**taxable** | boolean | | Product is taxable
**reduced_rate** | string | [choices](https://shopk.it/iva-vat-eu?lang=en#reduced-rates) | VAT reduced rate
**meta_description** | string | | Meta description
**meta_tags** | string | | Meta tags
**page_title** | string | | Product page title
**weight** | integer | | Weight (in grams)
**images** | array[string] | | Array with images url, max 10
**tags** | array[string] | | Array with tags
**stock_enabled** | boolean | `true` `false` | Enables Product stock
**stock_qty** | integer | | Units in stock (requires product stock enabled)
**stock_backorder** | boolean | `true` `false` | Allows to receice orders without units in stock (requires stock enabled)
**stock_show** | boolean | `true` `false` | Show product stock units (requires stock enabled)
**stock_sold_single** | boolean | `true` `false` | Only allow to sell 1 unit per order (requires stock enabled)
**stock_notify** | integer | | Product minium stock units (requires stock enabled)

</div>

+ Parameters

    + id (required, integer) ... Product identifier

+ Request (application/json)

        {
          "reference": "SWB-001",
          "featured": true
        }

+ Response 200 (application/json)

    + Body

            {
                "id": 212314,
                "title": "Rustic Spice Bowl Set",
                "reference": "bowl-001",
                "price": 17.45,
                "price_formatted": "17,45 €",
                "price_promo": null,
                "price_promo_formatted": null,
                "promo_show_percentage": false,
                "price_promo_percentage": null,
                "price_on_request": false,
                "created_at": "2020-11-27T14:07:10+00:00",
                "status": 1,
                "status_alias": "active",
                "position": 0,
                "shipping": 0,
                "shipping_alone": false,
                "featured": false,
                "new": false,
                "is_promotion": false,
                "description": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay",
                "excerpt": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy",
                "video_url": null,
                "file": null,
                "tax": 0,
                "taxable": false,
                "reduced_rate": null,
                "meta_description": null,
                "meta_tags": null,
                "handle": "rustic-spice-bowl-set-2",
                "page_title": "Rustic Spice Bowl Set",
                "weight": 0,
                "hits": 0,
                "sales": 0,
                "variants_same_values": true,
                "updated_at": "2020-11-27T15:15:12+00:00",
                "description_short": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy&#8230;",
                "promo": false,
                "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set-2",
                "add_cart_url": "https://parallax.shopk.it/cart/add/rustic-spice-bowl-set-2",
                "wishlist": {
                    "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set-2",
                    "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set-2"
                },
                "permalink": "https://parallax.shopk.it/product/rustic-spice-bowl-set-2",
                "video_embed_url": false,
                "image": {
                    "thumb": "https://cdn.shopk.it/assets/store/img/no-img.jpg",
                    "square": "https://cdn.shopk.it/assets/store/img/no-img.jpg",
                    "full": "https://cdn.shopk.it/assets/store/img/no-img.jpg"
                },
                "images": [],
                "categories": [
                    {
                        "id": 44373,
                        "parent": 0,
                        "active": true,
                        "title": "API",
                        "description": "",
                        "handle": "api",
                        "url": "https://parallax.shopk.it/category/api",
                        "image": {
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/c61c5bd-c61c5bd-c61c5bd-sylwia-pietruszka-218363-unsplash.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/c61c5bd-c61c5bd-c61c5bd-sylwia-pietruszka-218363-unsplash.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/c61c5bd-c61c5bd-c61c5bd-sylwia-pietruszka-218363-unsplash.jpg"
                        }
                    }
                ],
                "options": [],
                "option_groups": [],
                "stock": {
                    "stock_enabled": false
                },
                "rating": {
                    "total_reviews": 0,
                    "average_rating": 0,
                    "max_rating": 0,
                    "min_rating": 0
                }
            }

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## DELETE product [/product/{id}]

### DELETE product [DELETE]
Delete a product.

```bash
curl -X DELETE 'https://api.shopk.it/v1/product/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (required, integer, `1337`) ... Product identifier

+ Response 204 (application/json)

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## GET product search [/product/search{?query,fields,page,limit}]

### GET product search [GET]
Get a list of products from a search query and filtering fields.

```bash
curl -X GET 'https://api.shopk.it/v1/product/search/?query=Rustic&fields=title' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + query (required, string, `Rustic`) ... search query
    + fields (optional, string, `title,description`) ... product fields to search, comma separated
        + Values
            + `title`
            + `description`
            + `handle`
            + `brand`
            + `options`
            + `categories`
            + `tags`
            + `reference`
            + `barcode`

    + page (optional, integer, `1`) ... page number
    + limit = `25` (optional, integer, `10`) ... products per page

+ Response 200 (application/json)

    + Body

            {
                "id": 212322,
                "title": "Rustic Spice Bowl Set",
                "reference": "",
                "barcode": null,
                "price": 40.73,
                "price_formatted": "40,73 €",
                "price_promo": null,
                "price_promo_formatted": null,
                "promo_show_percentage": false,
                "price_promo_percentage": null,
                "price_on_request": false,
                "created_at": "2020-11-27T15:36:57+00:00",
                "status": 1,
                "status_alias": "active",
                "position": 0,
                "shipping": 0,
                "shipping_alone": false,
                "featured": false,
                "new": true,
                "is_promotion": false,
                "description": "<p>This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay. After shaping and drying, I bisque fired them and then glazed them in contrasting shades of white and dark turquoise. Pieces then went back into the kiln and were high fired, giving them strength and durability. These bowls are ideal for spices, dukkah, oil, chopped chilli or garlic.&nbsp;<br /><br />In many of my ceramic pieces you will find slight imperfections and marks left by the handmade process. These contribute to the uniqueness and beauty of the forms and are simply part of the character of the individual piece.<br /><br />Larger size (x2) - 8cm (3\") across, 5cm (2\") deep<br />Mid size - 7cm (2.5\") across, 5cm (2\") deep<br />Small size - 5cm (2\") across, 4cm (1.5\") deep<br /><br />Please Note : These items are MADE TO ORDER and may vary slightly from the image shown. Current make time is 2-3 weeks.&nbsp;<br /><br />*food, oven and dishwasher safe<br />*not suitable for microwave</p>",
                "excerpt": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy",
                "video_url": "",
                "file": null,
                "tax": 0,
                "taxable": false,
                "reduced_rate": null,
                "meta_description": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay. After shaping and drying, I bisque fir",
                "meta_tags": "",
                "handle": "rustic-spice-bowl-set",
                "page_title": "Rustic Spice Bowl Set",
                "weight": 0,
                "hits": 0,
                "sales": 0,
                "variants_same_values": false,
                "updated_at": "2020-11-27T15:36:57+00:00",
                "description_short": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy",
                "promo": false,
                "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set",
                "add_cart_url": "https://parallax.shopk.it/cart/add/rustic-spice-bowl-set",
                "wishlist": {
                    "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set",
                    "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set"
                },
                "permalink": "https://parallax.shopk.it/product/rustic-spice-bowl-set",
                "video_embed_url": false,
                "image": {
                    "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                    "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                    "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                },
                "images": [
                    {
                        "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/f519f86-17d23f7b534bf365580989363da328d2.jpg",
                        "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/f519f86-17d23f7b534bf365580989363da328d2.jpg",
                        "full": "https://cdn.shopk.it/usercontent/parallax/media/images/f519f86-17d23f7b534bf365580989363da328d2.jpg"
                    },
                    {
                        "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/0bb2c71-7d2fe8d66dd9925ac72a3112d691f352.jpg",
                        "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/0bb2c71-7d2fe8d66dd9925ac72a3112d691f352.jpg",
                        "full": "https://cdn.shopk.it/usercontent/parallax/media/images/0bb2c71-7d2fe8d66dd9925ac72a3112d691f352.jpg"
                    },
                    {
                        "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/717897d-ff2216454ebbf8ca2727335ecacbc472.jpg",
                        "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/717897d-ff2216454ebbf8ca2727335ecacbc472.jpg",
                        "full": "https://cdn.shopk.it/usercontent/parallax/media/images/717897d-ff2216454ebbf8ca2727335ecacbc472.jpg"
                    }
                ],
                "categories": [
                    {
                        "id": 44355,
                        "parent": 0,
                        "active": true,
                        "title": "Cozinha",
                        "description": "",
                        "handle": "cozinha",
                        "url": "https://parallax.shopk.it/category/cozinha",
                        "image": []
                    }
                ],
                "brand": null,
                "tags": [],
                "options": [
                    {
                        "id": 363364,
                        "id_variant_1": 206585,
                        "id_variant_2": 206587,
                        "id_variant_3": null,
                        "title": "Small bowl / White",
                        "price": 40.73,
                        "price_formatted": "40,73 €",
                        "price_promo": null,
                        "price_promo_formatted": null,
                        "promo": false,
                        "price_promo_percentage": null,
                        "price_on_request": false,
                        "stock": 88,
                        "shipping": 0,
                        "weight": 0,
                        "reference": "",
                        "barcode": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363364",
                        "image": {
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363364",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363364"
                        }
                    },
                    {
                        "id": 363365,
                        "id_variant_1": 206585,
                        "id_variant_2": 206588,
                        "id_variant_3": null,
                        "title": "Small bowl / Dark turquoise",
                        "price": 40.73,
                        "price_formatted": "40,73 €",
                        "price_promo": null,
                        "price_promo_formatted": null,
                        "promo": false,
                        "price_promo_percentage": null,
                        "price_on_request": false,
                        "stock": 94,
                        "shipping": 0,
                        "weight": 0,
                        "reference": "",
                        "barcode": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363365",
                        "image": {
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363365",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363365"
                        }
                    },
                    {
                        "id": 363366,
                        "id_variant_1": 206586,
                        "id_variant_2": 206587,
                        "id_variant_3": null,
                        "title": "Big bowl / White",
                        "price": 45.73,
                        "price_formatted": "45,73 €",
                        "price_promo": null,
                        "price_promo_formatted": null,
                        "promo": false,
                        "price_promo_percentage": null,
                        "price_on_request": false,
                        "stock": 100,
                        "shipping": 0,
                        "weight": 0,
                        "reference": "",
                        "barcode": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363366",
                        "image": {
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363366",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363366"
                        }
                    },
                    {
                        "id": 363367,
                        "id_variant_1": 206586,
                        "id_variant_2": 206588,
                        "id_variant_3": null,
                        "title": "Big bowl / Dark turquoise",
                        "price": 45.73,
                        "price_formatted": "45,73 €",
                        "price_promo": null,
                        "price_promo_formatted": null,
                        "promo": false,
                        "price_promo_percentage": null,
                        "price_on_request": false,
                        "stock": 100,
                        "shipping": 0,
                        "weight": 0,
                        "reference": "",
                        "barcode": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363367",
                        "image": {
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363367",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363367"
                        }
                    }
                ],
                "option_groups": [
                    {
                        "id": 62775,
                        "title": "Size",
                        "options": [
                            {
                                "id": 206585,
                                "title": "Small bowl"
                            },
                            {
                                "id": 206586,
                                "title": "Big bowl"
                            }
                        ]
                    },
                    {
                        "id": 62776,
                        "title": "Color",
                        "options": [
                            {
                                "id": 206587,
                                "title": "White"
                            },
                            {
                                "id": 206588,
                                "title": "Dark turquoise"
                            }
                        ]
                    }
                ],
                "stock": {
                    "stock_enabled": true,
                    "stock_qty": 88,
                    "stock_backorder": true,
                    "stock_show": true,
                    "stock_sold_single": true,
                    "stock_notify": 10
                },
                "rating": {
                    "total_reviews": 0,
                    "average_rating": 0,
                    "max_rating": 0,
                    "min_rating": 0
                },
                "custom_fields": null,
                "tabs": null
            }

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


# Group Product Option Groups

## GET product option group [/product/{id}/option_group/{id_option_group}]

### GET product option group [GET]
Get a list of a product option groups or a single product option group by id.

```bash
curl -X GET 'https://api.shopk.it/v1/product/212322/option_group' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'

curl -X GET 'https://api.shopk.it/v1/product/212322/option_group/62775' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (required, integer) ... Product identifier
    + id_option_group (optional, integer) ... Product option group identifier

+ Response 200 (application/json)

    + Body

            [
                {
                    "id": 62775,
                    "title": "Size",
                    "options": [
                        {
                            "id": 206585,
                            "title": "Small bowl"
                        },
                        {
                            "id": 206586,
                            "title": "Big bowl"
                        }
                    ]
                },
                {
                    "id": 62776,
                    "title": "Color",
                    "options": [
                        {
                            "id": 206587,
                            "title": "White"
                        },
                        {
                            "id": 206588,
                            "title": "Dark turquoise"
                        }
                    ]
                }
            ]

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## POST product option group [/product/{id}/option_group]

### POST product option group [POST]
Create a product option group.

```bash
curl -X POST 'https://api.shopk.it/v1/product/212322/option_group' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c' \
-H 'Content-Type: application/json' \
-d '{"title": "Color", "options": ["White", "Dark turquoise"]}'
```

<div class="well">

Attributes | Type | Description
---------- | ---- | -----------
**title**<br>(required) | string | Product option group title
**options**<br>(required) | array[string] | Array with product option group values

</div>

+ Parameters

    + id (required, integer) ... Product identifier

+ Request (application/json)

        {
            "title": "Color",
            "options": [
                "White",
                "Dark turquoise"
            ]
        }

+ Response 201 (application/json)

    + Body

            [
                {
                    "id": 62775,
                    "title": "Size",
                    "options": [
                        {
                            "id": 206585,
                            "title": "Small bowl"
                        },
                        {
                            "id": 206586,
                            "title": "Big bowl"
                        }
                    ]
                },
                {
                    "id": 62776,
                    "title": "Color",
                    "options": [
                        {
                            "id": 206587,
                            "title": "White"
                        },
                        {
                            "id": 206588,
                            "title": "Dark turquoise"
                        }
                    ]
                }
            ]

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## PUT product option group [/product/{id}/option_group/{id_option_group}]

### PUT product option group [PUT]
Update a product option group.

```bash
curl -X PUT 'https://api.shopk.it/v1/product/212322/option_group/62779' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c' \
-H 'Content-Type: application/json' \
-d '{"title": "Color", "options": ["White", "Dark turquoise"]}'
```

<div class="well">

Attributes | Type | Description
---------- | ---- | -----------
**title**<br>(required) | string | Product option group title
**options**<br>(required) | array[string] | Array with product option group values

</div>

+ Parameters

    + id (required, integer) ... Product identifier
    + id_option_group (required, integer) ... Product option group identifier

+ Request (application/json)

        {
            "title": "Color",
            "options": [
                "White",
                "Dark turquoise"
            ]
        }

+ Response 200 (application/json)

    + Body

            [
                {
                    "id": 62775,
                    "title": "Size",
                    "options": [
                        {
                            "id": 206585,
                            "title": "Small bowl"
                        },
                        {
                            "id": 206586,
                            "title": "Big bowl"
                        }
                    ]
                },
                {
                    "id": 62776,
                    "title": "Color",
                    "options": [
                        {
                            "id": 206587,
                            "title": "White"
                        },
                        {
                            "id": 206588,
                            "title": "Dark turquoise"
                        }
                    ]
                }
            ]

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


## DELETE product option group [/product/{id}/option_group/{id_option_group}]

### DELETE product option group [DELETE]
Delete a product option group.

```bash
curl -X DELETE 'https://api.shopk.it/v1/product/212322/option_group/62779' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (required, integer) ... Product identifier
    + id_option_group (required, integer) ... Product option group identifier

+ Response 204 (application/json)

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


# Group Product Options

## GET Product Option [/product/{id}/option/{id_option}]

### GET Product Option [GET]
Get a list of a product options or a single product option by id.

```bash
curl -X GET 'https://api.shopk.it/v1/product/212322/option' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'

curl -X GET 'https://api.shopk.it/v1/product/212322/option/363364' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (required, integer) ... Product identifier
    + id_option (optional, integer) ... Product option identifier

+ Response 200 (application/json)

    + Body

            [
                {
                    "id": 363364,
                    "id_variant_1": 206585,
                    "id_variant_2": 206587,
                    "id_variant_3": null,
                    "title": "Small bowl / White",
                    "price": 40.73,
                    "price_formatted": "40,73 €",
                    "price_promo": null,
                    "price_promo_formatted": null,
                    "promo": false,
                    "price_promo_percentage": null,
                    "price_on_request": false,
                    "stock": 88,
                    "shipping": 0,
                    "weight": 0,
                    "reference": "",
                    "barcode": "",
                    "active": true,
                    "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363364",
                    "image": {
                        "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                        "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                        "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                    },
                    "wishlist": {
                        "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363364",
                        "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363364"
                    }
                },
                {
                    "id": 363365,
                    "id_variant_1": 206585,
                    "id_variant_2": 206588,
                    "id_variant_3": null,
                    "title": "Small bowl / Dark turquoise",
                    "price": 40.73,
                    "price_formatted": "40,73 €",
                    "price_promo": null,
                    "price_promo_formatted": null,
                    "promo": false,
                    "price_promo_percentage": null,
                    "price_on_request": false,
                    "stock": 94,
                    "shipping": 0,
                    "weight": 0,
                    "reference": "",
                    "barcode": "",
                    "active": true,
                    "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363365",
                    "image": {
                        "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                        "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                        "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                    },
                    "wishlist": {
                        "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363365",
                        "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363365"
                    }
                },
                {
                    "id": 363366,
                    "id_variant_1": 206586,
                    "id_variant_2": 206587,
                    "id_variant_3": null,
                    "title": "Big bowl / White",
                    "price": 45.73,
                    "price_formatted": "45,73 €",
                    "price_promo": null,
                    "price_promo_formatted": null,
                    "promo": false,
                    "price_promo_percentage": null,
                    "price_on_request": false,
                    "stock": 100,
                    "shipping": 0,
                    "weight": 0,
                    "reference": "",
                    "barcode": "",
                    "active": true,
                    "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363366",
                    "image": {
                        "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                        "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                        "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                    },
                    "wishlist": {
                        "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363366",
                        "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363366"
                    }
                },
                {
                    "id": 363367,
                    "id_variant_1": 206586,
                    "id_variant_2": 206588,
                    "id_variant_3": null,
                    "title": "Big bowl / Dark turquoise",
                    "price": 45.73,
                    "price_formatted": "45,73 €",
                    "price_promo": null,
                    "price_promo_formatted": null,
                    "promo": false,
                    "price_promo_percentage": null,
                    "price_on_request": false,
                    "stock": 100,
                    "shipping": 0,
                    "weight": 0,
                    "reference": "",
                    "barcode": "",
                    "active": true,
                    "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363367",
                    "image": {
                        "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                        "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                        "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                    },
                    "wishlist": {
                        "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363367",
                        "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363367"
                    }
                }
            ]

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## PUT Product Option [/product/{id}/option/{id_option}]

### PUT Product Option [PUT]
Update a product option.

```bash
curl -X PUT 'https://api.shopk.it/v1/product/212322/option/363364' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c' \
-H 'Content-Type: application/json' \
-d '{"reference": "SWB-001"}'
```

<div class="well">

Attributes | Type | Choices | Description
---------- | ---- | ------- | -----------
**price** | float | Price
**price_promo** | float | | Promotion price (must be lower than price)
**price_on_request** | boolean | `true` `false` | Price is on request
**stock** | integer | | Units in stock (requires product stock enabled)
**shipping** | float | | Shipping cost
**weight** | integer | | Weight (in grams)
**reference** | string | | SKU
**barcode** | string | | EAN, ISBN, UPC, GTIN, etc.
**image** | string | | Option image url
**active** | boolean | `true` `false` | Option is active

</div>

+ Parameters

    + id (required, integer) ... Product identifier
    + id_option (optional, integer) ... Product option identifier

+ Request (application/json)

        {
            "reference": "SWB-001"
        }

+ Response 200 (application/json)

    + Body

            {
                "id": 363364,
                "id_variant_1": 206585,
                "id_variant_2": 206587,
                "id_variant_3": null,
                "title": "Small bowl / White",
                "price": 40.73,
                "price_formatted": "40,73 €",
                "price_promo": null,
                "price_promo_formatted": null,
                "promo": false,
                "price_promo_percentage": null,
                "price_on_request": false,
                "stock": 88,
                "shipping": 0,
                "weight": 0,
                "reference": "SWB-001",
                "barcode": "SWB-001",
                "active": true,
                "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=363364",
                "image": {
                    "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                    "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg",
                    "full": "https://cdn.shopk.it/usercontent/parallax/media/images/da84db6-472c46da6a786edb5b67cf338c2b9c58.jpg"
                },
                "wishlist": {
                    "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=363364",
                    "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=363364"
                }
            }

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


## DELETE Product Option [/product/{id}/option/{id_option}]

### DELETE Product Option [DELETE]
Delete a product option.

```bash
curl -X DELETE 'https://api.shopk.it/v1/product/212322/option/363364' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (required, integer) ... Product identifier
    + id_option (required, integer) ... Product option identifier

+ Response 204 (application/json)

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


# Group Categories

## GET Category [/category/{id,handle,active,is_parent,page,limit}]

### GET Category [GET]
Get products categories by id or handle. **Only one parameter is required.**

```bash
curl -X GET 'https://api.shopk.it/v1/category/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (optional, integer, `1337`) ... Category identifier
    + handle (optional, string, `rustic-bowl`) ... Category handle
    + active (optional, boolean) ... Category is active
        + Values
            + `true`
            + `false`
    + is_parent (optional, boolean) ... Category parent only
        + Values
            + `true`
            + `false`
    + page (optional, integer, `1`) ... Page number
    + limit = `25` (optional, integer, `10`) ... Categories per page

+ Response 200 (application/json)

    + Body

            {
                "id": 14535,
                "title": "Decoração",
                "is_parent": true,
                "is_child": false,
                "parent": 0,
                "parent_title": null,
                "description": "Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.",
                "position": 7,
                "active": true,
                "handle": "decoracao",
                "page_title": "Decoração",
                "meta_description": "Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Morbi posuere sodales tellus, sit amet tincidunt mi al",
                "meta_tags": null,
                "num_products": 0,
                "url": "https://parallax.shopk.it/category/decoracao",
                "permalink": "https://parallax.shopk.it/category/decoracao",
                "image": {
                    "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/4778681bb73229d7d038c077c741b7bd.jpg",
                    "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/4778681bb73229d7d038c077c741b7bd.jpg",
                    "full": "https://cdn.shopk.it/usercontent/parallax/media/images/4778681bb73229d7d038c077c741b7bd.jpg"
                },
                "parents": null,
                "children": [
                    {
                        "id": 167757,
                        "title": "Sala",
                        "is_parent": false,
                        "is_child": true,
                        "parent": 14535,
                        "description": "Morbi posuere sodales tellus, sit amet tincidunt mi aliquam porta.",
                        "position": 0,
                        "active": true,
                        "handle": "decoracao-sala",
                        "page_title": "Sala",
                        "meta_description": null,
                        "meta_tags": null,
                        "num_products": 9,
                        "url": "https://parallax.shopk.it/category/decoracao-sala",
                        "permalink": "https://parallax.shopk.it/category/decoracao-sala",
                        "image": {
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/276f8c112c887d830a8e3c585da5d93d.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/276f8c112c887d830a8e3c585da5d93d.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/276f8c112c887d830a8e3c585da5d93d.jpg"
                        },
                        "children": null
                    },
                ],
                "created_at": "2019-10-02T17:03:56+01:00",
                "updated_at": "2019-10-02T17:11:08+01:00"
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## POST Category [/category]

### POST Category [POST]
Create a category.

```bash
curl -X POST 'https://api.shopk.it/v1/category/' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c' \
-H 'Content-Type: application/json' \
-d '{"title": "Rustic Spice Bowl Set", "price": 17.45, "categories": [44373]}'
```

<div class="well">

Attributes | Type | Choices | Description
---------- | ---- | ------- | -----------
**title**<br>(required) | string | | Title
**active** | boolean | `true` `false` | Category is active
**parent_id** | integer | | Category parent identifier
**description** | string | | Description
**handle** | string | | Handle
**image** | string | | Image url
**position** | integer | | Position
**meta_description** | string | | Meta description
**meta_tags** | string | | Meta tags
**page_title** | string | | Page title

</div>

+ Request (application/json)

        {
          "title": "Prints"
        }

+ Response 201 (application/json)

    + Body

            {
                "id": 14534,
                "title": "Prints",
                "is_parent": false,
                "is_child": false,
                "parent": 0,
                "parent_title": null,
                "description": "",
                "position": 0,
                "active": true,
                "handle": "prints",
                "page_title": "Prints",
                "meta_description": "",
                "meta_tags": null,
                "num_products": 0,
                "url": "https://parallax.shopk.it/category/prints",
                "permalink": "https://parallax.shopk.it/category/prints",
                "image": {
                    "thumb": "https://cdn.shopk.it/assets/store/img/no-img.png",
                    "square": "https://cdn.shopk.it/assets/store/img/no-img.png",
                    "full": "https://cdn.shopk.it/assets/store/img/no-img.png"
                },
                "parents": null,
                "children": null,
                "created_at": "2019-10-02T17:11:07+01:00",
                "updated_at": "2019-10-02T17:11:08+01:00"
            }

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## PUT Category [/category/{id}]

### PUT Category [PUT]
Update a category.

```bash
curl -X PUT 'https://api.shopk.it/v1/category/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c' \
-H 'Content-Type: application/json' \
-d'{"reference": "SWB-001", "featured": true}'
```

<div class="well">

Attributes | Type | Choices | Description
---------- | ---- | ------- | -----------
**title**<br>(required) | string | | Title
**active** | boolean | `true` `false` | Category is active
**parent_id** | integer | | Category parent identifier
**description** | string | | Description
**handle** | string | | Handle
**image** | string | | Image url
**position** | integer | | Position
**meta_description** | string | | Meta description
**meta_tags** | string | | Meta tags
**page_title** | string | | Page title

</div>

+ Parameters

    + id (required, integer) ... Category identifier

+ Request (application/json)

        {
            "description": "Mauris ut ex iaculis, rhoncus nisl sit amet, posuere nisl."
        }

+ Response 200 (application/json)

    + Body

            {
                "id": 14534,
                "title": "Prints",
                "is_parent": false,
                "is_child": false,
                "parent": 0,
                "parent_title": null,
                "description": "Mauris ut ex iaculis, rhoncus nisl sit amet, posuere nisl.",
                "position": 0,
                "active": true,
                "handle": "prints",
                "page_title": "Prints",
                "meta_description": "",
                "meta_tags": null,
                "num_products": 0,
                "url": "https://parallax.shopk.it/category/prints",
                "permalink": "https://parallax.shopk.it/category/prints",
                "image": {
                    "thumb": "https://cdn.shopk.it/assets/store/img/no-img.png",
                    "square": "https://cdn.shopk.it/assets/store/img/no-img.png",
                    "full": "https://cdn.shopk.it/assets/store/img/no-img.png"
                },
                "parents": null,
                "children": null,
                "created_at": "2019-10-02T17:11:07+01:00",
                "updated_at": "2019-10-02T17:11:09+01:00"
            }


+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## DELETE Category [/category/{id}]

### DELETE Category [DELETE]
Delete a category.

```bash
curl -X DELETE 'https://api.shopk.it/v1/category/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (required, integer, `1337`) ... Category identifier

+ Response 204 (application/json)

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


# Group Orders

## GET Orders [/order{?id,status,status_alias,paid,date_filter,date_from,date_to,date_type,page,limit,coupon_code}]

### GET Order [GET]
Get a list of orders or single order by id.

```bash
curl -X GET 'https://api.shopk.it/v1/order/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'

curl -X GET 'https://api.shopk.it/v1/order?status=3&date_filter=last_month' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (optional, integer, `1337`) ... Order identifier
    + status (optional, integer, `0`) ... Order status as an integer
        + Values
            + `0`
            + `1`
            + `2`
            + `3`
            + `4`
            + `5`
            + `6`
            + `7`
            + `8`
            + `9`
            + `10`
            + `11`
    + status_alias (optional, string, `all`) ... Order status as a string
        + Values
            + `all`
            + `pending`
            + `processing`
            + `sent`
            + `canceled`
            + `waiting_confirmation`
            + `waiting_payment`
            + `waiting_stock`
            + `delivered`
            + `returned`
            + `pickup_available`
            + `waiting_shipment`
    + paid (optional, boolean, `true`) ... Order paid field
        + Values
            + `true`
            + `false`
    + date_filter (optional, string, `yesterday`) ... Date filter
        + Values
            + `today`
            + `yesterday`
            + `last_week`
            + `last_month`
    + date_from (optional, string, `2015-01-01`) ... Date format yyyy-mm-dd
    + date_to (optional, string, `2015-01-01`) ... Date format yyyy-mm-dd
    + date_type (optional, string) ... Affects all date parameters
        + Values
            + `created_at`
            + `update_at`
            + `sent_at`
            + `paid_at`
    + page (optional, integer, `1`) ... Page number
    + limit = `25` (optional, integer, `10`) ... Orders per page
    + coupon_code (optional, integer, `1337`) ... Coupon code

+ Response 200 (application/json)

    + Body

            {
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
                    "tax_percent": null,
                    "discount": 0,
                    "discount_percent": 0
                },
                "created_at": "2017-05-17T10:45:05+01:00",
                "update_at": "2017-12-06T17:18:41+00:00",
                "sent_at": "2017-05-17T11:23:21+01:00",
                "paid_at": "2017-05-17T11:23:21+01:00",
                "currency": "EUR",
                "payment": {
                    "type": "multibanco",
                    "data": {
                        "entity": 88888,
                        "reference": 888888888,
                        "value": 157.03
                    },
                    "description": "Multibanco"
                },
                "status": 3,
                "status_alias": "sent",
                "status_description": "Sent",
                "paid": true,
                "is_new": false,
                "invoice_url": "https://www.invoiceservice.com/invoice_permalink/",
                "weight": 0,
                "observations": null,
                "note": null,
                "client_note": null,
                "custom_field": null,
                "tracking_code": null,
                "tracking_url": "",
                "shipping_url": null,
                "coupon": {
                    "code": "bajevolp",
                    "type": "percent",
                    "value": 10
                },
                "shipment_method": "Transportadora",
                "permalink": "https://parallax.shopk.it/order/a77e38d0b16ba62f32361331774324904278edcf",
                "client": {
                    "name": "Shopkit",
                    "email": "info@shopk.it",
                    "fiscal_id": null,
                    "company": "Shopkit",
                    "is_registered": false,
                    "delivery": {
                        "name": "Shopkit",
                        "phone": "969057993",
                        "address": "Centro de Empresas Inovadoras\\nAvª do Empresário",
                        "address_extra": "1, S1.08",
                        "country": "Portugal - Continental",
                        "country_code": "PRT",
                        "zip_code": "6000-767",
                        "city": "Castelo Branco"
                    },
                    "billing": {
                        "name": "Shopkit",
                        "phone": "969057993",
                        "address": "Centro de Empresas Inovadoras\\nAvª do Empresário",
                        "address_extra": "1, S1.08",
                        "country": "Portugal - Continental",
                        "country_code": "PRT",
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
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/4778681bb73229d7d038c077c741b7bd.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/4778681bb73229d7d038c077c741b7bd.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/4778681bb73229d7d038c077c741b7bd.jpg"
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
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/eacc633fe509af083776db911a5f02b9.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/eacc633fe509af083776db911a5f02b9.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/eacc633fe509af083776db911a5f02b9.jpg"
                        }
                    }
                ]
            }

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## PUT Order [/order/{id}]

### PUT Order [PUT]
Update an order.

```bash
curl -X PUT 'https://api.shopk.it/v1/order/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c' \
-H 'Content-Type:application/json' \
-d '{"paid":true, "status_alias":"sent"}'
```

<div class="well">

Attributes | Type | Choices | Description
---------- | ---- | ------- | -----------
**status** | integer | `1` `2` `3` `4` `5` `6` `7` `8` `9` `10` `11` | Order status as an integer
**status_alias** | string | `pending` `processing` `sent` `canceled` `waiting_confirmation` `waiting_payment` `waiting_stock` `delivered` `returned` `pickup_available` `waiting_shipment` | Order status as a string
**paid** | boolean | `true` `false` | Order paid field
**invoice_url** | string | | Invoice permalink
**tracking_url** | string | | Tracking URL
**tracking_code** | string | | Tracking code
**shipping_url** | string | | Shipping URL
**pickup_code** | string | | Pickup code
**note** | string | | Order note
**client_note** | string | | Order note from client

</div>

+ Parameters

    + id (optional, integer, `1337`) ... Order identifier

+ Request (application/json)

    + Body

            {
                "paid": true,
                "status_alias": "sent"
            }

+ Response 200 (application/json)

    + Body

            {
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
                    "tax_percent": null,
                    "discount": 0,
                    "discount_percent": 0
                },
                "created_at": "2017-05-17T10:45:05+01:00",
                "update_at": "2017-12-06T17:18:41+00:00",
                "sent_at": "2017-05-17T11:23:21+01:00",
                "paid_at": "2017-05-17T11:23:21+01:00",
                "currency": "EUR",
                "payment": {
                    "type": "multibanco",
                    "data": {
                        "entity": 88888,
                        "reference": 888888888,
                        "value": 157.03
                    },
                    "description": "Multibanco"
                },
                "status": 3,
                "status_alias": "sent",
                "status_description": "Sent",
                "paid": true,
                "is_new": false,
                "invoice_url": "https://www.invoiceservice.com/invoice_permalink/",
                "weight": 0,
                "observations": null,
                "note": null,
                "client_note": null,
                "custom_field": null,
                "tracking_code": null,
                "tracking_url": "",
                "shipping_url": null,
                "coupon": {
                    "code": "bajevolp",
                    "type": "percent",
                    "value": 10
                },
                "shipment_method": "Transportadora",
                "permalink": "https://parallax.shopk.it/order/a77e38d0b16ba62f32361331774324904278edcf",
                "client": {
                    "name": "Shopkit",
                    "email": "info@shopk.it",
                    "fiscal_id": null,
                    "company": "Shopkit",
                    "is_registered": false,
                    "delivery": {
                        "name": "Shopkit",
                        "phone": "969057993",
                        "address": "Centro de Empresas Inovadoras\\nAvª do Empresário",
                        "address_extra": "1, S1.08",
                        "country": "Portugal - Continental",
                        "country_code": "PRT",
                        "zip_code": "6000-767",
                        "city": "Castelo Branco"
                    },
                    "billing": {
                        "name": "Shopkit",
                        "phone": "969057993",
                        "address": "Centro de Empresas Inovadoras\\nAvª do Empresário",
                        "address_extra": "1, S1.08",
                        "country": "Portugal - Continental",
                        "country_code": "PRT",
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
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/4778681bb73229d7d038c077c741b7bd.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/4778681bb73229d7d038c077c741b7bd.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/4778681bb73229d7d038c077c741b7bd.jpg"
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
                            "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/eacc633fe509af083776db911a5f02b9.jpg",
                            "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/eacc633fe509af083776db911a5f02b9.jpg",
                            "full": "https://cdn.shopk.it/usercontent/parallax/media/images/eacc633fe509af083776db911a5f02b9.jpg"
                        }
                    }
                ]
            }

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## DELETE Order [/order/{id}/]

### DELETE Order [DELETE]
Delete an order.

```bash
curl -X DELETE 'https://api.shopk.it/v1/order/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (required, integer, `1337`) ... Order identifier

+ Response 204 (application/json)

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


# Group Shipping

## GET Shipping [/shipping{?country_code,weight,value}]

### GET Shipping [GET]
Get a list of shipping methods available for a country.

```bash
curl -X GET 'https://api.shopk.it/v1/shipping?country_code=prt' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + country_code (required, string, `prt`) ... three-letter country codes (ISO 3166-1 Alfa-3)
    + weight (optional, integer, `100`) ... Order weight
    + value (optional, integer, `10`) ... Orders value

+ Response 200 (application/json)

    + Body

            [
                {
                    "title": "CTT",
                    "description": "Via CTT Expresso. Entrega em 24 horas.",
                    "price": 6.76,
                    "price_formatted": "6,76 €"
                },
                {
                    "title": "Transportadora",
                    "description": "Envio via Nacex no próprio dia",
                    "price": 7.25,
                    "price_formatted": "7,25 €"
                }
            ]

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


# Group Coupons

## GET Coupon [/coupon{?id,code}]

### GET Coupon [GET]
Get a coupon by id or code. **Only one parameter is required.**

```bash
curl -X GET 'https://api.shopk.it/v1/coupon/bajevolp' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (optional, integer, `1337`) ... Coupon identifier
    + code (optional, string, `bajevolp`) ... Coupon code

+ Response 200 (application/json)

    + Body

            [
                {
                    "id": 1337,
                    "code": "bajevolp",
                    "limit": 5,
                    "used": 2,
                    "value": 10,
                    "type": "percent",
                    "applies_to": "all_orders",
                    "orders_over": null,
                    "category": null,
                    "product": null,
                    "date_from": null,
                    "date_to": null,
                    "created_at": "2014-11-18T23:41:32+00:00",
                    "orders_total": 157.03,
                    "orders_discount": 14.864
                }
            ]

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


## POST Coupon [/coupon/]

### POST Coupon [POST]
Create a coupon.

```bash
curl -X POST 'https://api.shopk.it/v1/coupon' \
-H "X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c" \
-H 'Content-Type:application/json' \
-d '{"code":"bajevolp", "limit":"5", "value":"10", "type":"percent", "applies_to":"all_orders"}'
```

<div class="well">

Attributes | Type | Choices | Description
---------- | ---- | ------- | -----------
**code** (required) | string | | Coupon code
**limit** (required) | int | | Coupon usage limit. Set `0` for unlimited
**value** (required) | float | | Coupon discount value
**type** (required) | string | `money` `percent` `shipping` | Coupon allowed types
**applies_to** (required) | string |  `all_orders` `orders_over` `category` `product` | Coupon applies to...
**orders_over** | float | | Order minimum value to apply discount.<br>**Required** when `applies_to` is `orders_over`
**category** | mixed | | Category to apply discount.<br>**Required** when `applies_to` is `category`, valid category `id` or `handle`
**product** | mixed | | Product to apply discount.<br>**Required** when `applies_to` is `product`, valid product `id` or `handle`
**date_from** | string | | Coupon start date. Date format yyyy-mm-dd
**date_to** | string | | Coupon expire date. Date format yyyy-mm-dd

</div>

+ Response 201 (application/json)

    + Body

            [
                {
                    "id": 1337,
                    "code": "bajevolp",
                    "limit": 5,
                    "used": 2,
                    "value": 10,
                    "type": "percent",
                    "applies_to": "all_orders",
                    "orders_over": null,
                    "category": null,
                    "product": null,
                    "date_from": null,
                    "date_to": null,
                    "created_at": "2014-11-18T23:41:32+00:00",
                    "orders_total": 157.03,
                    "orders_discount": 14.864
                }
            ]

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 409 (application/json)

    + Body

            {
                "message": "Already exists."
            }

+ Response 409


## DELETE Coupon [/coupon/{id}]

### DELETE Coupon [DELETE]
Delete a coupon.

```bash
curl -X DELETE 'https://api.shopk.it/v1/coupon/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (required, integer, `1337`) ... Coupon identifier

+ Response 204 (application/json)

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


# Group Webhooks
Webhooks allow you to build or set up integrations which subscribe to certain events on Shopkit stores. For more information visit [webhooks documentation](https://shopk.it/developers/webhooks).<br><br>Available webhook events: `order_canceled` `order_deleted` `order_created` `order_updated` `order_paid` `order_sent` `order_change_status` `order_invoice` `order_shipping` `order_delivered` `order_change_payment` `order_payment_failed` `order_returned` `order_pickup_available` `order_waiting_shipment` `client_created` `client_updated` `client_deleted` `newsletter_subscribed` `newsletter_unsubscribed`<br>

## GET Webhook [/webhook/{id}{?active,event}]

### GET Webhook [GET]
Get a list of webhooks or single webhook by id.

```bash
curl -X GET 'https://api.shopk.it/v1/webhook/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (optional, integer, `1337`) ... Webhook identifier
    + active (optional, boolean, `true`) ... Webhook active status
        + Values
            + `true`
            + `false`
    + event (optional, string, `order_created`) ... Webhook event, see list above

+ Response 200 (application/json)

    + Body

            {
                "id": 1337,
                "event": "order_created",
                "url": "https://www.example.com/url",
                "active": true
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## POST Webhook [/webhook/]

### POST Webhook [POST]
Create a webhook.

```bash
curl -X POST 'https://api.shopk.it/v1/webhook' \
-H "X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c" \
-H 'Content-Type:application/json' \
-d '{"url":"https://www.example.com/url", "event":"order_created"}'
```

<div class="well">

Attributes | Type | Description
---------- | ---- | -----------
**url** | string | Webhook url
**event** | string | Webhook event, see list above

</div>

+ Response 201 (application/json)

    + Body

            {
                "id": 1337,
                "event": "order_created",
                "url": "https://www.example.com/url",
                "active": true
            }

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 409 (application/json)

    + Body

            {
                "message": "Already exists."
            }


## DELETE Webhook [/webhook/{id}]

### DELETE Webhook [DELETE]
Delete a webhook.

```bash
curl -X DELETE 'https://api.shopk.it/v1/webhook/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (required, integer, `1337`) ... Webhook identifier

+ Response 204 (application/json)

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }


# Group Media

## GET Media [/media/{?id,checksum,type,q,page,limit}]

### GET Media [GET]
Get a list of media files or single media file by id or hash.

```bash
curl -X GET 'https://api.shopk.it/v1/media/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (optional, integer, `1337`) ... Media identifier
    + checksum (optional, string, `6afb72c3074212b171f472a1ade4c0f5`) ... Media md5 checksum
    + type (optional, string, `all`)) ... Media type
        + Values
            + `all`
            + `image`
            + `file`
    
    + q (optional, string, `bowl`) ... Search for media
    + page (optional, integer, `1`) ... Page number
    + limit = `25` (optional, integer, `25`) ... Media per page

+ Response 200 (application/json)

    + Body

            {
                "id": 725,
                "checksum": "3df623e086a7d6cd606c4b1043bd7150",
                "file_name": "3df623e-010547-4778681bb73229d7d038c077c741b7bd.jpg",
                "file_type": "image/jpeg",
                "file_ext": ".jpg",
                "file_size": 60.82,
                "image_width": 600,
                "image_height": 674,
                "created_at": "2021-05-07 01:05:51",
                "url": {
                    "thumb": "https://cdn.shopk.it/usercontent/parallax/media/images/thumb/3df623e-010547-4778681bb73229d7d038c077c741b7bd.jpg",
                    "square": "https://cdn.shopk.it/usercontent/parallax/media/images/square/3df623e-010547-4778681bb73229d7d038c077c741b7bd.jpg",
                    "full": "https://cdn.shopk.it/usercontent/parallax/media/images/3df623e-010547-4778681bb73229d7d038c077c741b7bd.jpg"
                }
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }

## POST Media [/media/]

### POST Media [POST]
Upload a file to media, via url or base64 encoded.<br><br>Files are processed asynchronous, there is no body response.

```bash
curl -X POST 'https://api.shopk.it/v1/media/images' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c' \
-H 'Content-Type: application/json' \
-d '{"url": "https://cdn.shopk.it/usercontent/parallax/media/images/3df623e-010547-4778681bb73229d7d038c077c741b7bd.jpg"}'

```

<div class="well">

Attributes | Type | Description
---------- | ---- | -----------
**url** | string | Media url
**file** | string | Media base64 encoded

</div>

+ Response 201 (application/json)

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

## Delete Media [/media/{id,checksum}]

### Delete Media [DELETE]
Delete a media file by id or hash. **Only one parameter is required.**

```bash
curl -X DELETE 'https://api.shopk.it/v1/media/1337' \
-H 'X-API-KEY: f4c3cfc9af72e01c60d8b5f0b47492b2ee467c0c'
```

+ Parameters

    + id (optional, integer, `1337`) ... Media identifier
    + checksum (optional, string, `6afb72c3074212b171f472a1ade4c0f5`) ... Media md5 checksum

+ Response 204 (application/json)

+ Response 400 (application/json)

    + Body

            {
                "message": "Bad request."
            }

+ Response 404 (application/json)

    + Body

            {
                "message":"Not found."
            }
