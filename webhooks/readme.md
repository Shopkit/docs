![Shopkit](https://drwfxyu78e9uq.cloudfront.net/assets/frontend/img/logo-shopkit-black-xs.png)

Welcome to the Shopkit Webhooks documentation.

Full documentation at https://shopk.it/developers/webhooks

If you find a bug or something worth fixing, create an issue or a pull request.

### How to compile documentation

Install [MkDocs](https://github.com/tomchristie/mkdocs), requires [Python](https://www.python.org/) and [pip](https://pip.pypa.io/en/stable/installation/) (Python package manager).

To generate documentation use: `mkdocs build --clean`, this creates a new directory, named `site` with the generated documentation inside.

### Changelog

##### 2025-04-08
* Add events `cart_abandoned`, `order_tag_added`, `client_tag_added`, `client_wholesale_accepted`, `client_wholesale_revoked`, `client_wholesale_requested`, `order_invoiced`, `shipping_expedited`
* Update payloads

##### 2022-10-27
* Update payload

##### 2022-03-08
* Add products wholesale

##### 2022-01-31
* Add events `product_created`, `product_updated`, `product_deleted`, `product_updated_stock`

##### 2021-09-06
* Add `order_waiting_shipment` event

##### 2021-08-23
* Add `X-Webhook-Resource-Origin` header

##### 2019-10-29
* Add `order_pickup_available` event
* Add `newsletter_subscribed` event
* Add `newsletter_unsubscribed` event

##### 2019-05-20
* Add `order_returned` event

##### 2017-12-06
* Add `order_shipping` event
* Update payload

##### 2017-08-14
* Add `order_delivered` event

##### 2017-06-06
* Add `X-Webhook-Signature` header
* Update payload

##### 2017-05-17
* Update payload

##### 2016-12-07
* Add `order.client.delivery`
* Add `order.client.billing`
* Update payload

##### 2016-12-07
* Add `order.hash`

##### 2016-10-26
* Add `coupon` object
* Add `order.subtotal`, `order.product_tax`
* Add `order.coupon` (`order.coupon.code`, `order.coupon.type`, `order.coupon.value`)
* Add to `order.product` (`order.product.discount`, `order.product.discount_percent`)
* Update `shipping` is now an object (`order.shipping.value`, `order.shipping.tax`, `order.shipping.tax_percent`, `order.shipping.discount`, `order.shipping.discount_percent`)
* Update `order.total_tax`
* Update payload

##### 2016-05-12
* Add `order.custom_field`

##### 2016-03-01
* Add `order_invoice` event

##### 2015-07-29
* Fixed misplaced quote

##### 2015-06-29
* Fixed typo `cupon_code`

##### 2015-05-13
* Add `order.currency`

##### 2015-05-12
* Add `order.products.option`
* Add `order.products.image`

##### 2015-03-11
* Initial release
