![Shopkit](https://drwfxyu78e9uq.cloudfront.net/assets/frontend/img/logo-shopkit-black-xs.png)

Welcome to the Shopkit Themes documentation.

Full documentation at https://shopk.it/developers/themes

If you find a bug or something worth fixing, create an issue or a pull request.

### How to compile documentation

Install [MkDocs](https://github.com/tomchristie/mkdocs), requires [Python](https://www.python.org/) and [pip](http://pip.readthedocs.org/en/latest/installing.html) (Python package manager).

To generate documentation use: `mkdocs build --clean`, this creates a new directory, named `site` with the generated documentation inside.

### Changelog

##### 2016-10-19
* Fixed typo

##### 2016-09-28
* Added `product.options.reference`
* Added `product.options.image`
* Clean up

##### 2016-05-12
* Added `user.custom_field` and `order.custom_field`

##### 2016-03-02
* Added `apps`
* Added `store.navigation`
* Added `store.category_default_order`
* Added `cart.item.product_title`
* Added `cart.item.stock_qty`
* Added `notices.cart.product_data`
* Clean up deprecated properties

##### 2015-10-21
* Fixed cart events

##### 2015-08-17
* Fixed some descriptions

##### 2015-06-29
* Fixed typo `cupon_code`

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
