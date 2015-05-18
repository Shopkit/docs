![Shopkit](https://drwfxyu78e9uq.cloudfront.net/assets/frontend/img/logo-shopkit-black-xs.png)

Welcome to the Shopkit Themes documentation.

Full documentation at https://shopk.it/developers/themes

If you find a bug or something worth fixing, create an issue or a pull request.

### How to compile documentation

Install [MkDocs](https://github.com/tomchristie/mkdocs), requires [Python](https://www.python.org/) and [pip](http://pip.readthedocs.org/en/latest/installing.html) (Python package manager).

To generate documentation use: `mkdocs build --clean`, this creates a new directory, named `site` with the generated documentation inside.

### Changelog

#### 2015-05-18
* Fix order payment data

#### 2015-05-12
* Add `payment.pick_up_msg`
* Fix `complete.tpl` order data

#### 2015-05-07
* Add `user.country_code`

#### 2015-04-29
* Add `{{ head_content }}` special variable

#### 2015-03-12
* Initial release
