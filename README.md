# sails-magik-swagger

[![NPM version][npm-image]][npm-url]

[swagger.io](http://swagger.io/) (v2.0) hook for Sails. The application's models, controllers, and routes are aggregated and transformed into a Swagger Document. Supports the Swagger 2.0 specification.

## Install

```sh
$ npm install sails-magik-swagger --save
```

## Configuration
```js
// config/swagger.js
module.exports.swagger = {
  /**
   * require() the package.json file for your Sails app.
   */
  pkg: require('../package'),
  ui: {
    url: 'http://swagger.magikevolution.com'
  }
};
```

## Usage
After installing and configuring swagger, you can find the docs output on the [/swagger/doc](http://localhost:1337/swagger/doc) route.

You may also specify additional swagger endpoints by specifying the swagger spec in config/routes.js

```
/**
 * Route Mappings
 * @file config/routes.js
 * (sails.config.routes)
 *
 * Your routes map URLs to views and controllers.
 */

module.exports.routes = {

    /***************************************************************************
     *                                                                          *
     * Make the view located at `views/homepage.ejs` (or `views/homepage.jade`, *
     * etc. depending on your default view engine) your home page.              *
     *                                                                          *
     * (Alternatively, remove this and add an `index.html` file in your         *
     * `assets` directory)                                                      *
     *                                                                          *
     ***************************************************************************/

    '/': {
        view: 'homepage'
    },

    /***************************************************************************
     *                                                                          *
     * Custom routes here...                                                    *
     *                                                                          *
     * If a request to a URL doesn't match any of the custom routes above, it   *
     * is matched against Sails route blueprints. See `config/blueprints.js`    *
     * for configuration options and examples.                                  *
     *                                                                          *
     ***************************************************************************/
    'GET /groups/:id': {
        controller: 'Group',
        action: 'test',
        skipAssets: 'true',
        //swagger path object
        swagger: {
            methods: ['GET'],
            summary: ' Get Groups ',
            description: 'Get Groups Description',
            produces: [
                'application/json'
            ],
            tags: [
                'Groups'
            ],
            responses: {
                '200': {
                    description: 'List of Groups',
                    schema: 'Group', // api/model/Group.js,
                    type: 'array'
                }
            },
            parameters: []
        }
    },

    'POST /api/products': {
    controller: 'products',
    action: 'create',
    swagger: {
      methods: ['POST'],
      summary: 'Create Products',
      description: 'Create Products using....',
      produces: [
        'application/json'
      ],
      tags: [
        'Products'
      ],
      responses: {
        '201': {
          description: 'Product created',
          schema: 'products'
        }
      },
      parameters: [
        {
          "name": "$product",
          "in": "body",
          "description": "Product object to insert",
          "required": true,
          "schema": { $ref: '#/definitions/products' } // this links to products model 
        }
      ]
    }
  }
};

```

## License
MIT

## Maintained By
[<img src='http://www.magikevolution.com/img/logos/bola.png' height='64px'>](http://magikevolution.com)

[sails-url]: http://sailsjs.org
[npm-image]: https://img.shields.io/npm/v/sails-swagger.svg?style=flat
[npm-url]: https://npmjs.org/package/sails-magik-swagger

