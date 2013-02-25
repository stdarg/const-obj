# Introduction

A simple node.js module that recursively iterates over an object and make the properties
read-only. This is useful for values in objects that are to never change. This simple module
exports only two methods explained below.

# Installation

    $ npm install const-obj

# API

The following are exported from the const-obj module:

  - [makeObjConst()](#makeobjconstobjobject)
  - [makePropConst()](#makepropconstobjectobjectpropertystring)

## makeObjConst(obj:object)

  Recursively makes each property in the object and its sub-objects immutable. This function
  returns the object upon success and false upon failure.

## makePropConst(object:Object, property:String)

  Make a property immutable (assuring it cannot be changed from the current value).
  This operation cannot be un-done. This function returns the object on success and false
  on any failre.

# Examples

    var makeObjConst = require('const-obj').makeObjConst;
    var obj = {
        a: 111,
        b: '222',
        c: { d: 333 } };
    makeObjConst(obj);
    obj.a = 222;            // this is legal, but has no effect
    assert.ok(obj.a === 111);
    obj.b = 'Hmm';          // this is legal, but has no effect
    assert.ok(obj.b === '222');
    obj.c.d = true;
    assert.ok(obj.c.d === 333);

  The above code would not throw because the values cannot be changed. Also, assignments to the
  properties does not cause an error.

        var makePropConst = require('const-obj').makePropConst;
        var obj = { alpha: '0', beta: false };
        makePropConst(obj, 'alpha');
        obj.alpha = 678;
        assert.ok(obj.alpha === '0');
        obj.beta = true;
        assert.ok(obj.beta === true);

  The above code will not throw because the property set constant, cannot be changed.