#EcasPhpCASParser

## Why
Default parsing of ECAS attributes is currently broken with phpCAS, 
groups end-up in an un-parsable concentaned string. 

## Installation

```
composer require ec-europa/ecas-phpcas-parser:dev-master
```

## Usage

```
//config the client client as usual
phpCAS::client(
    constant($config['cas.version']),
    $config['cas.host'],
    (int) $config['cas.port'],
    $config['cas.uri'],
    false
);

//set the attribute callback 
phpCAS::setCasAttributeParserCallback(
    array(
      new \EcasPhpCASParser\EcasPhpCASParser(),
      'parse'
    )
);

```
