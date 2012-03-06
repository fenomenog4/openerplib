# openerplib

openerplib es una librería para PHP que permite realizar operaciones xml-rpc con OpenERP 
cómodamente.

Está inspirada en ORM de [Django](https://www.djangoproject.com/)

## Requeriments

openerlib depende de:

* xmlrpc.inc >= 1.174 http://phpxmlrpc.sourceforge.net/ (incluida)

## Installation

No requiere ningún tipo de instalación especial. Copiar directorio /openerplib 
donde ser quiera utilizar e importar a tu script php.

## Configuration

Dos forma de uso.

1. Configurar fichero /openerplib/openerplib.inc.php

```php
define('_OPENERPLIB_BD_', '');
define('_OPENERPLIB_UID_', 0);
define('_OPENERPLIB_PASSWD_', '');
define('_OPENERPLIB_URL_', 'http://<URL>/xmlrpc');
```

2. Configuración on-live.

```php
<?php
	$config = array(
		'bd'        => 'mybdname',
		'uid'       => 1212,
		'passwd'    => 'foo',
		'url'       => 'http://openerp/xmlrpc',
	);
	
	$open = new OpenERP($config);
?>
```

## Usage

### Creando la factoria de objetos OpenERP

```php
$open = new OpenERP();	// read config => openerlib.inc.php
```

### Leyendo objetos por id de objeto.

```php
// lee objecto res.partner con id 1 (solamente lee la propiedad 'id')
$p = $open->res_partner->get(1);
print $p->id;

// lee objecto res.partner con id 1 y algunas de sus propiedades
$p = $open->res_partner('name', 'active')->get(1);
print $p->id;
print $p->name . " ". $p->active;

$p = $open->res_partner(array('name', 'active'))->get(1);
print $p->id;
print $p->name . " ". $p->active;

// lee objecto res.partner con id 1, todos sus propiedades
$p = $open->res_partner('__ALL')->get(1);
print $p->id;
print $p->name . " ". $p->ref . " " . $p->vat;
```
    
### Navegando por objectos con many2one OpenERP
	
```php
$p = $open->res_partner('country')->get(1);
print $p->id;
print $p->country->id;	// many2one => res.country
print $p->country('name')->name;
```
	
### Navegando por objectos con one2many OpenERP

```php
$p = $open->res_partner('departament_ids')->get(1);
print "Departaments of " . $p->id; 
foreach($p->departament_ids('name', 'address_id') as $d)	// res.partner.departament
	print $d->name . " " . $d->address_id->id;
```
	
### Búsquedas


## Contacts

openerplib is written by:

* Benito Rodriguez

Para cualquier sugerencia, bugs,...

brarcos@gmail.com