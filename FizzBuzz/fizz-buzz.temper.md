# Fizz Buzz

From https://rosettacode.org/wiki/FizzBuzz

    export let fizzBuzzInto(sink: fn (String): Void): Void {

Fizz buzz involves iterating over numbers from 1 to 100, inclusive, and
printing one of four kinds of messages.

- "FizzBuzz" when the number is evenly divisible by 3 and by 5.
- "Fizz" when it is evenly divisible by 3 but not 5.
- "Buzz" when it is evenly divisible by 5 but not 3.
- The decimal form of the number otherwise.

Within a loop, we use the `%` (remainder) operator to check
divisibility for the current number.

      for (var i = 1; i <= 100; ++i) {
        let divisibleByThree = (i % 3) == 0;
        let divisibleByFive =  (i % 5) == 0;
        let message: String = (

Everything in Temper is an expression, including `if`, so we can
focus on the values stored in `message` instead of repeatedly
assigning to it.

          if (divisibleByThree) {
            if (divisibleByFive) {
              "FizzBuzz"
            } else {
              "Fizz"
            }
          } else if (divisibleByFive) {
            "Buzz"
          } else {
            i.toString()
          }
        );

And instead of directly writing each message, we make this a generic report by
calling into the provided `sink` function.

        sink(message);
      }
    }

## Logging version

We can also make a support function that logs each message. The exact behavior
of `console.log` depends on the logging configuration for a particular backend.

    export let fizzBuzz(): Void {
      fizzBuzzInto { (message);; console.log(message); }
    }

## Test

When writing code as a library, it's also nice to automate testing of it. Here
we test some of the output values.

    test("some fizz and/or buzz") {

First prepare a place and store the messages, and insert an ignored value at
index 0, so we can use 1-based indexing to match the looping logic.

      let messages = new ListBuilder<String>();
      messages.add("ignore");
      fizzBuzzInto { (message);; messages.add(message) orelse void; }

Now check some values.

      assert(messages[1] == "1");
      assert(messages[6] == "Fizz");
      assert(messages[10] == "Buzz");
      assert(messages[15] == "FizzBuzz");
      assert(messages[100] == "Buzz");
    }
