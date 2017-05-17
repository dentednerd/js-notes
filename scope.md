# Scope
Compilation is the translation of code into language the computer can understand (machine code).

Started with binary, punch cards

Assembly code: a step up from binary

then things like Pascal and Cobol

Javascript is dynamically interpreted, not compiled -- processed whilst it's running, whereas a compiled code needs to be turned into machine code first

```javascript
var name = 'Joey';
function print (name) {
    console.log(name);
}
print('Chris');
// -> Chris
```
```javascript
var name = 'Joey';
function print (name) {
console.log(animal);
}
print ('Chris');
var animal = 'cat';
// undefined
```
```javascript
var name = 'Joey';
function print (name) {
console.log(animal);
}
print ('Chris');
// Reference Error
```
```javascript
var name = 'Joey';
function print (name) {
var animal = 'cat';
}
print ('Chris');
// Reference Error
```