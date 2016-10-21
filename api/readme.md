![Shopkit](https://drwfxyu78e9uq.cloudfront.net/assets/frontend/img/logo-shopkit-black-xs.png)

Welcome to the Shopkit REST API documentation.

Full documentation at https://shopk.it/developers/api

If you find a bug or something worth fixing, create an issue or a pull request.

### How to compile documentation

Install [Aglio](https://github.com/danielgtaylor/aglio), requires Node.js, at this date, use v0.10.x.

Optional: install [Node Version Manager](https://github.com/creationix/nvm) to manage Node.js versions.

To generate documentation use: `aglio -i api.md -o index.html`

### Changelog

##### 2016-10-20
* Add `product.options.url`
* Add `product.options.id_variant_1`, `product.options.id_variant_2`, `product.options.id_variant_3`

##### 2016-09-28
* Add `product.options.reference`
* Add `product.options.image.thumb`, `product.options.image.square`, `product.options.image.full`
* Add `product.categories.handle`
* Add `product.stock.stock_notify`

##### 2016-05-12
* Add `order.custom_field`

##### 2016-03-09
* Remove `store.translate_meta`

##### 2016-03-01
* Add `order.note`
* Add `order.client_note`
* Add `webhook.event` choice `order_invoice`
* Replace `order.invoice_id` to `order.invoice_url`
* Hard limit lowered to 50

##### 2015-06-29
* Fixed typo `cupon_code`

##### 2015-06-22
* Fix typo on the `X-API-KEY` param

##### 2015-06-15
* Add `price_on_request`
* Update `product` example

##### 2015-05-13
* Add `order.currency`
* Fix Content-Length values

##### 2015-05-12
* Add `order.products.option`
* Add `order.products.image`

##### 2015-03-29
* Changed `order_state` to `order_change_status`

##### 2015-03-12
* Added order_put > invoice_id
* Fixed texts and typos

##### 2015-03-05
* Added webhooks post and delete
* Fixed orders responses
* Uniform methods syntax

##### 2015-02-10
* Initial release
