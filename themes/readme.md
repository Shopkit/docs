![Shopkit](https://drwfxyu78e9uq.cloudfront.net/assets/frontend/img/logo-shopkit-black-xs.png)

Welcome to the Shopkit Themes documentation.

Full documentation at https://shopk.it/developers/themes

If you find a bug or something worth fixing, create an issue or a pull request.

### How to compile documentation

Install [MkDocs](https://github.com/tomchristie/mkdocs), requires [Python](https://www.python.org/) and [pip](https://pip.readthedocs.io/en/stable/installing/) (Python package manager).

To generate documentation use: `mkdocs build --clean`, this creates a new directory, named `site` with the generated documentation inside.

### Changelog

##### 2020-09-17
* Add `store.featured_blocks`

##### 2020-06-16
* Update `products` function `category` parameter now accepts an array

##### 2020-03-12
* Update `user.custom_field`

##### 2020-01-14
* Update `category` object

##### 2019-11-25
* Update `store` object

##### 2019-10-15
* Update `products` function with parameter `search`

##### 2019-09-19
* Add attributes `exclude` and `search` to products function

##### 2019-08-07
* Add filter  `e_attr`

##### 2019-03-07
* Add functions `pages` and `page`

##### 2018-10-23
* Add `category.image`

##### 2018-01-03
* Rename `promotions.tpl` to `sales.tpl`
* Rename `recent.tpl` to `new.tpl`

##### 2017-12-20
* Fix `page` object

##### 2017-12-13
* Update `cart` object

##### 2017-11-29
* Update `product` object
* `notices` are now `events`

##### 2017-04-10
* Update `blog_post.image` to array

##### 2017-03-31
* Remove `custom_html`

##### 2016-12-07
* Add `order.hash`

##### 2016-12-02
* Add `cart.payments` object
* Update `apps` object

##### 2016-11-28
* Move `payment` object into `store.payments`
* Remove `store.paypal_email`

##### 2016-11-09
* Add `store.navigation.primary.menu_item_handle`
* Add `store.navigation.secondary.menu_item_handle`

##### 2016-11-08
* Remove `cart.free_shipping`

##### 2016-10-19
* Fix typo

##### 2016-09-28
* Add `product.options.reference`
* Add `product.options.image`
* Clean up

##### 2016-05-12
* Add `user.custom_field`
* Add `order.custom_field`

##### 2016-03-02
* Add `apps`
* Add `store.navigation`
* Add `store.category_default_order`
* Add `cart.item.product_title`
* Add `cart.item.stock_qty`
* Add `notices.cart.product_data`
* Clean up deprecated properties

##### 2015-10-21
* Fix cart events

##### 2015-08-17
* Fix some descriptions

##### 2015-06-29
* Fix typo `cupon_code`

##### 2015-06-19
* Add `countries` global

##### 2015-06-15
* Add `price_on_request`

##### 2015-05-18
* Fix order payment data

##### 2015-05-12
* Add `payment.pick_up_msg`
* Fix `complete.tpl` order data

##### 2015-05-07
* Add `user.country_code`

##### 2015-04-29
* Add `{{ head_content }}` special variable

##### 2015-03-12
* Initial release
