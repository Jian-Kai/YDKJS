# 🌜  Lexical-this 🌛 #

## arrow function ##

    var foo = a => {
        console.log( a );
    };

    foo( 2 ); // 2

> More important going on with arrow-functions

    var obj = {
        id: "awesome",
        cool: function coolFn() {
            console.log( this.id );
        }
    };

    var id = "not awesome";

    obj.cool(); // awesome

    setTimeout( obj.cool, 100 ); // not awesome

- `var self = this;` is the answer.

        var obj = {
            count: 0,
            cool: function coolFn() {
                var self = this;

                if (self.count < 1) {
                    setTimeout( function timer(){
                        self.count++;
                        console.log( "awesome?" );
                    }, 100 );
                }
            }
        };

        obj.cool(); // awesome?

- Arrow function 

        var obj = {
            count: 0,
            cool: function coolFn() {
                if (this.count < 1) {
                    setTimeout( () => { 
                        this.count++;
                        console.log( "awesome?" );
                    }, 100 );
                }
            }
        };

        obj.cool(); // awesome?


> The `arrow-function` doesn't get its `this` unbound in some unpredictable way, it just `"inherits"` the `this` binding of the `cool() function `

>which is to confuse and conflate "this binding" rules with "lexical scope" rules.

- `bind(this)`

> use and embrace the `this mechanism` correctly.

        var obj = {
            count: 0,
            cool: function coolFn() {
                if (this.count < 1) {
                    setTimeout( function timer(){
                        this.count++; // `this` is safe because of `bind(..)`
                        console.log( "more awesome" );
                    }.bind( this ), 100 ); // look, `bind()`!
                }
            }
        };

        obj.cool(); // more awesome