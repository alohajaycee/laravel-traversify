# Traversify [Work-in-Progress]
[![Total Downloads](https://img.shields.io/packagist/v/alohajaycee/laravel-traversify.svg)](https://packagist.org/packages/alohajaycee/laravel-traversify)
## Installation
**Composer**

Install via composer using ``composer requrie alohajaycee/laravel-traversify``

**Model setup**

```php
use Traversify/Traversify;

use Eloquent;

class MyClass extends Eloquent {
	use Traversify;
}

```
**Controller Setup**

```php
use MyModel

class MyController {

     public function index() {

          return MyModel::traversify();

     }
}
```

## Configure
To use a search like function, you must create a static variables and assign an array containing an array of the fields that needed to be searched. These are the following:
* $searchbales
* $filterables
* $orderables
* $rangables

### Search
This uses a __%keyword%__ approach in sql. Traversify currently does not support scout or any advance search engine. For basic usage, this is more than enough.


```php 
use Traversify/Traversify;
    
    class MyModel {
    
    	use Traversify;
    
        public static $searchables = ['title', 'description']
    }
```

### Filter
Use filter for foreign key values of tables. This will only pull data whose foreign key values matches the requested filter.

```php 
use Traversify/Traversify;
    
    class MyModel {
    
    	use Traversify;
    
        public static $filterables = ['status_id', 'is_active']
    }
```

### Order / Sort
Can sort fields with number, letters, but is commonly used on dates which is also supported.

```php 
use Traversify/Traversify;
    
    class MyModel {
    
    	use Traversify;
    
        public static $orderables = ['created_at', 'is_active']
    }
```
### Range
Show records only that has values within the requested values. Requires 2 values, start & end.

```php 
use Traversify/Traversify;
    
    class MyModel {
    
    	use Traversify;
    
        public static $rangables = ['created_at', 'price']
    }
```
### Custom
For added custom query/s you can pass a query function inside ``traversify()``. This is then combined to the existing queries that traversify already uses.
```php
use MyModel;

class MyController {

     public function index()
     {
          return MyModel::traversify(function($q){
               
               $q->where('is_active', TRUE);
               
          });
     }
}

```
