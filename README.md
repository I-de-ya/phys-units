# Phys-Units

GNU Units-compatible library for Ruby.
Former name is [Quanty](http://narray.rubyforge.org/quanty/quanty-en.html),
the first Ruby units library released in 2001.

* [GitHub](https://github.com/masa16/phys-units)
* [RubyGems](https://rubygems.org/gems/phys-units)
* [Class Documentation](http://rubydoc.info/gems/phys-units/frames/)

## Installation

Install from gem as:

    $ gem install phys-units

Or install from source tree:

    $ ruby setup.rb

## Overview

### Phys::Quantity
is the primary class of Phys-Units library, intended to be manipulated by users.
This class represents Physical Quantities with a Unit of measurement.
It contains *Value* and *Unit*.

* *Value*
  must be a class instance having arithmetic methods,
  but it is not necessary to be a Numeric.
  This is a duck typing way.

        Phys::Quantity[2.5,"miles"].value  #=> 2.5

* *Unit*
  is an instance of Phys::Unit class obtained by parsing *expr* string.

        Phys::Quantity[2.5,"miles"].unit   #=> #<Phys::Unit 1609.344,{"m"=>1},@expr="5280 ft">

### Phys::Unit
is a class to represent Physical Units of measurement.
This class is used in the Phys::Quantity for calculations with Units,
and users do not always need to know its mechanism.
It has *Factor* and *Dimension*:

* *Factor* of the unit is a scale factor relative to its base unit.

        Phys::Unit["km"].factor #=> 1000

* *Dimension* of the unit
  is a hash table containing base units and dimensions as key-value pairs.

        Phys::Unit["N"].dimension #=> {"kg"=>1, "m"=>1, "s"=>-2}

### Examples

    require "phys/units"
    Q = Phys::Quantity
    U = Phys::Unit

    Q[1.23,'km'] + Q[4.56,'m']    #=> Phys::Quantity[1.23456,'km']
    Q[123,'mile'] / Q[2,'hr']     #=> Phys::Quantity[61,'mile/hr']
    Q[61,'miles/hr'].want('m/s')  #=> Phys::Quantity[27.26944,'m/s']
    Q[1.0,'are'] == Q[10,'m']**2  #=> true
    Q[70,'tempF'] + Q[10,'tempC'] #=> Phys::Quantity[88,'tempF']
    Q[20,'tempC'].want('tempF')   #=> Phys::Quantity[68,'tempF']
    Math.cos(Q[60,'degree'].to_f) #=> 0.5

    U["m/s"] === Q[1,'miles/hr']  #=> true

    case Q[1,"miles/hr"]
    when U["LENGTH"]
      puts "length"
    when U["TIME"]
      puts "time"
    when U["VELOCITY"]
      puts "velocity"
    else
      puts "other"
    end                    #=> "velocity"

## Features

Phys-Units library is discriminated from many other units libraries for Ruby,
by the following features:

* Compatible with GNU Units except nonlinear units.
* Provides 2331 units, 85 prefixes, including UTF-8 unit names.
* Defines Units by reading GNU Units text data,
  unlike other libraries which define Units in Ruby code.
* No addition or modification to Ruby standard classes,
  avoiding conflict with other libraries.
* Calculation of values is through Ruby Numeric arithmetic methods.
  Phys-Units does not care it.
* Conversion factors are internally held in Rational form even
  defined as the decimal form such as `1.0e10'.
* PI number has a dimension.
* Japanese Units are available by require 'phys/units/jp'.

## Platforms tested

* ruby 2.0.0p0 (2013-02-24 revision 39474) [x86_64-linux]

## Copying License

This program is free software.
You can distribute/modify this program
under the same terms as GPL3.
See "COPYING" file.
NO WARRANTY.

## Author

Masahiro TANAKA
