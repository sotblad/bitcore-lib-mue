# Unit

Unit is a utility for handling and converting bitcoin units. We strongly recommend to always use satoshis to represent amount inside your application and only convert them to other units in the front-end.

To understand the need of using the `Unit` class when dealing with unit conversions, see this example:

```javascript
> 81.99 * 100000 // wrong
8198999.999999999
> var bitcore = require('bitcore');
> var Unit = bitcore.Unit;
> Unit.fromMilis(81.99).toSatoshis() // correct
8199000
```

## Supported units

The supported units are MUE, mMUE, bits (micro MUEs, uMUE) and satoshis. The codes for each unit can be found as members of the Unit class.

```javascript
var mueCode = Unit.MUE;
var mmueCode = Unit.mMUE;
var umueCode = Unit.uMUE;
var bitsCode = Unit.bits;
var satsCode = Unit.satoshis;
```

## Creating units

There are two ways for creating a unit instance. You can instantiate the class using a value and a unit code; alternatively if the unit it's fixed you could you some of the static methods. Check some examples below:

```javascript
var unit;
var amount = 100;

// using a unit code
var unitPreference = Unit.MUE;
unit = new Unit(amount, unitPreference);

// using a known unit
unit = Unit.fromMUE(amount);
unit = Unit.fromMilis(amount);
unit = Unit.fromBits(amount);
unit = Unit.fromSatoshis(amount);
```

## Conversion

Once you have a unit instance, you can check its representation in all the available units. For your convenience the classes expose three ways to accomplish this. Using the `.to(unitCode)` method, using a fixed unit like `.toSatoshis()` or by using the accessors.

```javascript
var unit;

// using a unit code
var unitPreference = Unit.MUE;
value = Unit.fromSatoshis(amount).to(unitPreference);

// using a known unit
value = Unit.fromMUE(amount).toMUE();
value = Unit.fromMUE(amount).toMilis();
value = Unit.fromMUE(amount).toBits();
value = Unit.fromMUE(amount).toSatoshis();

// using accessors
value = Unit.fromMUE(amount).MUE;
value = Unit.fromMUE(amount).mMUE;
value = Unit.fromMUE(amount).bits;
value = Unit.fromMUE(amount).satoshis;
```

## Using a fiat currency

The unit class also provides a convenient alternative to create an instance from a fiat amount and the corresponding MUE/fiat exchange rate. Any unit instance can be converted to a fiat amount by providing the current exchange rate. Check the example below:

```javascript
var unit, fiat;
var amount = 100;
var exchangeRate = 350;

unit = new Unit(amount, exchangeRate);
unit = Unit.fromFiat(amount, exchangeRate);

fiat = Unit.fromBits(amount).atRate(exchangeRate);
fiat = Unit.fromBits(amount).to(exchangeRate);
```
