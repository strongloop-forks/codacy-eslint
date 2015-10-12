Under the strict mode, this keywords outside of classes or class-like objects might be undefined and raise a TypeError.
This rule aims to flag usage of this keywords outside of classes or class-like objects.
Basically this rule checks whether or not a function which are containing this keywords is a constructor or a method.

```
/*eslint no-invalid-this: 2*/ /*eslint-env es6*/ this.a = 0;
/*error Unexpected `this`.*/ baz(() => this);
/*error Unexpected `this`.*/ (function() {
this.a = 0;
/*error Unexpected `this`.*/ baz(() => this);
/*error Unexpected `this`.*/ }
)();
function foo() {
this.a = 0;
/*error Unexpected `this`.*/ baz(() => this);
/*error Unexpected `this`.*/ }
var foo = function() {
this.a = 0;
/*error Unexpected `this`.*/ baz(() => this);
/*error Unexpected `this`.*/ }
;
foo(function() {
this.a = 0;
/*error Unexpected `this`.*/ baz(() => this);
/*error Unexpected `this`.*/ }
);
obj.foo = () => {
// `this` of arrow functions is the outer scope's. this.a = 0;
/*error Unexpected `this`.*/ }
;
var obj = {
aaa: function() {
return function foo() {
// There is in a method `aaa`, but `foo` is not a method. this.a = 0;
/*error Unexpected `this`.*/ baz(() => this);
/*error Unexpected `this`.*/ }
;
}
}
;
class Foo {
static foo() {
this.a = 0;
/*error Unexpected `this`.*/ baz(() => this);
/*error Unexpected `this`.*/ }
}
foo.forEach(function() {
this.a = 0;
/*error Unexpected `this`.*/ baz(() => this);
/*error Unexpected `this`.*/ }
);

```

[Source](http://eslint.org/docs/rules/no-invalid-this)