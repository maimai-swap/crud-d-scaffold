# Crud-D-Scaffold for Laravel 5.5

  Hi, this is a scaffold generator for Laravel 5.5.
  You can Create Basic CRUD application by using this package.
  (For laravel 5.4, use package version 2.3.0)

  The CRUD application generated by this package has the following features.

  [ General ]
* In addition to the basic CRUD (new creation, detail display, update, delete), there is a "Duplicate" function.
* Adopted Bootstrap 3 for display
* Describe application configuration in setting file -> Automatic generation completed by command execution.
* At the time of execution from the second time, all newly overwritten by the -f option (excluding the migration file)
* it is possible to create One-to-many relation creation between models
* The main creation files are model, controller, migration, seeding, view

[ List Page ]
* Refine search available (Text input items are partially matched, otherwise the range specification)
* You can sort by each item.
* Pager function.
* You can set columns Display or non-display in the initial setting file.
* When deleting, there is confirmation.

[ New registration / edit / duplication page ]
* Input format can be selected from input or textarea
* However, a column with belongsto relation displays a pulldown.



## Latest Release note

#### Ver 2.4.0

  It corresponds to laravel 5.5.
  And, it became possible to coexist with the authentication incorporated in Laravel.

## How to installation and execution

### Step 1: Installing package through Composer

```
composer require dog-ears/crud-d-scaffold
```

### Step 2: Run Artisan!

You're all set.
Run `php artisan` from the console, and you'll see the new commands below.
```
- 'crud-d-scaffold:setup' : Setup crud-d-scaffold with bootstrap 3
```

  This completes the preparation.  
  Let's register the sample.  

### Step 3: Crud-D-Scaffold

##### (i) publish public resource.
```
php artisan vendor:publish --tag=public --force
```
##### (ii) Copy /vendor/dog-ears/crud-d-scaffold/crud-d-scaffold.json.sample to your laravel project root
```
cp ./vendor/dog-ears/crud-d-scaffold/crud-d-scaffold.json.sample ./crud-d-scaffold.json
```
##### (iii) run crud-d-scaffold:setup
```
php artisan crud-d-scaffold:setup -f
```
  Overwriting the file with -f option.  
  For the first time, the f option is unnecessary. (No problem with putting on)

##### (iii) run migration and seeding
```
php artisan migrate
```
```
php artisan db:seed
```

  It's all over.  
  Please check your application.

  If you want to modify the application structure,
  After running [migrate: rollback], delete the migration file (/ database / migrations /) and then
  execute [ Crud-d-scaffold: setup-f ]



## Specification of crud-d-scaffold.json

- /*...*/ It is treated as a comment.
- please surround it with double quotation like "true".

```
{
    "app_type": "web",                          /* [default:web]  */	<-  Currently, only 'web' is acceptable
    "use_laravel_auth": "false",                  /* [default:false]  */	<-  If you want use laravel auth, set "true"
    "models": [
        {
            "name": "jointAuthor",              /* [required] format[nameName] */				<-  Name of model
            "display_name": "JOINT AUTHOR",     /* [required] */								<-  Display name of the model
            "schemas": [
                {
                    "name": "realName",         /* [required] */								<-  Column name (In the case of relation, make it model name _id)
                    "type": "string",           /* [default:string] ex( integer, string ) */	<-  Column type
                    "input_type": "text",       /* [default:text] text, textarea */ /* relation_column forced to pulldown */
                    "faker_type": "name()",     /* [default -> no seeding] ex( randomDigit(), randomNumber(2), numberBetween(1,30), word(), sentence(), paragraph(), text(), name(), address(), date('Y-m-d','now'), safeEmail(), password() )  */	<-  seed faker type (If not, it is generated by '' (please make nullable "true") )
                    "nullable": "false",        /* [default:false] ex( true, false ) */			<-  Whether null is allowed or not
                    "display_name": "REAL NAME",/* [required] */								<-  Display name
                    "show_in_list": "true",     /* [default:true] ex( true, false ) */			<-  Whether to display on the list page
                    "show_in_detail": "true",   /* [default:true] ex( true, false ) */			<-  Whether to display on the detail page
					"belongsto": "",            /* [default:""] */								<-  Target model to belongsto
					"belongsto_column": ""      /* [default:""] */								<-  Column name of target model to be displayed in relation column
                },{

```

## Options
-f, --force Overwrite the file. (If there is an existing file in the absence of the option, processing stops there.)



## Screen Capture
![image](https://github.com/dog-ears/crud-d-scaffold/wiki/img/cap01.jpg)
![image](https://github.com/dog-ears/crud-d-scaffold/wiki/img/cap02.jpg)
![image](https://github.com/dog-ears/crud-d-scaffold/wiki/img/cap03.jpg)



## Usage notes

* You can use laravel auth. At first [ php artisan make:auth ] and run crud-d-scaffold.
* You can not change / delete tables, change columns or delete columns. Create a new one from 0 and overwrite it.
* Column names, model names, etc. are automatically converted according to the convention of laravel, so it is not possible to create singular and plural models at the same time.



## Functions to be implemented in the future

* Enable to choose as web application or backend api.
* create package for angular front-end with crud-d-scaffold.json.(it is about another package.)
* form validation
* Display the list of hasmany objects on detail page
* Implement file upload form
* Generate test Files

and so on



## Testing

This package is tested by laravel dusk.
see below repository.

https://github.com/dog-ears/crud-d-scaffold-dusktest



## See more information

visit my blog
<http://dog-ears.net/en/category/laravel/package/scaffold/history/>
