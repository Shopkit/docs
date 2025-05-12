![Shopkit](https://drwfxyu78e9uq.cloudfront.net/assets/frontend/img/logo-shopkit-black-xs.png)

Welcome to the Shopkit REST API documentation.

Full documentation at https://shopk.it/developers/api

If you find a bug or something worth fixing, create an issue or a pull request.

### How to compile documentation

Install [Aglio](https://github.com/danielgtaylor/aglio), requires Node.js, at this date, use v0.10.x.

Optional: install [Node Version Manager](https://github.com/creationix/nvm) to manage Node.js versions.

To generate documentation use: `aglio -i api.md -o index.html`

### Changelog

##### 2025-04-12
* update `client` methods `POST`, `PUT`

##### 2025-04-08
* Add `client` methods `POST`, `PUT`, `DELETE`

##### 2024-10-22
* Add `order` `PUT` parameter `invoice_file`
* Add `order` `GET` parameters `shipped`, `invoice`

##### 2024-09-23
* Add `client` method `GET`
* Add `shipment` method `GET`
* Add `shipment/carrier` method `GET`
* Add `stats` method `GET`
* Add `order/invoice` method `GET`
* Update`order` methods `GET`, `PUT`
* Update`product` methods `POST`, `PUT`

##### 2023-03-08
* Add `PUT` `order/bulk`

##### 2023-02-16
* Add `order` `GET` parameter `ids`
* Add `order` `PUT` parameter `tracking_carrier`

##### 2022-10-27
* Add `order` field `at_code`

##### 2022-05-26
* Add GET `product` and GET `order` can now combine `status`

##### 2022-04-08
* Add `brand` methods `GET`, `POST`, `PUT`, `DELETE`

##### 2022-03-08
* Add products wholesale

##### 2021-09-06
* Add orders status `waiting_shipment`

##### 2021-07-16
* Add `product/search`

##### 2021-07-07
* Add product `product.taxable`, `product.reduced_rate`

##### 2021-05-25
* Add header `X-Total-Count`

##### 2021-05-14
* Add `GET /store` to replace deprecated `GET /`

##### 2021-05-09
* Add `media` methods `GET`, `POST`, `DELETE`

##### 2021-02-19
* Add `category` methods `POST`, `PUT`, `DELETE`
* Update `category` `GET` `active`, `active`, `is_parent`, `page`, `limit`

##### 2021-01-27
* Add `product` `GET` parameter `ids`

##### 2021-01-05
* Update products with `barcode`, `brand`, `tags`

##### 2020-12-14
* Add `product` methods `POST`, `DELETE`
* Add `product_option_group` methods `GET`, `POST`, `PUT`, `DELETE`
* Add `product_option` methods `GET`, `PUT`, `DELETE`
* Add `webhook` methods `GET`

##### 2020-05-26
* Add `Already exists.` messages
* Update available webhooks list

##### 2020-05-19
* Fix typo

##### 2020-01-14
* Update `category` payload

##### 2019-11-25
* Update `store` payload

##### 2019-10-29
* Add orders status `returned`, `pickup_available`

##### 2018-10-23
* Add `category.image`

##### 2018-06-20
* Add `product` `GET` parameter `q`

##### 2018-06-06
* Update `order` `GET` parameter `date_type` default value

##### 2018-05-29
* Add `product.price_formatted`, `product.price_promo_formatted`, `product.shipping_url`
* Add `order` `GET` parameter `date_type`

##### 2018-01-03
* Update product payload

##### 2017-12-06
* Add `order.tracking_url`, `order.tracking_code`, `order.shipping_url`, `order.pickup_code`
* Update payloads

##### 2017-09-15
* Get `category` parameters are optional

##### 2017-08-14
* Add `order` status `delivered`
* Add event `order_delivered`

##### 2017-06-13
* Add `order.tracking_url`

##### 2017-05-17
* Update `store` payload
* Update `product` payload
* Update `order` payload

##### 2017-03-29
* Fix `product`, `order` duplicated entries

##### 2017-03-09
* Add `coupon` `GET`, `POST`, `DELETE`
* Add `order` `GET` by `coupon_code`

##### 2017-01-18
* Fix links protocol

##### 2017-01-06
* Add shipping endpoint

##### 2016-12-07
* Add `order.hash`
* update payloads

##### 2016-11-28
* Add `store.navigation`
* Add `store.payments`
* update payload

##### 2016-10-26
* Add `coupon` object
* Add `order.subtotal`, `order.product_tax`
* Add `order.coupon` (`order.coupon.code`, `order.coupon.type`, `order.coupon.value`)
* Add to `order.product` (`order.product.discount`, `order.product.discount_percent`)
* Update `shipping` is now an object (`order.shipping.value`, `order.shipping.tax`, `order.shipping.tax_percent`, `order.shipping.discount`, `order.shipping.discount_percent`)
* Update `order.total_tax`
* Update payload

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
* Change `order_state` to `order_change_status`

##### 2015-03-12
* Add order_put > invoice_id
* Fix texts and typos

##### 2015-03-05
* Add webhooks post and delete
* Fix orders responses
* Uniform methods syntax

##### 2015-02-10
* Initial release
