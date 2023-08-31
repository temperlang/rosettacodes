# Greatest common divisor

## Test

    test("positive and negative values") {

Try out the example from Rosetta Code.

      assert(gcd([57, 0, -45, -18, 90, 447]) == 3) { "bad result" }

And also a simpler one of our own.

      assert(gcd([12, 18]) == 6) { "bad result" }

Also cases of pure 0.

      assert((gcd([0, 0, 0]) orelse -1) == -1) { "bad success" }

    }

## Implementation

    export let gcd(nums: Listed<Int>): Int | NoResult {

Greatest is always positive .

      var result = abs(nums[0]);

      for (var i = 1; i < nums.length; i += 1) {
        var next = abs(nums[i]);

Loop until we have something perfectly divided.

        while (result != 0 && next != 0) {
          if (result > next) {
            result %= next;
          } else {
            next %= result;
          }
        }

Now one of them is 0, and the other is the gcd. We could explicitly check for
that or even use `max`, but because 0, addition is equivalent here.

        result += next;
      }

But check first for 0 before we provide the result, because all 0 is undefined.

      if (result == 0) { fail() }
      result
    }

Temper doesn't yet have `abs`, so implement it here.

    let abs(i: Int): Int {
      if (i < 0) { -i } else { i }
    }
