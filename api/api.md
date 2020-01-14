FORMAT: 1A
HOST: https://api.shopk.it/v1

# Shopkit API
Welcome to the **Shopkit** REST API documentation.

For now there are only a few available methods. We will add more over time.

If you have a suggestion, find a bug or something worth fixing, create an issue or a pull request on the **[Github repo](https://github.com/Shopkit/docs)**.

<small class="last-modified">Last Modified 2020-01-14T11:30:58+00:00</small>

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
https://api.shopk.it/v1/?X-API-KEY=0bb18b34ba33cb2d7c55d568353fdc6f345b8d78
```

2. In the HTTP Authorization header:

```http
X-API-KEY: 0bb18b34ba33cb2d7c55d568353fdc6f345b8d78
```

### Endpoints
All API requests are made to https://api.shopk.it/ and all requests are served over **HTTPS**. The current version is **v1**.

### Schema
The API only supports JSON. <small class="text-light">(2005 called and wants its XML back)</small>

All timestamps are returned in ISO 8601 format: `YYYY-MM-DDTHH:MM:SS±HH:MM`

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
curl -i -X PUT \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
-H 'Content-Type:application/json' \
-d '{"paid":true, "status_alias":"sent"}' \
https://api.shopk.it/v1/order/1337
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
```


### Resources

# Group Store

## Get Store [/]

### Get Store [GET]
Get Store info. **No parameters**

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/
```

+ Response 200

    + Headers

            Content-Length: 5997
            Content-Type: application/json

    + Body

            {
                "username": "parallax",
                "name": "Parallax",
                "logo": null,
                "description": "A Shopkit é um serviço que te permite criar a tua loja on-line de forma fácil, prática e adequada ao teu tipo de negócio. O processo é simples e rápido. Em 5 minutos estás pronto para começar a vender os teus produtos on-line.",
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
                "custom_css": null,
                "custom_js": null,
                "footer_info": "Os produtos listados são apenas de apresentação e não se encontram á venda.",
                "page_title": "Parallax",
                "meta_description": "A Shopkit é um serviço que te permite criar a tua loja on-line de forma fácil, prática e adequada ao teu tipo de negócio. O processo é simpl",
                "meta_tags": null,
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
                            "menu_url": "https://parallax.shopk.it/sobre-nos",
                            "menu_item": "sobre-nos",
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
                            "menu_url": "https://parallax.shopk.it/promocoes",
                            "menu_item": "promocoes",
                            "target_blank": false
                        },
                        {
                            "menu_text": "Novidades",
                            "menu_type": "menu_page",
                            "menu_url": "https://parallax.shopk.it/novidades",
                            "menu_item": "novidades",
                            "target_blank": false
                        },
                        {
                            "menu_text": "Contactos",
                            "menu_type": "menu_page",
                            "menu_url": "https://parallax.shopk.it/contatos",
                            "menu_item": "contatos",
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
                        "image": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/credit_card-pt.png",
                        "logo": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/credit-card-brands.png"
                    },
                    "multibanco": {
                        "active": true,
                        "message": "EInstruções método de pagamento Multibanco.",
                        "description": "O método de pagamento mais utilizado pelos portugueses para pagamentos online.",
                        "default": true,
                        "gateway": "stripe",
                        "method": "multibanco",
                        "alias": "multibanco",
                        "title": "Multibanco",
                        "image": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/multibanco-pt.png",
                        "logo": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/multibanco-color.png"
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
                        "image": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/mbway-pt.png",
                        "logo": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/mbway-color.png"
                    },
                    "paypal": {
                        "active": true,
                        "email": "info@shopk.it",
                        "message": "Instruções método de pagamento Paypal.",
                        "description": "Pague de forma rápida e segura usando a sua conta Paypal.",
                        "default": false,
                        "gateway": "paypal",
                        "method": "paypal",
                        "alias": "paypal",
                        "title": "Paypal",
                        "image": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/paypal-pt.png",
                        "logo": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/paypal-color.png"
                    },
                    "bank_transfer": {
                        "active": true,
                        "message": "Instruções método de pagamento Transferência Bancária.",
                        "description": "Pague por transferência bancária ou interbancária.",
                        "default": true,
                        "gateway": "manual",
                        "method": "bank_transfer",
                        "alias": "bank_transfer",
                        "title": "Transferência Bancária",
                        "image": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/bank_transfer-pt.png"
                    },
                    "on_delivery": {
                        "active": true,
                        "value": 0,
                        "message": "Instruções método de pagamento À Cobrança",
                        "description": "Pagamento contra reembolso. Acresce aos portes de envio.",
                        "default": false,
                        "gateway": "manual",
                        "method": "on_delivery",
                        "alias": "on_delivery",
                        "title": "À Cobrança",
                        "image": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/on_delivery-pt.png"
                    },
                    "pick_up": {
                        "active": true,
                        "message": "Instruções método de pagamento Levantamento nas instalações",
                        "description": "Levante a sua encomenda nas nossas instalações. Não paga portes de envio.",
                        "default": false,
                        "gateway": "manual",
                        "method": "pick_up",
                        "alias": "pick_up",
                        "title": "Levantamento nas instalações",
                        "image": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/common/icons/payments/pick_up-pt.png"
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
                "category_default_order": null,
                "categories_sorting": null,
                "domain": "parallax.shopk.it",
                "is_ssl": true,
                "assets": {
                    "url": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/shopkit/parallax",
                    "images": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/shopkit/parallax/img",
                    "css": "https://drwfxyu78e9uq.cloudfront.net/css/store/parallax/style.css?template=shopkit/parallax&amp;last_modified=1504786507",
                    "plugins": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/shopkit/parallax/js/plugins.js?template=shopkit/parallax&amp;last_modified=1504786507",
                    "scripts": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/shopkit/parallax/js/script.js?template=shopkit/parallax&amp;last_modified=1504786507"
                },
                "images_header": [
                    "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/14bb24a112fafccdd36680be2b03f4ce.jpg",
                    "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/c788681a62eff02c640765d3c215c920.jpg",
                    "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/f669d550743b2e27a81c22812b270101.jpg"
                ],
                "taxes_included": true
            }


# Group Products

## Get Product [/product{?id,handle,category,status,status_alias,reference,featured,new,q,page,limit}]

### Get Product [GET]
Get a list of products or single product by id or handle

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/product/1337

curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/product/?category=1337&limit=5
```

+ Parameters

    + id (optional, integer, `1337`) ... Product identifier
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
    + featured (optional, string, `true`) ... Product featured field
        + Values
            + `true`
            + `false`

    + new (optional, string, `true`) ... Product new field
        + Values
            + `true`
            + `false`
    + q (optional, string, `bowl`) ... Search for products
    + page (optional, integer, `1`) ... page number
    + limit = `25` (optional, integer, `10`) ... products per page

+ Response 200

    + Headers

            Content-Length: 8578
            Content-Type: application/json

    + Body

            {
                "id": 1337,
                "title": "Rustic Spice Bowl Set",
                "reference": "",
                "price": 40.73,
                "price_formatted": "40,73 €",
                "price_promo": null,
                "price_promo_formatted": null,
                "promo_show_percentage": false,
                "price_promo_percentage": null,
                "price_on_request": false,
                "created_at": "2014-11-30T01:04:40+00:00",
                "status": 1,
                "status_alias": "active",
                "position": 0,
                "shipping": 0,
                "shipping_alone": false,
                "featured": false,
                "new": true,
                "is_promotion": false,
                "description": "<p>This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay. After shaping and drying, I bisque fired them and then glazed them in contrasting shades of white and dark turquoise. Pieces then went back into the kiln and were high fired, giving them strength and durability. These bowls are ideal for spices, dukkah, oil, chopped chilli or garlic.&nbsp;<br /><br />In many of my ceramic pieces you will find slight imperfections and marks left by the handmade process. These contribute to the uniqueness and beauty of the forms and are simply part of the character of the individual piece.<br /><br />Larger size (x2) - 8cm (3\") across, 5cm (2\") deep<br />Mid size - 7cm (2.5\") across, 5cm (2\") deep<br />Small size - 5cm (2\") across, 4cm (1.5\") deep<br /><br />Please Note : These items are MADE TO ORDER and may vary slightly from the image shown. Current make time is 2-3 weeks.&nbsp;<br /><br />*food, oven and dishwasher safe<br />*not suitable for microwave</p>",
                "video_url": "",
                "file": null,
                "tax": 0,
                "meta_description": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay. After shaping and drying, I bisque fir",
                "meta_tags": "",
                "handle": "rustic-spice-bowl-set",
                "page_title": "Rustic Spice Bowl Set",
                "weight": 0,
                "hits": 849,
                "sales": 0,
                "variants_same_values": false,
                "description_short": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy&#8230;",
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
                    "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/472c46da6a786edb5b67cf338c2b9c58.jpg",
                    "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/472c46da6a786edb5b67cf338c2b9c58.jpg",
                    "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/472c46da6a786edb5b67cf338c2b9c58.jpg"
                },
                "images": [
                    {
                        "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/17d23f7b534bf365580989363da328d2.jpg",
                        "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/17d23f7b534bf365580989363da328d2.jpg",
                        "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/17d23f7b534bf365580989363da328d2.jpg"
                    },
                    {
                        "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/7d2fe8d66dd9925ac72a3112d691f352.jpg",
                        "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/7d2fe8d66dd9925ac72a3112d691f352.jpg",
                        "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/7d2fe8d66dd9925ac72a3112d691f352.jpg"
                    },
                    {
                        "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/ff2216454ebbf8ca2727335ecacbc472.jpg",
                        "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/ff2216454ebbf8ca2727335ecacbc472.jpg",
                        "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/ff2216454ebbf8ca2727335ecacbc472.jpg"
                    }
                ],
                "options": [
                    {
                        "id": 192867,
                        "id_variant_1": 45896,
                        "id_variant_2": 90261,
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
                        "reference": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=192867",
                        "image": {
                            "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=192867",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=192867"
                        }
                    },
                    {
                        "id": 192868,
                        "id_variant_1": 45896,
                        "id_variant_2": 90262,
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
                        "reference": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=192868",
                        "image": {
                            "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=192868",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=192868"
                        }
                    },
                    {
                        "id": 192869,
                        "id_variant_1": 45897,
                        "id_variant_2": 90261,
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
                        "reference": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=192869",
                        "image": {
                            "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=192869",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=192869"
                        }
                    },
                    {
                        "id": 192870,
                        "id_variant_1": 45897,
                        "id_variant_2": 90262,
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
                        "reference": null,
                        "active": true,
                        "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set?option=192870",
                        "image": {
                            "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/472c46da6a786edb5b67cf338c2b9c58.jpg"
                        },
                        "wishlist": {
                            "add_url": "https://parallax.shopk.it/wishlist/add/rustic-spice-bowl-set?option=192870",
                            "remove_url": "https://parallax.shopk.it/wishlist/remove/rustic-spice-bowl-set?option=192870"
                        }
                    }
                ],
                "categories": [
                    {
                        "id": 15942,
                        "parent": 0,
                        "title": "Cozinha",
                        "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque lacus neque, dapibus eu volutpat a, consectetur elementum purus. Nam quis eros eu nunc mollis venenatis.",
                        "handle": "cozinha",
                        "url": "https://parallax.shopk.it/category/cozinha",
                        "image": {
                            "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/472c46da6a786edb5b67cf338c2b9c58.jpg",
                            "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/472c46da6a786edb5b67cf338c2b9c58.jpg"
                        }
                    }
                ],
                "option_groups": [
                    {
                        "title": "Size",
                        "options": [
                            {
                                "id": 45896,
                                "title": "Small bowl"
                            },
                            {
                                "id": 45897,
                                "title": "Big bowl"
                            }
                        ]
                    },
                    {
                        "title": "Color",
                        "options": [
                            {
                                "id": 90261,
                                "title": "White"
                            },
                            {
                                "id": 90262,
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
                }
            }

+ Response 400

    + Headers

            Content-Length: 26
            Content-Type: application/json

    + Body

            {
                "message": "Bad request."
            }

+ Response 404

    + Headers

            Content-Length: 24
            Content-Type: application/json

    + Body

            {
                "message":"Not found."
            }


# Group Categories

## Get Category [/category/{id,handle}]

### Get Category [GET]
Get products categories by id or handle. **Only one parameter is required.**

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/category/1337
```

+ Parameters

    + id (optional, integer, `1337`) ... Category identifier
    + handle (optional, string, `rustic-bowl`) ... Category handle

+ Response 200

    + Headers

            Content-Length: 543
            Content-Type: application/json

    + Body

            {
                "id": 14535,
                "title": "Decoração",
                "is_parent": true,
                "is_child": false,
                "parent": 0,
                "parent_title": null,
                "description": "Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Morbi posuere sodales tellus, sit amet tincidunt mi aliquam porta.",
                "position": 0,
                "active": true,
                "handle": "decoracao",
                "page_title": "Decoração",
                "meta_description": "Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Morbi posuere sodales tellus, sit amet tincidunt mi al",
                "meta_tags": null,
                "num_products": 0,
                "url": "https://parallax.shopk.it/category/decoracao",
                "permalink": "https://parallax.shopk.it/category/decoracao",
                "image": {
                    "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/4778681bb73229d7d038c077c741b7bd.jpg",
                    "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/4778681bb73229d7d038c077c741b7bd.jpg",
                    "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/4778681bb73229d7d038c077c741b7bd.jpg"
                },
                "parents": null,
                "children": [
                    {
                        "id": 105283,
                        "title": "Sala",
                        "is_parent": true,
                        "is_child": true,
                        "parent": 14535,
                        "description": "",
                        "position": 0,
                        "active": true,
                        "handle": "decoracao-sala",
                        "page_title": "Sala",
                        "meta_description": "",
                        "meta_tags": null,
                        "num_products": 4,
                        "url": "https://parallax.shopk.it/category/decoracao-sala",
                        "permalink": "https://parallax.shopk.it/category/decoracao-sala",
                        "image": {
                            "thumb": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/thumb/276f8c112c887d830a8e3c585da5d93d.jpg",
                            "square": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/square/276f8c112c887d830a8e3c585da5d93d.jpg",
                            "full": "https://drwfxyu78e9uq.cloudfront.net/usercontent/parallax/media/images/276f8c112c887d830a8e3c585da5d93d.jpg"
                        },
                        "children": null
                    }
                ]
            }

+ Response 404

    + Headers

            Content-Length: 24
            Content-Type: application/json

    + Body

            {
                "message":"Not found."
            }


# Group Orders

## Get Orders [/order{?id,status,status_alias,paid,date_filter,date_from,date_to,datetype,page,limit,coupon_code}]

### Get Order [GET]
Get a list of orders or single order by id

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/order/1337

curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/order?status=3&date_filter=last_month
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
    + paid (optional, string, `true`) ... Order paid field
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
    + datetype = `created_at` (optional, string, `created_at`) ... Affects all date parameters
        + Values
            + `created_at`
            + `update_at`
            + `sent_at`
            + `paid_at`
    + page (optional, integer, `1`) ... Page number
    + limit = `25` (optional, integer, `10`) ... Orders per page
    + coupon_code (optional, integer, `1337`) ... Coupon code

+ Response 200

    + Headers

            Content-Length: 3224
            Content-Type: application/json

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

+ Response 400

    + Headers

            Content-Length: 26
            Content-Type: application/json

    + Body

            {
                "message": "Bad request."
            }

+ Response 404

    + Headers

            Content-Length: 24
            Content-Type: application/json

    + Body

            {
                "message":"Not found."
            }

## Put Order [/order/{id}]

### Put Order [PUT]
Update an order

```bash
curl -i -X PUT \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
-H 'Content-Type:application/json' \
-d '{"paid":true, "status_alias":"sent"}' \
https://api.shopk.it/v1/order/1337
```

<div class="well">

Attributes | Type | Choices | Description
---------- | ---- | ------- | -----------
**status** | integer | `1` `2` `3` `4` `5` `6` `7` `8` `9` `10` | Order status as an integer
**status_alias** | string | `pending` `processing` `sent` `canceled` `waiting_confirmation` `waiting_payment` `waiting_stock` `delivered` `returned` `pickup_available` | Order status as a string
**paid** | string | `true` `false` | Order paid field
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

+ Request

    + Headers

            Content-Type: application/json

    + Body

            {
                "paid": true,
                "status_alias": "sent"
            }

+ Response 200

    + Headers

            Content-Length: 3224
            Content-Type: application/json

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

+ Response 400

    + Headers

            Content-Length: 26
            Content-Type: application/json

    + Body

            {
                "message": "Bad request."
            }

+ Response 404

    + Headers

            Content-Length: 24
            Content-Type: application/json

    + Body

            {
                "message":"Not found."
            }

## Delete Order [/order/{id}/]

### Delete Order [DELETE]
Delete an order

```bash
curl -i -X DELETE \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/order/1337
```

+ Parameters

    + id (required, integer, `1337`) ... Order identifier

+ Response 204

+ Response 400

    + Headers

            Content-Length: 26
            Content-Type: application/json

    + Body

            {
                "message": "Bad request."
            }

+ Response 404

    + Headers

            Content-Length: 24
            Content-Type: application/json

    + Body

            {
                "message":"Not found."
            }

# Group Shipping

## Get Shipping [/shipping{?country_code,weight,value}]

### Get Shipping [GET]
Get a list of shipping methods available for a country

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/shipping?country_code=prt
```

+ Parameters

    + country_code (required, string, `prt`) ... three-letter country codes (ISO 3166-1 Alfa-3)
    + weight (optional, integer, `100`) ... Order weight
    + value (optional, integer, `10`) ... Orders value

+ Response 200

   + Headers

            Content-Length: 234
            Content-Type: application/json

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

+ Response 400

    + Headers

            Content-Length: 26
            Content-Type: application/json

    + Body

            {
                "message": "Bad request."
            }

+ Response 404

    + Headers

            Content-Length: 24
            Content-Type: application/json

    + Body

            {
                "message":"Not found."
            }


# Group Coupon

## Get Coupon [/coupon{?id,code}]

### Get Coupon [GET]
Get a coupon by id or code. **Only one parameter is required.**

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/coupon/bajevolp
```

+ Parameters

    + id (optional, integer, `1337`) ... Coupon identifier
    + code (optional, string, `bajevolp`) ... Coupon code

+ Response 200

   + Headers

            Content-Length: 289
            Content-Type: application/json

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

+ Response 404

    + Headers

            Content-Length: 24
            Content-Type: application/json

    + Body

            {
                "message":"Not found."
            }


## Post Coupon [/coupon/]

### Post Coupon [POST]
Create a coupon

```bash
curl -i -X POST \
-H "X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78" \
-H 'Content-Type:application/json' \
-d '{"code":"bajevolp", "limit":"5", "value":"10", "type":"percent", "applies_to":"all_orders"}' \
'https://api.shopk.it/v1/coupon'
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

+ Response 201

    + Headers

            Content-Length: 289
            Content-Type: application/json

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

+ Response 400

    + Headers

            Content-Length: 26
            Content-Type: application/json

    + Body

            {
                "message": "Bad request."
            }

+ Response 409


## Delete Coupon [/coupon/{id}]

### Delete Coupon [DELETE]
Delete a coupon

```bash
curl -i -X DELETE \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/coupon/1337
```

+ Parameters

    + id (required, integer, `1337`) ... Coupon identifier

+ Response 204

+ Response 400

    + Headers

            Content-Length: 26
            Content-Type: application/json

    + Body

            {
                "message": "Bad request."
            }

+ Response 404

    + Headers

            Content-Length: 24
            Content-Type: application/json

    + Body

            {
                "message":"Not found."
            }


# Group Webhooks
Webhooks allow you to build or set up integrations which subscribe to certain events on Shopkit stores. For more information visit [webhooks documentation](https://shopk.it/developers/webhooks).

## Post Webhook [/webhook/]

### Post Webhook [POST]
Create a webhook

```bash
curl -i -X POST \
-H "X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78" \
-H 'Content-Type:application/json' \
-d '{"url":"https://www.mysite.com/mywebhook_url", "event":"order_created"}' \
'https://api.shopk.it/v1/webhook'
```

<div class="well">

Attributes | Type | Choices | Description
---------- | ---- | ------- | -----------
**url** | string | | Webhook url
**event** | string |`order_canceled` `order_deleted` `order_created` `order_updated` `order_paid` `order_sent` `order_change_status` `order_invoice` `order_delivered` | Available webhooks

</div>


+ Response 201

    + Headers

            Content-Length: 98
            Content-Type: application/json

    + Body

            {
                "id": 1337,
                "event": "order_created",
                "url": "https://www.mysite.com/mywebhook_url",
                "active": true
            }

+ Response 400

    + Headers

            Content-Length: 26
            Content-Type: application/json

    + Body

            {
                "message": "Bad request."
            }

+ Response 409


## Delete Webhook [/webhook/{id}]

### Delete Webhook [DELETE]
Delete a webhook

```bash
curl -i -X DELETE \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/webhook/1337
```

+ Parameters

    + id (required, integer, `1337`) ... Webhook identifier

+ Response 204

+ Response 400

    + Headers

            Content-Length: 26
            Content-Type: application/json

    + Body

            {
                "message": "Bad request."
            }

+ Response 404

    + Headers

            Content-Length: 24
            Content-Type: application/json

    + Body

            {
                "message":"Not found."
            }
