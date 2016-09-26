<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [data type](#data-type)
- [declaration](#declaration)
  - [var](#var)
  - [let](#let)
  - [const](#const)
  - [destructuring](#destructuring)
    - [array destructuring](#array-destructuring)
    - [object destructuring](#object-destructuring)
    - [default value](#default-value)
  - [function declaration](#function-declaration)
- [interface](#interface)
  - [optional properties](#optional-properties)
  - [readonly properties](#readonly-properties)
  - [function type](#function-type)
  - [indexed type](#indexed-type)
  - [class type](#class-type)
    - [static and instance side class(confused)](#static-and-instance-side-classconfused)
  - [extending interface](#extending-interface)
  - [hybrid types](#hybrid-types)
  - [interface extending class](#interface-extending-class)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# data type

    // bolean
    let isDone: boolean = false;
    // number
    let decimal: number = 6;
    let hex: number = 0xf00d;
    let binary: number = 0b1010;
    let octal: number = 0o744;
    // string
    let color: string = "blue";
    color = 'red';
    // string template
    let fullName: string = `Bob Bobbington`;
    let age: number = 37;
    let sentence: string = `Hello, my name is ${ fullName }.
    I'll be ${ age + 1 } years old next month.`
    // array
    let list: number[] = [1, 2, 3];
    // tuple
    let x: [string, number];
    // Initialize it
    x = ["hello", 10]; // OK
    // enum
    enum Color {Red, Green, Blue};
    let c: Color = Color.Green;
    // any
    let notSure: any = 4;
    notSure = "maybe a string instead";
    notSure = false; // okay, definitely a boolean
    // void
    function warnUser(): void {
        alert("This is my warning message");
    }
    // null and undefine
    let u: undefined = undefined;
    let n: null = null;
    // never
    function error(message: string): never {
        throw new Error(message);
    }
    // type assertion
    let strLength: number = (someValue as string).length;

# declaration

## var

    for (var i = 0; i < 10; i++) {
        setTimeout(function() { console.log(i); }, 100 * i);
    }
    for (var i = 0; i < 10; i++) {
        // capture the current state of 'i'
        // by invoking a function with its current value
        (function(i) {
            setTimeout(function() { console.log(i); }, 100 * i);
        })(i);
    }

## let

    function f(input: boolean) {
        let a = 100;

        if (input) {
            // Still okay to reference 'a'
            let b = a + 1;
            return b;
        }

        // Error: 'b' doesn't exist here
        return b;
    }
    for (let i = 0; i < 10 ; i++) {
        setTimeout(function() {console.log(i); }, 100 * i);
    }

## const

    const numLivesForCat = 9;
    const kitty = {
        name: "Aurora",
        numLives: numLivesForCat,
    }

    // Error
    kitty = {
        name: "Danielle",
        numLives: numLivesForCat
    };

    // all "okay"
    kitty.name = "Rory";
    kitty.name = "Kitty";
    kitty.name = "Cat";
    kitty.numLives--;


## destructuring

### array destructuring

    let input = [1, 2];
    let [first, second] = input;
    console.log(first); // outputs 1
    console.log(second); // outputs 2

### object destructuring

    let o = {
        a: "foo",
        b: 12,
        c: "bar"
    }
    let {a, b} = o;

    let {a: newName1, b: newName2} = o;
    let {a, b}: {a: string, b: number} = o;

### default value

    function keepWholeObject(wholeObject: {a: string, b?: number}) {
        let {a, b = 1001} = wholeObject;
    }

## function declaration

    type C = {a: string, b?: number}
    function f({a, b}: C): void {
        // ...
    }

# interface

## optional properties

    interface SquareConfig {
        color?: string;
        width?: number;
    }

    function createSquare(config: SquareConfig): { color: string; area: number } {
        let newSquare = {color: "white", area: 100};
        if (config.color) {
            newSquare.color = config.color;
        }
        if (config.width) {
            newSquare.area = config.width * config.width;
        }
        return newSquare;
    }

    let mySquare = createSquare({color: "black"});

## readonly properties

    interface Point {
        readonly x: number;
        readonly y: number;
    }
    let p1: Point = { x: 10, y: 20 };
    p1.x = 5; // error!

## function type

    interface SearchFunc {
        (source: string, subString: string): boolean;
    }
    let mySearch: SearchFunc;
    mySearch = function(src: string, sub: string): boolean {
        let result = src.search(sub);
        if (result == -1) {
            return false;
        }
        else {
            return true;
        }
    }

## indexed type

    interface StringArray {
        [index: number]: string;
    }
    let myArray: StringArray;
    myArray = ["Bob", "Fred"];
    let myStr: string = myArray[0];
    // readonly
    interface ReadonlyStringArray {
        readonly [index: number]: string;
    }
    let myArray: ReadonlyStringArray = ["Alice", "Bob"];
    myArray[2] = "Mallory"; // error!

## class type

    interface ClockInterface {
        currentTime: Date;
        setTime(d: Date);
    }

    class Clock implements ClockInterface {
        currentTime: Date;
        setTime(d: Date) {
            this.currentTime = d;
        }
        constructor(h: number, m: number) { }
    }

### static and instance side class(confused)

    interface ClockConstructor {
        new (hour: number, minute: number): ClockInterface;
    }
    interface ClockInterface {
        tick();
    }

    function createClock(ctor: ClockConstructor, hour: number, minute: number): ClockInterface {
        return new ctor(hour, minute);
    }

    class DigitalClock implements ClockInterface {
        constructor(h: number, m: number) { }
        tick() {
            console.log("beep beep");
        }
    }
    class AnalogClock implements ClockInterface {
        constructor(h: number, m: number) { }
        tick() {
            console.log("tick tock");
        }
    }

    let digital = createClock(DigitalClock, 12, 17);
    let analog = createClock(AnalogClock, 7, 32);

## extending interface

    interface Shape {
        color: string;
    }

    interface PenStroke {
        penWidth: number;
    }

    interface Square extends Shape, PenStroke {
        sideLength: number;
    }

    let square = <Square>{};
    square.color = "blue";
    square.sideLength = 10;
    square.penWidth = 5.0;

## hybrid types

    interface Counter {
        (start: number): string;
        interval: number;
        reset(): void;
    }

    function getCounter(): Counter {
        let counter = <Counter>function (start: number) { };
        counter.interval = 123;
        counter.reset = function () { };
        return counter;
    }

    let c = getCounter();
    c(10);
    c.reset();
    c.interval = 5.0;

## interface extending class

    class Control {
        private state: any;
    }

    interface SelectableControl extends Control {
        select(): void;
    }

    class Button extends Control {
        select() { }
    }

    class TextBox extends Control {
        select() { }
    }

    class Image extends Control {
    }

    class Location {
        select() { }
    }
    // Button and TextBox can access state while Image and Location not