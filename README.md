# Pagination.js

> A jQuery plugin to provide simple yet fully customisable pagination.

[![Bower version][bower-image]][bower-url]

[bower-url]:http://badge.fury.io/bo/paginationjs
[bower-image]: https://badge.fury.io/bo/paginationjs.svg

<img src="examples/images/paginationjs_record.gif" alt="paginationjs" width="500">

See demos and full documentation at official site: [http://paginationjs.com](http://paginationjs.com)

# Installation / Download

`bower install paginationjs` or just download [pagination.js](dist/pagination.js) from the git repo.

# Quick Start

HTML:

```html
<div id="data-container"></div>
<div id="pagination-container"></div>
```

JS:

```js
$('#pagination-container').pagination({
    dataSource: [1, 2, 3, 4, 5, 6, 7, ... , 195],
    callback: function(data, pagination) {
        // template method of yourself
        var html = template(data);
        $('#data-container').html(html);
    }
})
```

# Data rendering

Below is a minimal data rendering method:

```js
function simpleRender(data) {
    var html = '<ul>';
    $.each(data, function(index, item){
        html += '<li>'+ item +'</li>';
    });
    html += '</ul>';
    return html;
}
```

Calling:

```js
$('#container').pagination({
    dataSource: [1, 2, 3, 4, 5, 6, 7, ... , 195],
    callback: function(data, pagination) {
        var html = simpleRender(data);
        dataContainer.html(html);
    }
})
```

To make it easier to maintain, you'd better use specialized templating engine to do the data rendering.

Below is an example using [undercore.template](http://underscorejs.org/#template):

```js
$('#container').pagination({
    dataSource: [1, 2, 3, 4, 5, 6, 7, ... , 195],
    callback: function(data, pagination) {
        var html = _.template(templateString, {
            data: data
        });

        /* templateString:
        <ul>
        <% for (var i = 0, len = data.length; i < len; i++) { %>
            <li><%= data[i] %></li>
        <% } %>
        </ul>
        */

        dataContainer.html(html);
    }
})
```

Using [Handlebars](http://handlebarsjs.com/):

```js
$('#container').pagination({
    dataSource: [1, 2, 3, 4, 5, 6, 7, ... , 195],
    callback: function(data, pagination) {
        var html = Handlebars.compile(templateString, {
            data: data
        });

        /* templateString:
        <ul>
        {{#each data}}
            <li>{{this}}</li>
        </ul>
        {{/each}}
        */

        dataContainer.html(html);
    }
})
```

Or any other templating engine what you prefer.

# License

Released under the MIT license.

MIT: [http://rem.mit-license.org](http://rem.mit-license.org/), See [LICENSE](/LICENSE)