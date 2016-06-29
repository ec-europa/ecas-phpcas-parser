#EcasPhpCASParser

## Why
Default parsing of ECAS attributes is currently broken with phpCAS, 
groups end-up in an un-parsable concentaned string. 

### before
```
array (size=21)
  'user' => string 'gboddin' (length=7)
  'departmentNumber' => string 'xxxx' (length=13)
  'email' => string 'xxx' (length=31)
  'employeeNumber' => string 'xxx' (length=8)
  'employeeType' => string 'x' (length=1)
  'firstName' => string 'Gregory' (length=7)
  'lastName' => string 'BODDIN' (length=6)
  'domain' => string 'xxxxx' (length=12)
  'domainUsername' => string 'gboddin' (length=7)
  'telephoneNumber' => string 'xxx' (length=5)
  'locale' => string 'en' (length=2)
  'assuranceLevel' => string 'xx' (length=2)
  'uid' => string 'gboddin' (length=7)
  'orgId' => string 'xxxx' (length=6)
  'groups' => string 'GROUP1GROUP2GROUP3GROUP4GROUP5' (length=28)
  'strength' => string 'STRONG' (length=6)
  'authenticationFactors' => "xxxxgboddin"
  'loginDate' => string '2016-06-29T10:53:06.399+02:00' (length=29)
  'sso' => string 'true' (length=4)
  'ticketType' => string 'SERVICE' (length=7)
```
### after
```
array (size=21)
  'user' => string 'gboddin' (length=7)
  'departmentNumber' => string 'xxxx' (length=13)
  'email' => string 'xxx' (length=31)
  'employeeNumber' => string 'xxx' (length=8)
  'employeeType' => string 'x' (length=1)
  'firstName' => string 'Gregory' (length=7)
  'lastName' => string 'BODDIN' (length=6)
  'domain' => string 'xxxxx' (length=12)
  'domainUsername' => string 'gboddin' (length=7)
  'telephoneNumber' => string 'xxx' (length=5)
  'locale' => string 'en' (length=2)
  'assuranceLevel' => string 'xx' (length=2)
  'uid' => string 'gboddin' (length=7)
  'orgId' => string 'xxxx' (length=6)
  'groups' => 
    array (size=18)
      0 => string 'GROUP1' (length=6)
      1 => string 'GROUP2' (length=6)
      2 => string 'GROUP3' (length=6)
      3 => string 'GROUP4' (length=6)
      4 => string 'GROUP5' (length=6)
  'strength' => string 'STRONG' (length=6)
  'loginDate' => string '2016-06-29T10:53:06.399+02:00' (length=29)
  'authenticationFactors' => 
      array (size=1)
        'password' => string 'gboddin' (length=7)
        'sms' => string 'xxxxxxx' (length=7)
  'sso' => string 'true' (length=4)
  'ticketType' => string 'SERVICE' (length=7)
```
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

## ECAS auth success XML example :
```
<cas:authenticationSuccess>
	<cas:user>gboddin</cas:user>
	<cas:groups number="2">
		<cas:group>GROUP1</cas:group>
		<cas:group>GROUP1</cas:group>
	</cas:groups>
	<cas:ticketType>SERVICE</cas:ticketType>
        <!-- and so on ... -->
</cas:authenticationSuccess>
```
