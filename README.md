Laravel Binput
==============

Laravel Binput was created by, and is maintained by [Graham Campbell](https://github.com/GrahamCampbell), and is an input protector for [Laravel](http://laravel.com) that prevents potentially dangerous elements like `<script>` tags in any input you receive, from doing harm. It utilises my [Laravel Security](https://github.com/GrahamCampbell/Laravel-Security) package, which cleans the input using [voku/anti-xss](https://github.com/voku/anti-xss). Feel free to check out the [change log](CHANGELOG.md), [releases](https://github.com/GrahamCampbell/Laravel-Binput/releases), [security policy](https://github.com/GrahamCampbell/Laravel-Binput/security/policy), [license](LICENSE), [code of conduct](.github/CODE_OF_CONDUCT.md), and [contribution guidelines](.github/CONTRIBUTING.md).

![Banner](https://user-images.githubusercontent.com/2829600/71477342-6000a000-27e1-11ea-93d0-1ee413a31ab1.png)

<p align="center">
<a href="https://styleci.io/repos/12090308"><img src="https://styleci.io/repos/12090308/shield" alt="StyleCI Status"></img></a>
<a href="https://travis-ci.org/GrahamCampbell/Laravel-Binput"><img src="https://img.shields.io/travis/GrahamCampbell/Laravel-Binput/master.svg?style=flat-square" alt="Build Status"></img></a>
<a href="https://scrutinizer-ci.com/g/GrahamCampbell/Laravel-Binput/code-structure"><img src="https://img.shields.io/scrutinizer/coverage/g/GrahamCampbell/Laravel-Binput.svg?style=flat-square" alt="Coverage Status"></img></a>
<a href="https://scrutinizer-ci.com/g/GrahamCampbell/Laravel-Binput"><img src="https://img.shields.io/scrutinizer/g/GrahamCampbell/Laravel-Binput.svg?style=flat-square" alt="Quality Score"></img></a>
<a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square" alt="Software License"></img></a>
<a href="https://github.com/GrahamCampbell/Laravel-Binput/releases"><img src="https://img.shields.io/github/release/GrahamCampbell/Laravel-Binput.svg?style=flat-square" alt="Latest Version"></img></a>
</p>


## Installation

Laravel Binput requires [PHP](https://php.net) 7.1-7.4. This particular version supports Laravel 5.5-7.

| Binput | L5.1               | L5.2               | L5.3               | L5.4               | L5.5               | L5.6               | L5.7               | L5.8               | L6                 | L7                 |
|--------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|
| 3.6    | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x:                | :x:                | :x:                | :x:                | :x:                | :x:                |
| 4.0    | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x:                | :x:                | :x:                | :x:                | :x:                |
| 5.1    | :x:                | :x:                | :x:                | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x:                | :x:                | :x:                |
| 6.2    | :x:                | :x:                | :x:                | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x:                |
| 7.1    | :x:                | :x:                | :x:                | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |

To get the latest version, simply require the project using [Composer](https://getcomposer.org):

```bash
$ composer require graham-campbell/binput
```

Once installed, if you are not using automatic package discovery, then you need to register the `GrahamCampbell\Security\SecurityServiceProvider` and `GrahamCampbell\Binput\BinputServiceProvider` service providers in your `config/app.php`.

You can also optionally alias our facade:

```php
        'Binput' => GrahamCampbell\Binput\Facades\Binput::class,
```


## Configuration

Laravel Binput requires no configuration. Just follow the simple install instructions and go!


## Usage

##### Binput

This is the class of most interest. It is bound to the ioc container as `'binput'` and can be accessed using the `Facades\Binput` facade. There are a few public methods of interest.

The `'all'`, `'get'`, `'input'`, `'only'`, `'except'`, and `'old'` methods have an identical api to the methods found on the laravel request class accept from they all accept two extra parameters at the end. The first extra parameter is a boolean representing if the input should be trimmed. The second extra parameter is a boolean representing if the input should be xss cleaned. Both extra parameters are default to true.

There are two additional methods added to the public api. The first is a method called `'map'` which will remap the output from the `'only'` method. The `'map'` function requires an associative array as the first parameter. The second method is the `'clean'` function. It takes three parameters. The first is the value to be cleaned (it can be an array, and will be recursively iterated over and cleaned), and the final two are trim and clean, which behave in the same way as earlier.

Any methods not found on this binput class will actually fall back to the laravel request class with a dynamic call function, so every other method on the request class is available in exactly the same way it would be on the Laravel request class.

##### Facades\Binput

This facade will dynamically pass static method calls to the `'binput'` object in the ioc container which by default is the `Binput` class.

##### BinputServiceProvider

This class contains no public methods of interest. This class should be added to the providers array in `config/app.php`. This class will setup ioc bindings.


##### Real Examples

Here you can see an example of just how simple this package is to use.

```php
// request input data: ['test' => '123', 'foo' => '<script>alert(\'bar\');</script>    ']

$input = Binput::all(); // ['test' => '123', 'foo' => '']
```


## Security

If you discover a security vulnerability within this package, please send an email to Graham Campbell at graham@alt-three.com. All security vulnerabilities will be promptly addressed. You may view our full security policy [here](https://github.com/GrahamCampbell/Laravel-Binput/security/policy).


## License

Laravel Binput is licensed under [The MIT License (MIT)](LICENSE).


---

<div align="center">
	<b>
		<a href="https://tidelift.com/subscription/pkg/packagist-graham-campbell-binput?utm_source=packagist-graham-campbell-binput&utm_medium=referral&utm_campaign=readme">Get professional support for Laravel Binput with a Tidelift subscription</a>
	</b>
	<br>
	<sub>
		Tidelift helps make open source sustainable for maintainers while giving companies<br>assurances about security, maintenance, and licensing for their dependencies.
	</sub>
</div>
