# Fizz Buzz

From rosettacode.org/wiki/FizzBuzz

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

`console.log` lets us output the message.
Instead of exporting any symbols, we just dump them all.
Loading this module has the effect of producing the desired
output.

      console.log(message);
    }
