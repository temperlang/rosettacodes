# Dense matrix math

This implementation uses a single array per matrix.

## Test

    test("multiply dense") {

Use test case from Rosetta Code. Ints also format more consistently.

      let a = new Dense([1.0, 2.0, 3.0, 4.0], 2);
      let b = new Dense([-3.0, -8.0, 3.0, -2.0, 1.0, 4.0], 2);
      let m = a.times(b).toString();

And actually check the string value because that's easier for now.

      assert(m == "-7.0, -6.0, 11.0\n-17.0, -20.0, 25.0");
    }

## Benchmark

Also provide a function for benchmarking matrix multiplication. Just keep the
running of it disabled by default. The dense matrix can more easily go larger
than the array-per-row version.

    // benchmarkDense(1e7.toIntUnsafe());
    export let benchmarkDense(nrows: Int): Void | Bubble {

Provide a lot of distinct small values for matrix content.

      let values = do {
        let values = new ListBuilder<Float64>();
        for (var i = 0; i < nrows; i += 1) {
          let x = i.toFloat64Unsafe();
          let addDiv(divisor: Float64): Void {
            values.add(((x / divisor) % 1.0) orelse 0.0) orelse void;
          }
          addDiv(3.0);
          addDiv(5.0);
          addDiv(7.0);
        }
        values.toList()
      };

And log our size for a record of it when running.

      console.log(values.length.toString());
      let middle = 3;
      let big = new Dense(values.toList(), (values.length / middle) orelse 0);

Here's the multiply.

      let product = big.times(new Dense([1.0, 1.0, 1.0], middle));

Sum the product for an easy way to check consistency across backends.

      let sum(values: Listed<Float64>): Float64 {
        values.reduceFrom(0.0) { (sum: Float64, x): Float64;; sum + x }
      }
      let total = sum(product.data);
      console.log(total.toString());
    }

## Implementation

    export class Dense(

Data has to be public in some fashion, or else you can't access from another
instance for multiplication.

      public data: List<Float64>,
      public nrows: Int,
    ) {
      public ncols: Int = (data.length / nrows) orelse 0;

      public times(b: Dense): Dense | Bubble {

For now, just flatten out flat matrices, but error on mismatch.

        if (nrows == 0 || b.ncols == 0) { return new Dense([], 0) }
        if (ncols != b.nrows) { bubble() }

And just do the triple loop. It would be nice to support capacity in
ListBuilder.

        let result = new ListBuilder<Float64>();
        for (var i = 0; i < nrows; i += 1) {
          for (var j = 0; j < b.ncols; j += 1) {
            var sum = 0.0;
            for (var k = 0; k < b.nrows; k += 1) {
              sum += this[i, k] * b[k, j];
            }
            result.add(sum);
          }
        }

Return is required here due to some compiler bug.

        return new Dense(result.toList(), nrows);
      }

Provide conveniences.

      public get(i: Int, j: Int): Float64 {
        data[ncols * i + j] orelse 0.0
      }

      public toString(): String {
        let builder = new StringBuilder();
        for (var i = 0; i < nrows; i += 1) {
          if (i > 0) {
            builder.append("\n");
          }
          for (var j = 0; j < ncols; j += 1) {
            if (j > 0) {
              builder.append(", ");
            }
            builder.append(this[i, j].toString());
          }
        }
        builder.toString()
      }
    }

## Imports

    let { StringBuilder } = import("std/strings");
