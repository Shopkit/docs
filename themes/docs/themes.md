# Shopkit Themes

Welcome to the **Shopkit** theme documentation.
If you want to build a theme from scratch or just want to customize your current one, we've got everything you need.

Get to know how is the basic anatomy of a theme, our language syntax, functions, filters and tags. We also have some code samples to get you started.

<div class="callout callout-info">
  <strong>Not a developer?</strong> <a href="https://shopk.it/get-quote">Contact us</a> for a free quote.
</div>

### Getting Started

To customize a theme, you need to clone it first. Choose what theme you want to start from, clone it and work from there.

Our template language is based on [Twig](http://twig.sensiolabs.org). We suggest you to take a look on the official [twig documentation](http://twig.sensiolabs.org/documentation) to learn the basics and syntax.

We keep an updated [Github repo](https://github.com/Shopkit/Template-Default) with the default theme, so you can check the code and subscribe for updates we may add over time.

A Shopkit theme consists of 17 pages:

| Page       | Filename         | Description                                         |
|------------|------------------|-----------------------------------------------------|
| About      | `about.tpl`      | About page template                                 |
| Base       | `base.tpl`       | The base template                                   |
| Blog       | `blog.tpl`       | Blog template                                       |
| Cart       | `cart.tpl`       | Shopping cart template                              |
| Category   | `category.tpl`   | Product category template                           |
| Complete   | `complete.tpl`   | Complete order template                             |
| Confirm    | `confirm.tpl`    | Confirm order template                              |
| Contact    | `contact.tpl`    | Contact page template                               |
| Data       | `data.tpl`       | Order data form template                            |
| Home       | `home.tpl`       | Pomepage template                                   |
| Page       | `page.tpl`       | Page template                                       |
| Payment    | `payment.tpl`    | Payment template                                    |
| Post       | `post.tpl`       | Blog post template                                  |
| Product    | `product.tpl`    | Product template                                    |
| Sales      | `sales.tpl`      | Sales products template                             |
| New        | `new.tpl`        | New products template                               |
| Search     | `search.tpl`     | Search Results template                             |

The base template is the most important, where all other templates are included.
Header, footer and other components that are always displayed, must be set in base template.
It's required that this is included in every template with this code `{% extends 'base.tpl' %}`

This is a stripped down HTML template:

```twig
<html>
  <head>
   <title>{{ title }}</title>
    <link rel="stylesheet" href="{{ store.assets.css }}">
    {{ head_content }}
  </head>
  <body>
    {% block content %}{% endblock %}
    {{ footer_content }}
  </body>
</html>
```

```twig
{% extends 'base.tpl' %}

{% block content %}
  <h1>{{ page.title }}</h1>
  <div>{{ page.content }}</div>
{% endblock %}
```

<div class="callout callout-info">
  The <code>{{ head_content }}</code> and <code>{{ footer_content }}</code> are required to assure the theme works properly.
</div>

### Syntax

There are two kinds of delimiters: `{% ... %}` and `{{ ... }}`. The first one is used to execute statements such as for-loops, the latter prints the result of an expression to the template.

#### Twig reference

This is the Twig reference: tags, filters, functions, tests and operators.
You can use these *as is*, we have not modified any of their behavior.

##### Tags

Tags control the logic of the template.

| Tag                                                               | Description                                                                                                                                                          |
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [block](http://twig.sensiolabs.org/doc/tags/block.html)           | Blocks are used for inheritance and act as placeholders and replacements at the same time.                                                                           |
| [extends](http://twig.sensiolabs.org/doc/tags/extends.html)       | The extends tag can be used to extend a template from another one.                                                                                                   |
| [filter](http://twig.sensiolabs.org/doc/tags/filter.html)         | Filter sections allow you to apply regular Twig filters on a block of template data.                                                                                 |
| [for](http://twig.sensiolabs.org/doc/tags/for.html)               | Loop over each item in a sequence.                                                                                                                                   |
| [if](http://twig.sensiolabs.org/doc/tags/if.html)                 | The if statement in Twig is comparable with the if statements of PHP.                                                                                                |
| [set](http://twig.sensiolabs.org/doc/tags/set.html)               | Inside code blocks you can also assign values to variables. Assignments use the set tag and can have multiple targets.                                               |
| [spaceless](http://twig.sensiolabs.org/doc/tags/spaceless.html)   | Use the spaceless tag to remove whitespace between HTML tags, not whitespace within HTML tags or whitespace in plain text.                                           |
| [use](http://twig.sensiolabs.org/doc/tags/use.html)               | The use tag imports a template without using inheritance. Template inheritance is one of the most powerful Twig's feature but it is limited to single inheritance.   |

For a comprehensive list of tags refer to the [twig website](http://twig.sensiolabs.org/doc/tags/index.html).

##### Filters

Variables can be modified by filters. Filters are separated from the variable by a pipe symbol (`|`) and may have optional arguments in parentheses. Multiple filters can be chained. The output of one filter is applied to the next.

| Filter                                                                           | Description                                                                                                                                           |
|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| [abs](http://twig.sensiolabs.org/doc/filters/abs.html)                           | The abs filter returns the absolute value.                                                                                                            |
| [batch](http://twig.sensiolabs.org/doc/filters/batch.html)                       | The batch filter "batches" items by returning a list of lists with the given number of items.                                                         |
| [capitalize](http://twig.sensiolabs.org/doc/filters/mintalize.html)              | The capitalize filter capitalizes a value. The min character will be uppercase, all others lowercase.                                                 |
| [date](http://twig.sensiolabs.org/doc/filters/date.html)                         | The date filter formats a date to a given format.                                                                                                     |
| [date_modify](http://twig.sensiolabs.org/doc/filters/date_modify.html)           | The date_modify filter modifies a date with a given modifier string.                                                                                  |
| [escape](http://twig.sensiolabs.org/doc/filters/escape.html)                     | The escape filter escapes a string for safe insertion into the final output.                                                                          |
| [first](http://twig.sensiolabs.org/doc/filters/first.html)                       | The first filter returns the first "element" of a sequence, a mapping, or a string.                                                                   |
| [format](http://twig.sensiolabs.org/doc/filters/format.html)                     | The format filter formats a given string by replacing the placeholders (placeholders follows the sprintf notation).                                   |
| [join](http://twig.sensiolabs.org/doc/filters/join.html)                         | The join filter returns a string which is the concatenation of the items of a sequence.                                                               |
| [json_encode](http://twig.sensiolabs.org/doc/filters/json_encode.html)           | The json_encode filter returns the JSON representation of a value.                                                                                    |
| [keys](http://twig.sensiolabs.org/doc/filters/keys.html)                         | The keys filter returns the keys of an array. It is useful when you want to iterate over the keys of an array.                                        |
| [last](http://twig.sensiolabs.org/doc/filters/last.html)                         | The last filter returns the last "element" of a sequence, a mapping, or a string.                                                                     |
| [length](http://twig.sensiolabs.org/doc/filters/length.html)                     | The length filter returns the number of items of a sequence or mapping, or the length of a string.                                                    |
| [lower](http://twig.sensiolabs.org/doc/filters/lower.html)                       | The lower filter converts a value to lowercase.                                                                                                       |
| [merge](http://twig.sensiolabs.org/doc/filters/merge.html)                       | The merge filter merges an array with another array                                                                                                   |
| [nl2br](http://twig.sensiolabs.org/doc/filters/nl2br.html)                       | The nl2br filter inserts HTML line breaks before all newlines in a string.                                                                            |
| [number_format](http://twig.sensiolabs.org/doc/filters/number_format.html)       | The number_format filter formats numbers. It is a wrapper around PHP's number_format function.                                                        |
| [reverse](http://twig.sensiolabs.org/doc/filters/reverse.html)                   | The reverse filter reverses a sequence, a mapping, or a string.                                                                                       |
| [round](http://twig.sensiolabs.org/doc/filters/round.html)                       | The round filter rounds a number to a given precision.                                                                                                |
| [slice](http://twig.sensiolabs.org/doc/filters/slice.html)                       | The slice filter extracts a slice of a sequence, a mapping, or a string.                                                                              |
| [sort](http://twig.sensiolabs.org/doc/filters/sort.html)                         | The sort filter sorts an array.                                                                                                                       |
| [split](http://twig.sensiolabs.org/doc/filters/split.html)                       | The split filter splits a string by the given delimiter and returns a list of strings.                                                                |
| [striptags](http://twig.sensiolabs.org/doc/filters/striptags.html)               | The striptags filter strips SGML/XML tags and replace adjacent whitespace by one space.                                                               |
| [title](http://twig.sensiolabs.org/doc/filters/title.html)                       | The title filter returns a titlecased version of the value. Words will start with uppercase letters, all remaining characters are lowercase.          |
| [trim](http://twig.sensiolabs.org/doc/filters/trim.html)                         | The trim filter strips whitespace (or other characters) from the beginning and end of a string.                                                       |
| [upper](http://twig.sensiolabs.org/doc/filters/upper.html)                       | The upper filter converts a value to uppercase.                                                                                                       |
| [url_encode](http://twig.sensiolabs.org/doc/filters/url_encode.html)             | The url_encode filter percent encodes a given string as URL segment or an array as query string.                                                      |

For a comprehensive list of tags refer to the [twig website](http://twig.sensiolabs.org/doc/filters/index.html).

##### Functions

Functions can be called to generate content. Functions are called by their name followed by parentheses (`()`) and may have arguments.

| Function                                                                     | Description                                                                                                                                               |
|------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [attribute](http://twig.sensiolabs.org/doc/functions/attribute.html)         | The attribute function can be used to access a "dynamic" attribute of a variable.                                                                         |
| [block](http://twig.sensiolabs.org/doc/functions/block.html)                 | When a template uses inheritance and if you want to print a block multiple times, use the block function.                                                 |
| [cycle](http://twig.sensiolabs.org/doc/functions/cycle.html)                 | The cycle function cycles on an array of values.                                                                                                          |
| [date](http://twig.sensiolabs.org/doc/functions/date.html)                   | Converts an argument to a date to allow date comparison.                                                                                                  |
| [max](http://twig.sensiolabs.org/doc/functions/max.html)                     | max returns the biggest value of a sequence or a set of values.                                                                                           |
| [min](http://twig.sensiolabs.org/doc/functions/min.html)                     | min returns the lowest value of a sequence or a set of values.                                                                                            |
| [random](http://twig.sensiolabs.org/doc/functions/random.html)               | The random function returns a random value depending on the supplied parameter type.                                                                      |
| [range](http://twig.sensiolabs.org/doc/functions/range.html)                 | Returns a list containing an arithmetic progression of integers.                                                                                          |

For a comprehensive list of tags refer to the [twig website](http://twig.sensiolabs.org/doc/functions/index.html).

##### Tests

Tests can be used to test a variable against a common expression.

| Test                                                                      | Description                                                                                                                                                  |
|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [defined](http://twig.sensiolabs.org/doc/tests/defined.html)              | Checks if a variable is defined in the current context.                                                                                              |
| [divisible by](http://twig.sensiolabs.org/doc/tests/divisibleby.html)     | Checks if a variable is divisible by a number.                                                                                                  |
| [empty](http://twig.sensiolabs.org/doc/tests/empty.html)                  | Checks if a variable is empty.                                                                                                                         |
| [even](http://twig.sensiolabs.org/doc/tests/even.html)                    | Returns true if the given number is even.                                                                                                               |
| [iterable](http://twig.sensiolabs.org/doc/tests/iterable.html)            | Checks if a variable is an array or a traversable object.                                                                                           |
| [null](http://twig.sensiolabs.org/doc/tests/null.html)                    | Returns true if the variable is null.                                                                                                                   |
| [odd](http://twig.sensiolabs.org/doc/tests/odd.html)                      | Returns true if the given number is odd.                                                                                                                 |
| [same as](http://twig.sensiolabs.org/doc/tests/sameas.html)               | Checks if a variable is the same as another variable. This is the equivalent to === in PHP.                                                          |

For a comprehensive list of tags refer to the [twig website](http://twig.sensiolabs.org/doc/tests/index.html).

##### Operators

| Operator                                                                  | Description                                                                                                                                         |
|---------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| [in](http://twig.sensiolabs.org/doc/templates.html#containment-operator)  | The in operator performs containment test. It returns true if the left operand is contained in the right                                            |
| [is](http://twig.sensiolabs.org/doc/templates.html#test-operator)         | The is operator performs tests. Tests can be used to test a variable against a common expression. The right operand is name of the test             |
| [Math](http://twig.sensiolabs.org/doc/templates.html#math)                | `(+, -, /, %, //, *, **)`                                                                                                                           |
| [Logic](http://twig.sensiolabs.org/doc/templates.html#math)               | `(and, or, not, (), b-and, b-xor, b-or)`                                                                                                            |
| [Comparisons](http://twig.sensiolabs.org/doc/templates.html#comparisons)  | `(==, !=, <, >, >=, <=, ===, starts with, ends with, matches)`                                                                                      |
| [Others](http://twig.sensiolabs.org/doc/templates.html#other-operators)   | <code>(.., &#124;, ~, ., [], ?:)</code>                                                                                                             |


#### Shopkit reference

These are our proprietary functions, filters and tags.

##### Filters

###### `money_with_sign`

Returns a value formatted with the currency set in user account settings.

```twig
{{ item.price|money_with_sign }}
```

Prints <samp>122,95 €</samp>

##### Functions

###### `form_open`

Creates an opening form tag with a base URL built from your shop address. It will optionally let you add form attributes, and will always add the attribute accept-charset.

```twig
{{ form_open('cart/complete', {'class':'my-css-class', 'id':'my-id'}) }}
```

The above example would create a form that points to your base URL plus the "cart/complete" URI segments.

```html
<form action="http:/example.com/cart/complete" method="post" accept-charset="utf-8" class="my-css-class" id="my-id" />
```

These are special Shopkit form actions:

| Action                | Description                                 |
|-----------------------|---------------------------------------------|
| `newsletter/register` | Submit a newsletter form                    |
| `contact_form`        | Submit the contact form                     |
| `cart/update`         | Action to update the cart form              |
| `cart/complete`       | Action to the last step of checkout         |
| `cart/post/payment`   | Action to the payment step of checkout      |
| `cart/post/confirm`   | Action to the confirmation step of checkout |


###### `form_open_cart`  

Creates an opening form tag with the url to add a product to the cart. It will optionally let you add form attributes, and will always add the attribute accept-charset.
This is different from `form_open` because you pass the product id, instead of the URL.

```twig
{{ form_open_cart(product.id, {'class':'my-css-class'}) }}
```

###### `form_close`

Produces a closing `</form>` tag.

```twig
{{ form_close() }}
```

###### `products`

Returns a list of products with defined parameters.

You can list products from different pools:

* `featured` List products marked as featured
* `new` List products marked as new/recent
* `on_sale` List products marked as promotion/on sale
* `search` List products based on a search

*If you don't set a pool, no filter will be applied and all products will be retrieved.*

###### Examples:

```twig
{% set products = products('featured limit:9') %}
{# Assigns a variable with featured products limited by 9 per page #}
```

```twig
{% for product in products('order:featured') %}
{# Returns all products ordered by featured #}
```

```twig
{% for product in products('order:#{get.order_by} category:#{category.id} limit:25') %}
{# Returns products from the current category, ordered by a get parameter (?order_by) with a limit of 25 items per page #}
```

###### Parameters

| Attributes   | Type    | Choices                                                                                          | Description                                    |
|--------------|---------|--------------------------------------------------------------------------------------------------|------------------------------------------------|
| `order`      | string  | `title`, `newest`, `sales`, `views`, `price_asc`, `price_desc`, `featured`, `position`, `random` | Product order options, see table below         |
| `category`   | integer |                                                                                                  | Product category identifier                    |
| `paginate`   | string  | `true`, `false`                                                                                  | Enable or disable pagination. Default: `true`  |
| `limit`      | integer |                                                                                                  | The number of products to return. Default: `9` |
| `offset`     | integer |                                                                                                  | The product starting from. Default: `0`        |

###### `product`

Returns a single product by id.

```twig
{% set my_product = product(1337) %}
```

###### `category`

Returns the category and all children categories, a category identifier is mandatory.

```twig
{% set my_category = category(1337) %}
```

###### `pages`

Returns a list of all pages.

```twig
{% set my_pages = pages() %}
```

###### `page`

Returns a single page by id.

```twig
{% set my_page = page(1337) %}
```

###### `blog_posts`

Returns a list of blog posts. Optionally you can limit the number of posts. Default: `9`

```twig
{% for post in blog_posts('limit:9') %}
```

###### `pagination`

Pagination auto detects the template and outputs the according pagination with defined parameters, an extra class parameter can also be set.

###### Examples:

```twig
{{ pagination('limit:9') }}
{# outputs a pagination with a limit of 9 items per page #}
```

```twig
{% set products_per_page = 9 %}
{% set products_category = category.id %}

{% for product in products('category:#{products_category} limit:#{products_per_page}') %}
  <h1>{{ product.title }}</h1>
{% endfor %}

{{ pagination('category:#{products_category} limit:#{products_per_page}', 'my-css-class') }}

{# outputs a pagination with a limit of 9 items and passes an extra class #}
```

<div class="callout callout-warning">
  The <code>pagination()</code> parameters must match the loop function <code>products()</code>.
</div>

###### `site_url`

Returns your site URL, segments can be passed to the function as a string.

```twig
{{ site_url('blog') }}
```

Prints <samp>http:/example.com/blog</samp>

###### `current_url`

Returns the full URL (including segments) of the page being currently viewed.

```twig
{{ current_url() }}
```

###### `safe_mailto`

Creates a standard HTML email link. It writes an obfuscated version of the mailto tag using ordinal numbers written with JavaScript to help prevent the email address from being harvested by spam bots.

```twig
{{ safe_mailto('email@example.com') }}
```

###### `word_limiter`

Truncates a string to the number of words specified

```twig
{{ word_limiter(text, 250) }}
```

###### `character_limiter`

Truncates a string to the number of characters specified. It maintains the integrity of words so the character count may be slightly more or less then what you specify.

```twig
{{ character_limiter(text, 100) }}
```

### Variables

#### Common

These are variables available in all templates.

##### Generic

| Name                                        | Description                                                                                                                        |
|---------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| `css_class`                                 | CSS helper class(es) injected in the body tag related to the current page. Example: `<body class="page-product product-id-16644">` |
| `current_page`                              | Global variable to help you identifying the current template. Example: `cart`                                                      |
| `countries`                                 | Global array with the list of store available countries. Used in `data.tpl`                                                        |

##### Store

Used for retrieving store information, set on the Account Settings page of your backoffice.

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `store.username`                            | Store username                                                      |
| `store.name`                                | Store name                                                          |
| `store.logo`                                | Store logo URL                                                      |
| `store.description`                         | Store description                                                   |
| `store.notice`                              | Store notice                                                        |
| `store.facebook`                            | Store Facebook URL                                                  |
| `store.twitter`                             | Store Twitter URL                                                   |
| `store.instagram`                           | Store Instagram URL                                                 |
| `store.pinterest`                           | Store Pinterest URL                                                 |
| `store.show_email`                          | Show email in contacts page                                         |
| `store.show_branding`                       | Show Shopkit love                                                   |
| `store.email`                               | Store email                                                         |
| `store.phone`                               | Store phone                                                         |
| `store.cellphone`                           | Store cellphone                                                     |
| `store.address`                             | Store address                                                       |
| `store.basecolor`                           | Store basecolor                                                     |
| `store.favicon`                             | Store favicon URl                                                   |
| `store.latitude`                            | Store latitude                                                      |
| `store.longitude`                           | Store longitude                                                     |
| `store.currency`                            | Store currency                                                      |
| `store.custom_css`                          | Store custom CSS                                                    |
| `store.custom_js`                           | Store custom JavaScript                                             |
| `store.footer_info`                         | Store footer info                                                   |
| `store.page_title`                          | Store page title                                                    |
| `store.meta_description`                    | Store meta description                                              |
| `store.meta_tags`                           | Store meta tags                                                     |
| `store.navigation`                          | Store navigation array                                              |
| `store.payments`                            | Store payments array                                                |
| `store.category_default_order`              | Store category default order                                        |
| `store.domain`                              | Store current domain                                                |
| `store.assets`                              | Store assets array                                                  |
| `store.taxes_included`                      | Store taxes included option                                         |
| `store.images_header`                       | Store header images array                                           |


##### Special pages

These pages are automatically created and cannot be deleted, also have a particular template file. Although the content of these pages are available globally and can be used anywhere.

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `store.page.about.title`                    | Page about title                                                    |
| `store.page.about.content`                  | Page about content                                                  |
| `store.page.about.url`                      | Page about url                                                      |
| `store.page.about.meta_description`         | Page about meta description                                         |
| `store.page.about.meta_tags`                | Page about meta tags                                                |
| `store.page.about.handle`                   | Page about handle                                                   |
| `store.page.about.page_title`               | Page about title                                                    |
| `store.page.contact.title`                  | Page contact title                                                  |
| `store.page.contact.content`                | Page contact content                                                |
| `store.page.contact.url`                    | Page contact url                                                    |
| `store.page.contact.meta_description`       | Page contact meta description                                       |
| `store.page.contact.meta_tags`              | Page contact meta tags                                              |
| `store.page.contact.handle`                 | Page contact handle                                                 |
| `store.page.contact.page_title`             | Page contact title                                                  |


##### Navigation

Contains data about store navigation

| Name                                          | Description                                                                         |
|-----------------------------------------------|-------------------------------------------------------------------------------------|
| `store.navigation.primary.menu_text`          | Primary navigation text to display                                                  |
| `store.navigation.primary.menu_type`          | Primary navigation type. `menu_url`, `menu_product`, `menu_category`, `menu_page`   |
| `store.navigation.primary.menu_url`           | Primary navigation url                                                              |
| `store.navigation.primary.menu_item`          | Primary navigation item                                                             |
| `store.navigation.primary.menu_item_handle`   | Primary navigation item handle                                                      |
| `store.navigation.primary.target_blank`       | Primary navigation option open link in new window. `true`, `false`                  |
| `store.navigation.secondary.menu_text`        | Secondary navigation text to display                                                |
| `store.navigation.secondary.menu_type`        | Secondary navigation type. `menu_url`, `menu_product`, `menu_category`, `menu_page` |
| `store.navigation.secondary.menu_url`         | Secondary navigation url                                                            |
| `store.navigation.secondary.menu_item`        | Secondary navigation item                                                           |
| `store.navigation.secondary.menu_item_handle` | Secondary navigation item handle                                                    |
| `store.navigation.secondary.target_blank`     | Secondary navigation option open link in new window. `true`, `false`                |


##### Payments

Used for retrieving store payments options information.

| Name                                          | Description                                                         |
|-----------------------------------------------|---------------------------------------------------------------------|
| `store.payments.paypal.active`                | Payment Paypal option is enabled                                    |
| `store.payments.paypal.email`                 | Payment Paypal email                                                |
| `store.payments.paypal.message`               | Payment Paypal message                                              |
| `store.payments.paypal.min_value`             | Payment Paypal order minimum value                                  |
| `store.payments.paypal.max_value`             | Payment Paypal order maximum value                                  |
| `store.payments.multibanco.active`            | Payment multibanco option is enabled                                |
| `store.payments.multibanco.entity`            | Payment multibanco entity                                           |
| `store.payments.multibanco.user`              | Payment multibanco user                                             |
| `store.payments.multibanco.cin`               | Payment multibanco cin                                              |
| `store.payments.multibanco.message`           | Payment multibanco message                                          |
| `store.payments.multibanco.min_value`         | Payment multibanco order minimum value                              |
| `store.payments.multibanco.max_value`         | Payment multibanco order maximum value                              |
| `store.payments.bank_transfer.active`         | Payment bank transfer option is enabled                             |
| `store.payments.bank_transfer.message`        | Payment bank transfer message                                       |
| `store.payments.bank_transfer.min_value`      | Payment bank transfer minimum value                                 |
| `store.payments.bank_transfer.max_value`      | Payment bank transfer maximum value                                 |
| `store.payments.on_delivery.active`           | Payment on delivery option is enabled                               |
| `store.payments.on_delivery.value`            | Payment on delivery value                                           |
| `store.payments.on_delivery.message`          | Payment on delivery message                                         |
| `store.payments.on_delivery.min_value`        | Payment on delivery minimum value                                   |
| `store.payments.on_delivery.max_value`        | Payment on delivery maximum value                                   |
| `store.payments.pick_up.active`               | Payment facilities pick up option is enabled                        |
| `store.payments.pick_up.message`              | Payment facilities pick up message                                  |
| `store.payments.pick_up.min_value`            | Payment facilities pick up minimum value                            |
| `store.payments.pick_up.max_value`            | Payment facilities pick up maximum value                            |


##### Apps

Used for retrieving data about enabled apps. The global `apps` object is available globally.

| Name                                            | Description                                                                      |
|-------------------------------------------------|----------------------------------------------------------------------------------|
| `apps.adult_content.title`                      | App Adult Content title                                                          |
| `apps.adult_content.url`                        | App Adult Content url                                                            |
| `apps.adult_content.description`                | App Adult Content description                                                    |
| `apps.adult_content.text_color`                 | App Adult Content title                                                          |
| `apps.adult_content.bg_color`                   | App Adult Content text color code                                                |
| `apps.adult_content.bg_color`                   | App Adult Content background color code                                          |
| `apps.bablic.embed`                             | App Bablic embed code                                                            |
| `apps.cookies.text`                             | App Cookies bar text                                                             |
| `apps.cookies.link`                             | App Cookies bar url                                                              |
| `apps.cookies.bg_color`                         | App Cookies bar background color code                                            |
| `apps.cookies.text_color`                       | App Cookies bar text color code                                                  |
| `apps.delivery_date.title`                      | App Delivery Date title                                                          |
| `apps.delivery_date.description`                | App Delivery Date description                                                    |
| `apps.delivery_date.field_label`                | App Delivery field label                                                         |
| `apps.facebook_comments.username`               | App Facebook Comments username                                                   |
| `apps.facebook_comments.comments_products`      | App Facebook Comments on products is enabled. `true` or `false`                  |
| `apps.facebook_comments.comments_blog`          | App Facebook Comments on blog is enabled. `true` or `false`                      |
| `apps.facebook_page.facebook_url`               | App Facebook Page, Facebook URL                                                  |
| `apps.facebook_pixel.track`                     | App Facebook Pixel track code                                                    |
| `apps.facebook_store`                           | App Facebook Store is enabled. `true`                                            |
| `apps.followprice.store_key`                    | App Followprice Store key                                                        |
| `apps.getsocial.id`                             | App GetSocial id                                                                 |
| `apps.google_analytics.tracking_id`             | App Google Analytics tracking id                                                 |
| `apps.google_analytics_ec`                      | App Google Analytics Ecommerce is enabled. `true`                                |
| `apps.google_recaptcha.sitekey`                 | App Google reCAPTCHA Site Key                                                    |
| `apps.google_translate.languages`               | App Google Translate languages, list of languages comma separated. e.g. `en, es` |
| `apps.google_webmaster_tools.site_verification` | App Google Webmasters HTML tag                                                   |
| `apps.hello_bar.embed`                          | App Hello Bar embed code                                                         |
| `apps.invoicexpress`                            | App InvoiceXpress is enabled. `true`                                             |
| `apps.kuantokusta.trackk`                       | App KuantoKusta tracking code                                                    |
| `apps.localizejs.project_key`                   | App Localize project key                                                         |
| `apps.mailchimp`                                | App Newsletter is enabled. `true`                                                |
| `apps.moloni`                                   | App Moloni is enabled. `true`                                                    |
| `apps.newsletter`                               | App Newsletter is enabled. `true`                                                |
| `apps.tawk.embed`                               | App Tawk embed code                                                              |
| `apps.uservoice.embed`                          | App UserVoice embed code                                                         |
| `apps.zopim.embed`                              | App Zopim embed code                                                             |


##### Categories

Used for retrieving product categories data. The global `categories` object is available globally.

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `categories.id`                             | Category identifier                                                 |
| `categories.title`                          | Category title                                                      |
| `categories.description`                    | Category description                                                |
| `categories.parent`                         | Category parent identifier                                          |
| `categories.handle`                         | Category handle                                                     |
| `categories.page_title`                     | Category page title                                                 |
| `categories.meta_description`               | Category meta description                                           |
| `categories.meta_tags`                      | Category meta tags                                                  |
| `categories.image`                          | Category array with images in 3 sizes: thumb, square, full          |
| `categories.url`                            | Category url                                                        |
| `categories.total_products`                 | Category total products                                             |
| `categories.children`                       | Category array of children categories                               |


##### Cart

Used for retrieving shopping cart data.

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `cart.items`                                | Cart items *(see below the object attributes)*                      |
| `cart.total`                                | Cart total                                                          |
| `cart.shipping_methods`                     | Cart shipping methods *(see below the object attributes)*           |
| `cart.payments`                             | Cart payments methods *(see below the object attributes)*           |
| `cart.discount`                             | Cart discount                                                       |
| `cart.total_shipping`                       | Cart total number of products                                       |
| `cart.item_count`                           | Cart total number of unique products                                |
| `cart.taxes`                                | Cart total taxes                                                    |
| `cart.weight`                               | Cart total weight                                                   |
| `cart.subtotal`                             | Cart subtotal                                                       |


`cart.items`

Contains data about each product in the shopping cart.

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `cart.items.item_id`                        | Cart item identifier                                                |
| `cart.items.product_id`                     | Cart product identifier                                             |
| `cart.items.product_title`                  | Cart product title                                                  |
| `cart.items.product_url`                    | Cart product URL                                                    |
| `cart.items.remove_link`                    | Cart remove product URL                                             |
| `cart.items.qty`                            | Cart product quantity                                               |
| `cart.items.price`                          | Cart product price                                                  |
| `cart.items.price_without_tax`              | Cart product price before taxes                                     |
| `cart.items.discount`                       | Cart product discount value                                         |
| `cart.items.discount_percent`               | Cart product discount percent                                       |
| `cart.items.tax_percent`                    | Cart product tax percentage                                         |
| `cart.items.tax`                            | Cart product tax value                                              |
| `cart.items.taxes_total`                    | Cart product total taxes                                            |
| `cart.items.weight`                         | Cart product weight                                                 |
| `cart.items.title`                          | Cart product title                                                  |
| `cart.items.reference`                      | Cart product reference                                              |
| `cart.items.stock_sold_single`              | Cart stock sold single option                                       |
| `cart.items.metadata`                       | Cart product metadata                                               |
| `cart.items.image`                          | Cart product image URL                                              |
| `cart.items.shipping_alone`                 | Cart shipping alone option                                          |
| `cart.items.shipping`                       | Cart shipping                                                       |
| `cart.items.subtotal`                       | Cart product subtotal                                               |
| `cart.items.subtotal_without_tax`           | Cart product subtotal before taxes                                  |
| `cart.items.total`                          | Cart product total                                                  |


`cart.shipping_methods`

Contains data about available shipping methods.

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `cart.shipping_methods.id`                  | Cart shipping method identifier                                     |
| `cart.shipping_methods.title`               | Cart shipping method title                                          |
| `cart.shipping_methods.description`         | Cart shipping method description                                    |
| `cart.shipping_methods.price`               | Cart shipping method price                                          |


`cart.payments`

Contains data about available payments methods.

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `cart.payments.paypal.active`               | Payment Paypal option is enabled                                    |
| `cart.payments.paypal.email`                | Payment Paypal email                                                |
| `cart.payments.paypal.message`              | Payment Paypal message                                              |
| `cart.payments.paypal.min_value`            | Payment Paypal order minimum value                                  |
| `cart.payments.paypal.max_value`            | Payment Paypal order maximum value                                  |
| `cart.payments.multibanco.active`           | Payment multibanco option is enabled                                |
| `cart.payments.multibanco.entity`           | Payment multibanco entity                                           |
| `cart.payments.multibanco.user`             | Payment multibanco user                                             |
| `cart.payments.multibanco.cin`              | Payment multibanco cin                                              |
| `cart.payments.multibanco.message`          | Payment multibanco message                                          |
| `cart.payments.multibanco.min_value`        | Payment multibanco order minimum value                              |
| `cart.payments.multibanco.max_value`        | Payment multibanco order maximum value                              |
| `cart.payments.bank_transfer.active`        | Payment bank transfer option is enabled                             |
| `cart.payments.bank_transfer.message`       | Payment bank transfer message                                       |
| `cart.payments.bank_transfer.min_value`     | Payment bank transfer minimum value                                 |
| `cart.payments.bank_transfer.max_value`     | Payment bank transfer maximum value                                 |
| `cart.payments.on_delivery.active`          | Payment on delivery option is enabled                               |
| `cart.payments.on_delivery.value`           | Payment on delivery value                                           |
| `cart.payments.on_delivery.message`         | Payment on delivery message                                         |
| `cart.payments.on_delivery.min_value`       | Payment on delivery minimum value                                   |
| `cart.payments.on_delivery.max_value`       | Payment on delivery maximum value                                   |
| `cart.payments.pick_up.active`              | Payment facilities pick up option is enabled                        |
| `cart.payments.pick_up.message`             | Payment facilities pick up message                                  |
| `cart.payments.pick_up.min_value`           | Payment facilities pick up minimum value                            |
| `cart.payments.pick_up.max_value`           | Payment facilities pick up maximum value                            |


##### Pages

Used for retrieving store pages information, other then special pages.

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `pages.id`                                  | Page identifier                                                     |
| `pages.title`                               | Page title                                                          |
| `pages.content`                             | Page content                                                        |
| `pages.url`                                 | Page url                                                            |
| `pages.meta_description`                    | Page meta description                                               |
| `pages.meta_tags`                           | Page meta tags                                                      |
| `pages.handle`                              | Page handle                                                         |
| `pages.page_title`                          | Page browser title                                                  |

#### Category

This data is only available on the `category.tpl` template

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `category.id`                               | Category identifier                                                 |
| `category.title`                            | Category title                                                      |
| `category.description`                      | Category description                                                |
| `category.parent`                           | Category parent identifier                                          |
| `category.handle`                           | Category handle                                                     |
| `category.page_title`                       | Category page title                                                 |
| `category.meta_description`                 | Category meta description                                           |
| `category.meta_tags`                        | Category meta tags                                                  |
| `category.image`                            | Category array with images in 3 sizes: thumb, square, full          |
| `category.url`                              | Category url                                                        |
| `category.total_products`                   | Category total products                                             |
| `category.children`                         | Category array of children categories                               |


#### Page

This data is only available on the `page.tpl` template

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `page.id`                                   | Page identifier                                                     |
| `page.title`                                | Page title                                                          |
| `page.content`                              | Page content                                                        |
| `page.url`                                  | Page url                                                            |
| `page.meta_description`                     | Page meta description                                               |
| `page.meta_tags`                            | Page meta tags                                                      |
| `page.handle`                               | Page handle                                                         |
| `page.page_title`                           | Page title                                                          |


#### Blog post

This data is only available on the `post.tpl` template

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `blog_post.id`                              | Post identifier                                                     |
| `blog_post.url`                             | Post URL                                                            |
| `blog_post.meta_description`                | Post meta description                                               |
| `blog_post.meta_tags`                       | Post meta tags                                                      |
| `blog_post.handle`                          | Post handle                                                         |
| `blog_post.page_title`                      | Post page title                                                     |
| `blog_post.image`                           | Post array with images in 3 sizes: thumb, square, full              |
| `blog_post.title`                           | Post title                                                          |
| `blog_post.text`                            | Post text content                                                   |
| `blog_post.date`                            | Post date                                                           |


#### Product

This data is only available on the `product.tpl` template

| Name                                        | Description                                                                |
|---------------------------------------------|----------------------------------------------------------------------------|
| `product.id`                                | Product identifier                                                         |
| `product.title`                             | Product title                                                              |
| `product.reference`                         | Product reference                                                          |
| `product.price`                             | Product price                                                              |
| `product.price_promo`                       | Product promotion price                                                    |
| `product.promo_show_percentage`             | Product show price promotion percentage                                    |
| `product.price_on_request`                  | Product has price on request                                               |
| `product.promo`                             | Product is on promotion                                                    |
| `product.created_at`                        | Product creation date                                                      |
| `product.status`                            | Product status as an integer                                               |
| `product.status_alias`                      | Product status as a string                                                 |
| `product.position`                          | Product order position                                                     |
| `product.shipping`                          | Product shipping cost                                                      |
| `product.shipping_alone`                    | Product ships alone                                                        |
| `product.featured`                          | Product is featured attribute                                              |
| `product.new`                               | Product is new attribute                                                   |
| `product.is_promotion`                      | Product is promotion attribute                                             |
| `product.description`                       | Product description                                                        |
| `product.description_short`                 | Product short description                                                  |
| `product.video_url`                         | Product video URL                                                          |
| `product.video_embed_url`                   | Product video embed URL                                                    |
| `product.file`                              | Product file attachment URL                                                |
| `product.tax`                               | Product tax cost                                                           |
| `product.weight`                            | Product weight                                                             |
| `product.hits`                              | Product hits                                                               |
| `product.sales`                             | Product number of sales                                                    |
| `product.meta_description`                  | Product meta description                                                   |
| `product.meta_tags`                         | Product meta tags                                                          |
| `product.handle`                            | Product handle                                                             |
| `product.page_title`                        | Product page title                                                         |
| `product.url`                               | Product URL                                                                |
| `product.permalink`                         | Product permalink                                                          |
| `product.add_cart_url`                      | Product add to cart URL                                                    |
| `product.images`                            | Product array with images in 3 sizes:  `thumb`, `square`, `full`           |
| `product.image`                             | Product featured image array in 3 sizes: `thumb`, `square`, `full`         |
| `product.categories`                        | Array with  categories associated with the product                         |
| `product.option_groups`                     | Array with product option groups (variants)                                |
| `product.options`                           | Lists all option groups (variants) combined. Example: `XL / Blue / Cotton` |
| `product.stock`                             | Array with stock settings                                                  |
| `product.wishlist`                          | Array with wishlist URL                                                    |

`product.categories`

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `product.categories.id`                     | Product category identifier                                         |
| `product.categories.parent`                 | Product category parent identifier                                  |
| `product.categories.title`                  | Product category title                                              |
| `product.categories.description`            | Product category description                                        |
| `product.categories.handle`                 | Product category handle                                             |
| `product.categories.url`                    | Product category URL                                                |
| `product.categories.image`                  | Product category array with images in 3 sizes: thumb, square, full  |

`product.stock`

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `product.stock.stock_enabled`               | Product stock is enabled                                            |
| `product.stock.stock_qty`                   | Product stock quantity                                              |
| `product.stock.stock_backorder`             | Product allows back orders                                          |
| `product.stock.stock_show`                  | Show product stock information                                      |
| `product.stock.stock_sold_single`           | Product can only sold single                                        |

`product.options`

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `product.options.id`                        | Product option identifier                                           |
| `product.options.id_variant_1`              | Product option variant 1 identifier                                 |
| `product.options.id_variant_2`              | Product option variant 2 identifier                                 |
| `product.options.id_variant_3`              | Product option variant 3 identifier                                 |
| `product.options.title`                     | Product option title                                                |
| `product.options.price`                     | Product option price                                                |
| `product.options.promo`                     | Product option is on promotion                                      |
| `product.options.price_promo`               | Product option promotion price                                      |
| `product.options.price_on_request`          | Product option has price on request                                 |
| `product.options.stock`                     | Product option stock quantity                                       |
| `product.options.shipping`                  | Product option shipping cost                                        |
| `product.options.weight`                    | Product option weight                                               |
| `product.options.reference`                 | Product option reference                                            |
| `product.options.active`                    | Product option is enabled                                           |
| `product.options.url`                       | Product option URL                                                  |
| `product.options.image`                     | Product option image array in 3 sizes: `thumb`, `square`, `full`    |
| `product.options.wishlist`                  | Product option wishlist links: `add_url`, `remove_url`              |

`product.option_groups`

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `product.option_groups.title`               | Product option group title                                          |
| `product.option_groups.options`             | Array with `product.options`                                        |


`product.wishlist`

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `product.wishlist.add_url`                  | Product add to wishlist URL                                         |
| `product.wishlist.remove_url`               | Product remove from wishlist URL                                    |
| `product.wishlist.status`                   | Product is on wishlist status                                       |


#### Search

This data is only available on the `search.tpl` template

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `search.query`                              | Returns the search query                                            |

#### User

This data is only available on the `payment.tpl`, `data.tpl`, `confirm.tpl` and  `complete.tpl` templates

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `user.name`                                 | Name of the client                                                  |
| `user.email`                                | E-mail address of the client                                        |
| `user.address`                              | Address of the client                                               |
| `user.zip_code`                             | Zip code of the client                                              |
| `user.city`                                 | City of the client                                                  |
| `user.country`                              | Country of the client                                               |
| `user.country_code`                         | Country alpha-3 code of the client                                  |
| `user.phone`                                | Phone number of the client                                          |
| `user.tax_id`                               | Fiscal id of the client                                             |
| `user.notes`                                | Observations/notes that client added in the checkout                |
| `user.coupon`                               | Coupon code used by the client                                      |
| `user.payment`                              | Payment type selected by the client                                 |
| `user.shipping_method`                      | Array with shipping method data selected by the client              |
| `user.shipping_method.id`                   | Identifier of the shipping method                                   |
| `user.shipping_method.title`                | Title of the shipping method                                        |
| `user.custom_field`                         | Data from custom fields                                             |

`user.custom_field`

You can create custom fields with custom data in the checkout process. This data will be passed to the order.
`custom_field` is an array field containing a json, with the following structure:

```json
{"title":"The title of your custom field","key":"the key","value":"the value"}
```

You can have as many custom fields as you want/need.
Usually you register the custom field with an html input:

```twig
<input type="text" name="custom_field[field_name_1]" value='{{ user.custom_field.field_name_1 }}'>
```

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `user.custom_field.field_name_1.title`      | Title of the custom field named `field_name_1`                      |
| `user.custom_field.field_name_1.key`        | Key of the custom field named `field_name_1`                        |
| `user.custom_field.field_name_1.value`      | Value of the custom field named `field_name_1`                      |

<div class="callout callout-info">
  You can use our helper function to generate the json strucuture: <code>custom_field_encode('Your title', 'your_key', 'Your value')</code>
</div>

#### Order

This data is only available on the `complete.tpl` and `mailorder.tpl` templates

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `order.id`                                  | Order identifier                                                    |
| `order.hash`                                | Order identifier hash                                               |
| `order.total`                               | Order total value                                                   |
| `order.total_tax`                           | Order total taxes value                                             |
| `order.shipping`                            | Order shipping cost value                                           |
| `order.discount`                            | Order discount value                                                |
| `order.coupon_code`                         | Order coupon code                                                   |
| `order.created_at`                          | Order creation date                                                 |
| `order.update_at`                           | Order last update date                                              |
| `order.sent_at`                             | Order sent date                                                     |
| `order.paid_at`                             | Order paid date                                                     |
| `order.payment`                             | Order payment type                                                  |
| `order.msg_payment`                         | Order payment message                                               |
| `order.status`                              | Order status as an integer                                          |
| `order.status_alias`                        | Order status as an string                                           |
| `order.paid`                                | Order paid status boolean                                           |
| `order.is_new`                              | New order boolean                                                   |
| `order.invoice_url`                         | Order invoice permalink                                             |
| `order.weight`                              | Order weight value                                                  |
| `order.observations`                        | Order customer observations                                         |
| `order.shipment_method`                     | Order shipment method chosen by the customer                        |
| `order.multibanco`                          | Array with order Multibanco data                                    |
| `order.client`                              | Array with order client data                                        |
| `order.products`                            | Array with order products data                                      |
| `order.custom_field`                        | Array with data from custom field                                   |

`order.multibanco`

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `order.multibanco.entity`                   | Order Multibanco entity                                             |
| `order.multibanco.reference`                | Order Multibanco reference                                          |
| `order.multibanco.value`                    | Order Multibanco value                                              |

`order.client`

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `order.client.name`                         | Order client name                                                   |
| `order.client.email`                        | Order client email                                                  |
| `order.client.address`                      | Order client address                                                |
| `order.client.postcode`                     | Order client postal code                                            |
| `order.client.town`                         | Order client town                                                   |
| `order.client.country`                      | Order client country                                                |
| `order.client.phone`                        | Order client phone number                                           |
| `order.client.fiscal_id`                    | Order client fiscal identifier                                      |

`order.products`

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `order.products.id`                         | Order products identifier                                           |
| `order.products.title`                      | Order products title                                                |
| `order.products.option`                     | Order products option                                               |
| `order.products.reference`                  | Order products reference                                            |
| `order.products.price`                      | Order products price value                                          |
| `order.products.tax`                        | Order products tax value                                            |
| `order.products.quantity`                   | Order products quantity                                             |
| `order.products.subtotal`                   | Order products subtotal                                             |
| `order.products.weight`                     | Order products weight                                               |
| `order.products.url`                        | Order products url                                                  |
| `order.products.description_short`          | Order products short description                                    |
| `order.products.image.thumb`                | Order products image format thumb                                   |
| `order.products.image.square`               | Order products image format square                                  |
| `order.products.image.full`                 | Order products image format full                                    |

#### GET & POST

You can use custom `GET` and `POST` variables:

To retrieve the parameter from the URL `http:/example.com/?foo=bar`

```twig
{{ get.foo }}
```
Prints <samp>bar</samp>

### Assets

These assets are available to include and expand functionalities. Can be changed in Account settings > Templates

| Name                                        | Description                                                         |
|---------------------------------------------|---------------------------------------------------------------------|
| `store.assets.url`                          | Store assets base URL                                               |
| `store.assets.images`                       | Store assets images URL                                             |
| `store.assets.css`                          | Store asset CSS URL                                                 |
| `store.assets.plugins`                      | Store asset plugins URL                                             |
| `store.assets.scripts`                      | Store asset scripts URL                                             |

To include the CSS file:

```html
<link rel="stylesheet" href="{{ store.assets.css }}">
```

To include the plugins and scripts files:

```html
<script src="{{ store.assets.plugins }}"></script>
<script src="{{ store.assets.scripts }}"></script>
```

### Events

Every time an action occurs, an event is available for the current request. If the user leaves the current page it will no longer be available.

#### Cart events

| Name                                       | Description                                                                                    |
|--------------------------------------------|------------------------------------------------------------------------------------------------|
| `events.cart.added`                        | A product was added to the shopping cart                                                       |
| `events.cart.error`                        | An error occurred while performing an action to the shopping cart                              |
| `events.cart.updated`                      | A product in the shopping cart was updated                                                     |
| `events.cart.deleted`                      | A product was removed from the shopping cart                                                   |
| `events.cart.stock_sold_single`            | Fires when client is trying to purchase more than 1 unit and the product does not allow it     |
| `events.cart.stock_qty`                    | Fires if the product added to the cart does not have enough stock                              |
| `events.cart.no_stock`                     | Contains all products that were not updated/added to cart because of not having enough stock   |
| `events.cart.product_data`                 | Contains information about the product added, updated or deleted to the shopping cart          |
| `events.cart.qty`                          | Contains the quantity added to the shopping cart, fires when add or update                     |

#### Misc events

| Name                                       | Description                                                                                    |
|--------------------------------------------|------------------------------------------------------------------------------------------------|
| `events.paypal_success`                    | A payment through Paypal was successful                                                        |
| `events.contact_form_success`              | The contact form was sent with success                                                         |
| `events.contact_form_errors`               | Contains erros if the contact form was not sent                                                |

### Recipes

##### Allow categories to sort products by criteria

```twig
{#  Setup order #}
{% set order_options = { 'position' : 'Relevance', 'title' : 'Title', 'newest' : 'New', 'sales' : 'Popular', 'price_asc' : 'Price: low to high', 'price_desc' : 'Price: high to low' } %}

{% if not get.order_by in order_options|keys %}
  {% set get = {'order_by': 'position'} %}
{% endif %}

<div class="order-options">
  Sort by

  <div class="btn-group">

    <button type="button" class="btn btn-default btn-sm dropdown-toggle" data-toggle="dropdown">
      {% if get.order_by and order_options[get.order_by] %}
        {{ order_options[get.order_by] }}
      {% else %}
        {{ order_options['position'] }}
      {% endif %}
      <span class="caret"></span>
    </button>

    <ul class="dropdown-menu" role="menu">
      {% for order_option, order_title in order_options %}
        {% if order_option != get.order_by %}
          <li><a href="{{ category.url }}?order_by={{ order_option }}">{{ order_title }}</a></li>
        {% endif %}
      {% endfor %}
    </ul>
  </div>
</div>
```

##### Show random products from a list of products

Because of aggressive Shopkit caching, you might not be able to achieve randomness in every page request, so you want to random in the runtime instead of querying random products. ie: `products('featured order:random limit:3')`

```twig
{% set products = products('featured limit:25') %}
{% set products_to_show = 3 %}

{% for product in products|slice(random(products|length - products_to_show), products_to_show) %}
  <h1>{{ product.title }}</h1>
{% endfor %}
```

<small class="last-modified">Last Modified 2019-03-07T16:10:08+00:00</small>