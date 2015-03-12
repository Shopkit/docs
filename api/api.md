FORMAT: 1A
HOST: https://api.shopk.it/v1

# Shopkit API
Welcome to the **Shopkit** REST API documentation.

For now there are only a few available methods. We will add more over time.

If you find a bug or something worth fixing, create an issue or a pull request on the **[Github repo](https://github.com/Shopkit/API-Docs)**.

### API Status

<div class="api-status" style="display:none;">
    <h6>-</h6>
    <div class="metrics">Response time: <strong><span class="response_time">-</span>ms</strong></div>
</div>

### Authentication
You must first create a new API key from your store administration area:

1. Login into your store.
2. Navigate to the API section under the Account settings menu tab.
3. Create a new API key

**Do not share your API keys with other users or store them in insecure places.**

All requests to the API must be authenticated with an API key in one of two ways:

1. In the URL as the `X-KEY-API` parameter:

```http
https://api.shopk.it/v1/?X-KEY-API=0bb18b34ba33cb2d7c55d568353fdc6f345b8d78
```

2. In the HTTP Authorization header:

```http
X-KEY-API: 0bb18b34ba33cb2d7c55d568353fdc6f345b8d78
```

### Endpoints
All API requests are made to https://api.shopk.it/ and all requests are served over **HTTPS**. The current version is **v1**.

### Schema
The API only supports JSON. <small class="text-light">(2005 called and wants its XML back)</small>

All timestamps are returned in ISO 8601 format: `YYYY-MM-DDTHH:MM:SS±HH:MM`

### HTTP Verbs
Where possible, the API strives to use appropriate HTTP verbs for each action.

<div class="well">

Verb  | Description
------------- | -------------
`GET`  | Used for retrieving resources.
`POST`  | Used for creating resources.
`PUT`  | Used for updating resources, or performing custom actions.
`DELETE`  | Used for deleting resources.

</div>

### Rate Limiting
You can make up to **3600** requests per hour.

### Pagination
Requests that return multiple items will be paginated to **25** items by default.

You can specify further pages with the `page` parameter. For some resources, you can also set a custom page size up to **100** with the `limit` parameter.

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
    "total": 158.81,
    "total_tax": 17.78,
    "shipping": 7.25,
    "discount": 14.86,
    "cupon_code": "bajevolp",
    "created_at": "2014-11-19T00:44:19+00:00",
    "sent_at": "2014-11-25T15:00:20+00:00",
    "paid_at": "2014-11-25T25:00:20+00:00",
    "payment": {
        "type": "multibanco",
        "data": {
            "entity": 88888,
            "reference": 888888888,
            "value": 158.81
        }
    },
    "status": 3,
    "status_alias": "sent",
    "paid": true,
    "is_new": false,
    "invoice_id": null,
    "weight": 0,
    "observations": "",
    "shipment_method": "Transportadora",
    "client": {
        "name": "Shopkit",
        "email": "info@shopk.it",
        "address": "Centro de Empresas Inovadoras\nAvª do Empresário, 1, S1.08\n",
        "postcode": "6000-767 ",
        "town": "Castelo Branco",
        "country": "Portugal - Continental",
        "phone": "969057993",
        "fiscal_id": ""
    },
    "products": [
        {
            "id": 44752,
            "title": "Hanging Succulent Planter",
            "reference": "",
            "price": 71.32,
            "tax": 0,
            "quantity": 1,
            "subtotal": 71.32,
            "weight": 0,
            "url": false,
            "description_short": "<p>This stoneware planter/pot has been hand made by me from earthy textured, speckled clay using the traditional methods of pinching and coiling. It has been decorated with a white glaze and high fired giving it strength and durability. Perfect for succulents and cactus plants, it has a drain hole in the base. The hanger twine is made from natural jute fibre.<br /><br />In many of my ceramic pieces you will find slight imperfections and marks left by the handmade process. These contribute to the uniqueness and beauty of the forms and are simply part of the character of the individual piece. As they are completely hand built, each piece is totally unique and may vary slightly from the image shown.&nbsp;<br /><br />This pot is approx 6cm (2.2\") tall and is 10cm (4\") across at the opening.</p>"
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

            Content-Length: 961
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
                "instagram": null,
                "pinterest": null,
                "facebook_comments_product": true,
                "facebook_comments_blog": true,
                "facebook_likebox": true,
                "show_email": false,
                "email": "info@shopk.it",
                "phone": null,
                "cellphone": "(+351) 969 057 993",
                "address": "Avª do Empresário, 1, S1.08\n6000-767 Castelo Branco",
                "facebook_username": null,
                "paypal_email": "info@shopk.it",
                "basecolor": "#db0a5b",
                "favicon": null,
                "google_analytics": "UA-88888888-8",
                "latitude": "39.818466068593935",
                "longitude": "-7.491968556808545",
                "translate_languages": null,
                "translate_meta": null,
                "currency": "EUR",
                "custom_css": null,
                "custom_js": null,
                "footer_info": "Os produtos listados são apenas de apresentação e não se encontram á venda.",
                "page_title": "Parallax",
                "meta_description": "A Shopkit é um serviço que te permite criar a tua loja on-line de forma fácil, prática e adequada ao teu tipo de negócio. O processo é simples e rápido. Em 5 minutos estás pronto para começar a vender os teus produtos on-line.",
                "meta_tags": null,
                "assets": {
                    "url": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/store/parallax",
                    "images": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/store/parallax/img",
                    "css": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/store/parallax/css/style.css?template=store/parallax&amp;last_modified=1419706838",
                    "plugins": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/store/parallax/js/plugins.js?template=store/parallax&amp;last_modified=1419706838",
                    "scripts": "https://drwfxyu78e9uq.cloudfront.net/templates/assets/store/parallax/js/script.js?template=store/parallax&amp;last_modified=1419706838"
                },
                "images_header": [
                    "https://d38oac8e57zmkl.cloudfront.net/header/ef1a329cffb7ddcd33cc860863d60522.jpg",
                    "https://d38oac8e57zmkl.cloudfront.net/header/fd7516a5fc9c490a624c9d2ce152da2b.jpg",
                    "https://d38oac8e57zmkl.cloudfront.net/header/a68f777e6912cd917c0797fc47776f29.jpg"
                ],
                "taxes_included": false
            }


# Group Products

## Get Product [/product/{id|handle}]

### Get Product [GET]
Get a product by id or handle. **Only one parameter is required.**

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/product/1337
```

+ Parameters

    + id (required, integer, `1337`) ... Product identifier
    + handle (required, string, `rustic-bowl`) ... Product handle

+ Response 200

    + Headers

            Content-Length: 1435
            Content-Type: application/json

    + Body

            {
                "id": 1337,
                "title": "Rustic Spice Bowl Set",
                "reference": "",
                "price": 40.73,
                "price_promo": 0,
                "created_at": "2014-11-30T01:04:40+00:00",
                "status": 1,
                "status_alias": "active",
                "position": 0,
                "shipping": 0,
                "featured": false,
                "new": true,
                "description": "<p>This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay. After shaping and drying, I bisque fired them and then glazed them in contrasting shades of white and dark turquoise. Pieces then went back into the kiln and were high fired, giving them strength and durability. These bowls are ideal for spices, dukkah, oil, chopped chilli or garlic.&nbsp;<br /><br />In many of my ceramic pieces you will find slight imperfections and marks left by the handmade process. These contribute to the uniqueness and beauty of the forms and are simply part of the character of the individual piece.<br /><br />Larger size (x2) - 8cm (3\") across, 5cm (2\") deep<br />Mid size - 7cm (2.5\") across, 5cm (2\") deep<br />Small size - 5cm (2\") across, 4cm (1.5\") deep<br /><br />Please Note : These items are MADE TO ORDER and may vary slightly from the image shown. Current make time is 2-3 weeks.&nbsp;<br /><br />*food, oven and dishwasher safe<br />*not suitable for microwave</p>",
                "video_url": "",
                "file": null,
                "tax": 0,
                "meta_description": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay. After shaping and drying, I bisque fired them and then glazed them in contrasting shades of white and dark turquoise. Pieces then went back into the kiln",
                "meta_tags": "",
                "handle": "rustic-spice-bowl-set",
                "page_title": "Rustic Spice Bowl Set",
                "weight": 0,
                "hits": 104,
                "description_short": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy&#8230;",
                "promo": false,
                "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set",
                "add_cart_url": "https://parallax.shopk.it/cart/add/rustic-spice-bowl-set",
                "permalink": "https://parallax.shopk.it/product/rustic-spice-bowl-set",
                "video_embed_url": false,
                "sales": 0,
                "images": {
                    "1": {
                        "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/17d23f7b534bf365580989363da328d2.jpg",
                        "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/17d23f7b534bf365580989363da328d2.jpg",
                        "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/17d23f7b534bf365580989363da328d2.jpg"
                    },
                    "2": {
                        "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/7d2fe8d66dd9925ac72a3112d691f352.jpg",
                        "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/7d2fe8d66dd9925ac72a3112d691f352.jpg",
                        "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/7d2fe8d66dd9925ac72a3112d691f352.jpg"
                    },
                    "3": {
                        "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/ff2216454ebbf8ca2727335ecacbc472.jpg",
                        "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/ff2216454ebbf8ca2727335ecacbc472.jpg",
                        "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/ff2216454ebbf8ca2727335ecacbc472.jpg"
                    }
                },
                "image": {
                    "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/472c46da6a786edb5b67cf338c2b9c58.jpg",
                    "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/472c46da6a786edb5b67cf338c2b9c58.jpg",
                    "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/472c46da6a786edb5b67cf338c2b9c58.jpg"
                },
                "options": [
                    {
                        "id": 96201,
                        "title": "Small bowl",
                        "price": 40.73,
                        "promo": false,
                        "price_promo": 0,
                        "stock": 100,
                        "shipping": 0,
                        "weight": 0
                    },
                    {
                        "id": 96202,
                        "title": "Big bowl",
                        "price": 45.73,
                        "promo": false,
                        "price_promo": 0,
                        "stock": 100,
                        "shipping": 0,
                        "weight": 0
                    }
                ],
                "categories": [
                    {
                        "id": 1337,
                        "parent": 0,
                        "title": "Cozinha",
                        "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque lacus neque, dapibus eu volutpat a, consectetur elementum purus. Nam quis eros eu nunc mollis venenatis.",
                        "url": "https://parallax.shopk.it/category/cozinha"
                    }
                ],
                "option_groups": [
                    {
                        "title": "Size",
                        "options": [
                            {
                                "id": 45896,
                                "title": "Small bowl",
                                "price": 40.73,
                                "promo": false,
                                "price_promo": 0,
                                "stock": 100,
                                "shipping": 0,
                                "weight": 0
                            },
                            {
                                "id": 45897,
                                "title": "Big bowl",
                                "price": 45.73,
                                "promo": false,
                                "price_promo": 0,
                                "stock": 100,
                                "shipping": 0,
                                "weight": 0
                            }
                        ]
                    }
                ],
                "stock": {
                    "stock_enabled": true,
                    "stock_qty": 100,
                    "stock_backorder": true,
                    "stock_show": true,
                    "stock_sold_single": true
                }
            }

+ Response 404

    + Headers

            Content-Length: 24
            Content-Type: application/json

    + Body

            {
                "message":"Not found."
            }


## Get Products [/product{?category,status,status_alias,reference,featured,new,page,limit}]

### Get Products [GET]
Get a list of products

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/product/?category=1337&limit=5
```

+ Parameters

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
    
    + page (optional, integer, `1`) ... page number
    + limit = `25` (optional, integer, `10`) ... products per page

+ Response 200

    + Headers

            Content-Length: 1915
            Content-Type: application/json

    + Body

            {
                "0": {
                    "id": 1337,
                    "title": "Rustic Spice Bowl Set",
                    "reference": "",
                    "price": 40.73,
                    "price_promo": 0,
                    "created_at": "2014-11-30T01:04:40+00:00",
                    "status": 1,
                    "status_alias": "active",
                    "position": 0,
                    "shipping": 0,
                    "featured": false,
                    "new": true,
                    "description": "<p>This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay. After shaping and drying, I bisque fired them and then glazed them in contrasting shades of white and dark turquoise. Pieces then went back into the kiln and were high fired, giving them strength and durability. These bowls are ideal for spices, dukkah, oil, chopped chilli or garlic.&nbsp;<br /><br />In many of my ceramic pieces you will find slight imperfections and marks left by the handmade process. These contribute to the uniqueness and beauty of the forms and are simply part of the character of the individual piece.<br /><br />Larger size (x2) - 8cm (3\") across, 5cm (2\") deep<br />Mid size - 7cm (2.5\") across, 5cm (2\") deep<br />Small size - 5cm (2\") across, 4cm (1.5\") deep<br /><br />Please Note : These items are MADE TO ORDER and may vary slightly from the image shown. Current make time is 2-3 weeks.&nbsp;<br /><br />*food, oven and dishwasher safe<br />*not suitable for microwave</p>",
                    "video_url": "",
                    "file": null,
                    "tax": 0,
                    "meta_description": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy stoneware clay. After shaping and drying, I bisque fired them and then glazed them in contrasting shades of white and dark turquoise. Pieces then went back into the kiln",
                    "meta_tags": "",
                    "handle": "rustic-spice-bowl-set",
                    "page_title": "Rustic Spice Bowl Set",
                    "weight": 0,
                    "hits": 104,
                    "description_short": "This set of four rustic, pinch pots have been hand formed by me from textured, earthy&#8230;",
                    "promo": false,
                    "url": "https://parallax.shopk.it/product/rustic-spice-bowl-set",
                    "add_cart_url": "https://parallax.shopk.it/cart/add/rustic-spice-bowl-set",
                    "permalink": "https://parallax.shopk.it/product/rustic-spice-bowl-set",
                    "video_embed_url": false,
                    "sales": 0,
                    "images": {
                        "1": {
                            "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/17d23f7b534bf365580989363da328d2.jpg",
                            "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/17d23f7b534bf365580989363da328d2.jpg",
                            "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/17d23f7b534bf365580989363da328d2.jpg"
                        },
                        "2": {
                            "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/7d2fe8d66dd9925ac72a3112d691f352.jpg",
                            "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/7d2fe8d66dd9925ac72a3112d691f352.jpg",
                            "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/7d2fe8d66dd9925ac72a3112d691f352.jpg"
                        },
                        "3": {
                            "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/ff2216454ebbf8ca2727335ecacbc472.jpg",
                            "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/ff2216454ebbf8ca2727335ecacbc472.jpg",
                            "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/ff2216454ebbf8ca2727335ecacbc472.jpg"
                        }
                    },
                    "image": {
                        "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/472c46da6a786edb5b67cf338c2b9c58.jpg",
                        "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/472c46da6a786edb5b67cf338c2b9c58.jpg",
                        "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/472c46da6a786edb5b67cf338c2b9c58.jpg"
                    },
                    "options": [
                        {
                            "id": 96201,
                            "title": "Small bowl",
                            "price": 40.73,
                            "promo": false,
                            "price_promo": 0,
                            "stock": 100,
                            "shipping": 0,
                            "weight": 0
                        },
                        {
                            "id": 96202,
                            "title": "Big bowl",
                            "price": 45.73,
                            "promo": false,
                            "price_promo": 0,
                            "stock": 100,
                            "shipping": 0,
                            "weight": 0
                        }
                    ],
                    "categories": [
                        {
                            "id": 1337,
                            "parent": 0,
                            "title": "Cozinha",
                            "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque lacus neque, dapibus eu volutpat a, consectetur elementum purus. Nam quis eros eu nunc mollis venenatis.",
                            "url": "https://parallax.shopk.it/category/cozinha"
                        }
                    ],
                    "option_groups": [
                        {
                            "title": "Size",
                            "options": [
                                {
                                    "id": 45896,
                                    "title": "Small bowl",
                                    "price": 40.73,
                                    "promo": false,
                                    "price_promo": 0,
                                    "stock": 100,
                                    "shipping": 0,
                                    "weight": 0
                                },
                                {
                                    "id": 45897,
                                    "title": "Big bowl",
                                    "price": 45.73,
                                    "promo": false,
                                    "price_promo": 0,
                                    "stock": 100,
                                    "shipping": 0,
                                    "weight": 0
                                }
                            ]
                        }
                    ],
                    "stock": {
                        "stock_enabled": true,
                        "stock_qty": 100,
                        "stock_backorder": true,
                        "stock_show": true,
                        "stock_sold_single": true
                    }
                },
                "0": {
                    "id": 1338,
                    "title": "Let's Cook cutting board",
                    "reference": "",
                    "price": 29.72,
                    "price_promo": 0,
                    "created_at": "2014-11-30T00:59:27+00:00",
                    "status": 1,
                    "status_alias": "active",
                    "position": 0,
                    "shipping": 0,
                    "featured": false,
                    "new": true,
                    "description": "<p>Heisenberg, Let's Cook, personalized engraved cutting board, breaking bad. Walter white cutting board.<br /><br />We make and ship these boards daily, so the turnaround time is really quick.<br /><br />In honor of the brilliance that is breaking bad, we decided to make a cutting board for all the loyal fans! This beautifully engraved cutting board is the perfect gift for any fan that wants to reminisce Heisenberg every time they cook a meal.&nbsp;<br /><br />Wood type: bamboo<br />Size: 14 x 11</p>",
                    "video_url": "",
                    "file": null,
                    "tax": 0,
                    "meta_description": "Heisenberg, Let's Cook, personalized engraved cutting board, breaking bad. Walter white cutting board.We make and ship these boards daily, so the turnaround time is really quick.In honor of the brilliance that is breaking bad, we decided to make a cutting",
                    "meta_tags": "",
                    "handle": "let-s-cook-cutting-board",
                    "page_title": "Let's Cook cutting board",
                    "weight": 0,
                    "hits": 93,
                    "description_short": "Heisenberg, Let's Cook, personalized engraved cutting board, breaking bad. Walter white&#8230;",
                    "promo": false,
                    "url": "https://parallax.shopk.it/product/let-s-cook-cutting-board",
                    "add_cart_url": "https://parallax.shopk.it/cart/add/let-s-cook-cutting-board",
                    "permalink": "https://parallax.shopk.it/product/let-s-cook-cutting-board",
                    "video_embed_url": false,
                    "sales": 0,
                    "images": {
                        "1": {
                            "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/697610aa34185dfefa326724ea867818.jpg",
                            "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/697610aa34185dfefa326724ea867818.jpg",
                            "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/697610aa34185dfefa326724ea867818.jpg"
                        },
                        "2": {
                            "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/5d6f7ac0314930ef1c756da68c60cbb3.jpg",
                            "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/5d6f7ac0314930ef1c756da68c60cbb3.jpg",
                            "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/5d6f7ac0314930ef1c756da68c60cbb3.jpg"
                        }
                    },
                    "image": {
                        "thumb": "https://d38oac8e57zmkl.cloudfront.net/produtos/th/1609f7f3d86847eba5a5cc184577deea.jpg",
                        "square": "https://d38oac8e57zmkl.cloudfront.net/produtos/square/1609f7f3d86847eba5a5cc184577deea.jpg",
                        "full": "https://d38oac8e57zmkl.cloudfront.net/produtos/1609f7f3d86847eba5a5cc184577deea.jpg"
                    },
                    "options": [
                    ],
                    "categories": [
                        {
                            "id": 1337,
                            "parent": 0,
                            "title": "Cozinha",
                            "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque lacus neque, dapibus eu volutpat a, consectetur elementum purus. Nam quis eros eu nunc mollis venenatis.",
                            "url": "https://parallax.shopk.it/category/cozinha"
                        }
                    ],
                    "option_groups": [
                    ],
                    "stock": {
                        "stock_enabled": false
                    }
                },
                "paging": null
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

## Get Category [/category/{id|handle}]

### Get Category [GET]
Get products categories by id or handle. **Only one parameter is required.**

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/category/1337
```

+ Parameters

    + id (required, integer, `1337`) ... Category identifier
    + handle (required, string, `rustic-bowl`) ... Category handle



+ Response 200

    + Headers

            Content-Length: 265
            Content-Type: application/json

    + Body

            {
                "id": 1337,
                "title": "Cozinha",
                "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque lacus neque, dapibus eu volutpat a, consectetur elementum purus. Nam quis eros eu nunc mollis venenatis.",
                "parent": 0,
                "handle": "cozinha",
                "page_title": "Cozinha",
                "meta_description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque lacus neque, dapibus eu volutpat a, consectetur elementum purus. Nam quis eros eu nunc mollis venenatis.",
                "meta_tags": "",
                "url": "https://parallax.shopk.it/category/cozinha",
                "total_products": 2
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

## Order [/order/{id}]

### Get Order [GET]
Get an order

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/order/1337
```

+ Parameters

    + id (optional, integer, `1337`) ... Order identifier

+ Response 200

    + Headers

            Content-Length: 1394
            Content-Type: application/json

    + Body

            {
                "id": 1337,
                "total": 158.81,
                "total_tax": 17.78,
                "shipping": 7.25,
                "discount": 14.86,
                "cupon_code": "bajevolp",
                "created_at": "2014-11-19T00:44:19+00:00",
                "sent_at": null,
                "paid_at": null,
                "payment": {
                    "type": "multibanco",
                    "data": {
                        "entity": 88888,
                        "reference": 888888888,
                        "value": 158.81
                    }
                },
                "status": 5,
                "status_alias": "waiting_confirmation",
                "paid": false,
                "is_new": false,
                "invoice_id": null,
                "weight": 0,
                "observations": "",
                "shipment_method": "Transportadora",
                "client": {
                    "name": "Shopkit",
                    "email": "info@shopk.it",
                    "address": "Centro de Empresas Inovadoras\nAvª do Empresário, 1, S1.08\n",
                    "postcode": "6000-767 ",
                    "town": "Castelo Branco",
                    "country": "Portugal - Continental",
                    "phone": "969057993",
                    "fiscal_id": ""
                },
                "products": [
                    {
                        "id": 44753,
                        "title": "Shelving Tree with Birds",
                        "reference": "STHFBF7574",
                        "price": 77.32,
                        "tax": 23,
                        "quantity": 1,
                        "subtotal": 95.1036,
                        "weight": 0,
                        "url": false,
                        "description_short": "<p>This is a tree decal that is created to work with standard 24\" wall shelves that you can find at your local Target, Walmart, Ikea etc.. (shelving NOT INCLUDED) There are three locations where you can fit the shelves. This tree looks great on its own as well!<br /><br /><br />Tree Size (approx): 55&rdquo;w x 94&rdquo;h<br /><br />51\"w x 88\"h version is available upon request (they fit the same 24\" shelves). The price is the same. Please leave a note in the \"message to seller\" box during checkout if you would like the 88\"h version.<br /><br />At what heights would the shelf locations be at?<br />Standard Size Tree - (approx)<br />43\", 53\", 64\"<br /><br />For the 88\" Tree - (approx)<br />40\", 50\", 60\"</p>"
                    },
                    {
                        "id": 44752,
                        "title": "Hanging Succulent Planter",
                        "reference": "",
                        "price": 71.32,
                        "tax": 0,
                        "quantity": 1,
                        "subtotal": 71.32,
                        "weight": 0,
                        "url": false,
                        "description_short": "<p>This stoneware planter/pot has been hand made by me from earthy textured, speckled clay using the traditional methods of pinching and coiling. It has been decorated with a white glaze and high fired giving it strength and durability. Perfect for succulents and cactus plants, it has a drain hole in the base. The hanger twine is made from natural jute fibre.<br /><br />In many of my ceramic pieces you will find slight imperfections and marks left by the handmade process. These contribute to the uniqueness and beauty of the forms and are simply part of the character of the individual piece. As they are completely hand built, each piece is totally unique and may vary slightly from the image shown.&nbsp;<br /><br />This pot is approx 6cm (2.2\") tall and is 10cm (4\") across at the opening.</p>"
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
**status** | integer | `1` `2` `3` `4` `5` `6` `7` | Order status as an integer
**status_alias** | string | `pending` `processing` `sent` `canceled` `waiting_confirmation` `waiting_payment` `waiting_stock` | Order status as a string
**paid** | string | `true` `false` | Order paid field
**invoice_id** | integer | | Invoice identifier

</div>

+ Parameters

    + id (optional, integer, `25`) ... Order identifier

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

            Content-Length: 1414
            Content-Type: application/json

    + Body

            {
                "id": 1337,
                "total": 158.81,
                "total_tax": 17.78,
                "shipping": 7.25,
                "discount": 14.86,
                "cupon_code": "bajevolp",
                "created_at": "2014-11-19T00:44:19+00:00",
                "sent_at": "2014-11-25T15:00:20+00:00",
                "paid_at": "2014-11-25T25:00:20+00:00",
                "payment": {
                    "type": "multibanco",
                    "data": {
                        "entity": 88888,
                        "reference": 888888888,
                        "value": 158.81
                    }
                },
                "status": 3,
                "status_alias": "sent",
                "paid": true,
                "is_new": false,
                "invoice_id": null,
                "weight": 0,
                "observations": "",
                "shipment_method": "Transportadora",
                "client": {
                    "name": "Shopkit",
                    "email": "info@shopk.it",
                    "address": "Centro de Empresas Inovadoras\nAvª do Empresário, 1, S1.08\n",
                    "postcode": "6000-767 ",
                    "town": "Castelo Branco",
                    "country": "Portugal - Continental",
                    "phone": "969057993",
                    "fiscal_id": ""
                },
                "products": [
                    {
                        "id": 44753,
                        "title": "Shelving Tree with Birds",
                        "reference": "STHFBF7574",
                        "price": 77.32,
                        "tax": 23,
                        "quantity": 1,
                        "subtotal": 77.32,
                        "weight": 0,
                        "url": false,
                        "description_short": "<p>This is a tree decal that is created to work with standard 24\" wall shelves that you can find at your local Target, Walmart, Ikea etc.. (shelving NOT INCLUDED) There are three locations where you can fit the shelves. This tree looks great on its own as well!<br /><br /><br />Tree Size (approx): 55&rdquo;w x 94&rdquo;h<br /><br />51\"w x 88\"h version is available upon request (they fit the same 24\" shelves). The price is the same. Please leave a note in the \"message to seller\" box during checkout if you would like the 88\"h version.<br /><br />At what heights would the shelf locations be at?<br />Standard Size Tree - (approx)<br />43\", 53\", 64\"<br /><br />For the 88\" Tree - (approx)<br />40\", 50\", 60\"</p>"
                    },
                    {
                        "id": 44752,
                        "title": "Hanging Succulent Planter",
                        "reference": "",
                        "price": 71.32,
                        "tax": 0,
                        "quantity": 1,
                        "subtotal": 71.32,
                        "weight": 0,
                        "url": false,
                        "description_short": "<p>This stoneware planter/pot has been hand made by me from earthy textured, speckled clay using the traditional methods of pinching and coiling. It has been decorated with a white glaze and high fired giving it strength and durability. Perfect for succulents and cactus plants, it has a drain hole in the base. The hanger twine is made from natural jute fibre.<br /><br />In many of my ceramic pieces you will find slight imperfections and marks left by the handmade process. These contribute to the uniqueness and beauty of the forms and are simply part of the character of the individual piece. As they are completely hand built, each piece is totally unique and may vary slightly from the image shown.&nbsp;<br /><br />This pot is approx 6cm (2.2\") tall and is 10cm (4\") across at the opening.</p>"
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


## Get Orders [/order{?status,status_alias,paid,date_filter,date_from,date_to,page,limit}]

## Get Orders [GET]
Get a list of orders

```bash
curl -i -X GET \
-H 'X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78' \
https://api.shopk.it/v1/order?status=3&date_filter=last_month
```

+ Parameters

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
    + page (optional, integer, `1`) ... Page number
    + limit = `25` (optional, integer, `10`) ... Orders per page


+ Response 200

   + Headers

            Content-Length: 422
            Content-Type: application/json

    + Body

            {
                "0": {
                    "id": 1337,
                    "total": 158.81,
                    "total_tax": 17.78,
                    "shipping": 7.25,
                    "discount": 14.86,
                    "cupon_code": "bajevolp",
                    "created_at": "2014-11-19T00:44:19+00:00",
                    "sent_at": null,
                    "paid_at": null,
                    "payment": {
                        "type": "multibanco",
                        "data": {
                            "entity": 88888,
                            "reference": 888888888,
                            "value": 158.81
                        }
                    },
                    "status": 5,
                    "status_alias": "waiting_confirmation",
                    "paid": false,
                    "is_new": false,
                    "invoice_id": null,
                    "weight": 0,
                    "observations": "",
                    "shipment_method": "Transportadora",
                    "client": {
                        "name": "Shopkit",
                        "email": "info@shopk.it",
                        "address": "Centro de Empresas Inovadoras\nAvª do Empresário, 1, S1.08\n",
                        "postcode": "6000-767 ",
                        "town": "Castelo Branco",
                        "country": "Portugal - Continental",
                        "phone": "969057993",
                        "fiscal_id": ""
                    },
                    "products": [
                        {
                            "id": 44753,
                            "title": "Shelving Tree with Birds",
                            "reference": "STHFBF7574",
                            "price": 77.32,
                            "tax": 23,
                            "quantity": 1,
                            "subtotal": 95.1036,
                            "weight": 0,
                            "url": false,
                            "description_short": "<p>This is a tree decal that is created to work with standard 24\" wall shelves that you can find at your local Target, Walmart, Ikea etc.. (shelving NOT INCLUDED) There are three locations where you can fit the shelves. This tree looks great on its own as well!<br /><br /><br />Tree Size (approx): 55&rdquo;w x 94&rdquo;h<br /><br />51\"w x 88\"h version is available upon request (they fit the same 24\" shelves). The price is the same. Please leave a note in the \"message to seller\" box during checkout if you would like the 88\"h version.<br /><br />At what heights would the shelf locations be at?<br />Standard Size Tree - (approx)<br />43\", 53\", 64\"<br /><br />For the 88\" Tree - (approx)<br />40\", 50\", 60\"</p>"
                        },
                        {
                            "id": 44752,
                            "title": "Hanging Succulent Planter",
                            "reference": "",
                            "price": 71.32,
                            "tax": 0,
                            "quantity": 1,
                            "subtotal": 71.32,
                            "weight": 0,
                            "url": false,
                            "description_short": "<p>This stoneware planter/pot has been hand made by me from earthy textured, speckled clay using the traditional methods of pinching and coiling. It has been decorated with a white glaze and high fired giving it strength and durability. Perfect for succulents and cactus plants, it has a drain hole in the base. The hanger twine is made from natural jute fibre.<br /><br />In many of my ceramic pieces you will find slight imperfections and marks left by the handmade process. These contribute to the uniqueness and beauty of the forms and are simply part of the character of the individual piece. As they are completely hand built, each piece is totally unique and may vary slightly from the image shown.&nbsp;<br /><br />This pot is approx 6cm (2.2\") tall and is 10cm (4\") across at the opening.</p>"
                        }
                    ]
                },
                "paging": null
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


# Group Webhooks
Webhooks enable to post data to your server whenever an event has happened. For more information on webhooks visit https://shopk.it/developers/webhook

## Post Webhook [/webhook/]

### Post Webhook [POST]
Create a webhook

```bash
curl -i -X POST \
-H "X-API-KEY:0bb18b34ba33cb2d7c55d568353fdc6f345b8d78" \
-H 'Content-Type:application/json' \
-d '{"url":"https://www.mysite.com/mywebhook_url", "event":"order_created"}' \
'http://api.shopk.it/v1/webhook'
```

<div class="well">

Attributes | Type | Choices | Description
---------- | ---- | ------- | -----------
**url** | string | | Webhook url
**event** | string |`order_canceled` `order_deleted` `order_created` `order_updated` `order_paid` `order_sent` `order_state` | Available webhooks

</div>


+ Response 201

    + Headers

            Content-Length: 96
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
