# Arithmetic mean

The arithmetic mean is the un-weighted middle point of the samples.

    test("meanOfThreeNums") {
      assert(mean([1.0, 2.0, 3.0] == 2.0));
    }

Unlike the median, the mean of an even sized list is not necessarily
in the list.

    test("meanNotMedian") {
      assert(mean([1.0, 1.0, 1.0, 100.0]) == 25.75);
    }

The `mean` function takes some samples as a list of floats and returns
the arithmetic mean, also as a float.

    export let mean(samples: List<Float64>): Float64 {
      let n = samples.length;

We need to avoid dividing by zero.  Somewhat arbitrarily, the average
of zero samples is the additive identity.

      if (n == 0) { return 0.0; }

First, we just sum the samples.  Then we divide by the count of
samples.

      var sum = 0.0;
      for (var i = 0; i < n; ++i) {
        sum += samples.getOr(i, 0.0);
      }

      // We need to convert n to a float explicitly.
      sum / n.toFloat64()
    }
