# 🌜  Dynamic Scope 🌛 #

## Dynamic Scope v.s. Lexical Scope ##

> - `Dynamic scope` : Where they are called from.
> - `Lexical Scope` : Look-up a variable and where it will find it.

### Here is an example of Dynamic Scope ###

        function foo() {
            console.log( a ); // What will console.log be?
        }

        function bar() {
            var a = 3;
            foo();
        }

        var a = 2;

        bar();

    Scope Chain is based on the `call-stack`, not the nesting of scopes in code.

### Scope Chain ###

        function foo() {
            console.log( a );  
        }

        function bar() {  
            var a = 3;
            foo();
        }

        var a = 2;

        bar();  

    `Global/Window` ➡️ `bar()` ➡️  `foo()` ➡️ `console.log(a)`  

    > Related Work :
    > [NCCU Programming Languages (Page.36)](http://www.cs.nccu.edu.tw/~chenk/Courses/PL/Lectures/PL-Lect-5-S06.pdf)

### How about Lexical Scope ###

        function foo() {
            console.log( a ); // What will console.log be?
        }

        function bar() {
            var a = 3;
            foo();
        }

        var a = 2;

        bar();
    `RHS reference` to a in foo() will be resolved to the global variable a , which will result in value 2 being output.

## Dynamic Scope v.s. `this` ##

> `Dynamic Scope` actually is a near cousin to another mechanism [` this `](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/this) in JavaScript .

### `this` in Global/Window or Scope ###

        console.log(this);
        console.log(this === Window);
        function foo(){
            console.log(this === Window);
        }
        var a = 3
        foo.bind(a)();

        var boo = {
            b : 2,
            fun : function(){
                console.log(this);
            },
            bo: this
        }
        boo.fun();

    `this` in object will point to objcet.

    `this` in function will point to Global/Window.

### use `this` to realize Dynamic Scope ###

        function foo() {
            console.log(this.a);
        }

        var bar = {
            a: 3,
            foofn: function() {
                foo.bind(this)();
            }
        };

        var a = 2;

        bar.foofn();

    > `this` in bar will point to bar.
