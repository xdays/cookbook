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
