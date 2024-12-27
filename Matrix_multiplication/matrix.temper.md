# Matrix math

## Test

    test("multiply") {

Use test case from Rosetta Code. Ints also format more consistently.

      let a = new Matrix([[1.0, 2.0], [3.0, 4.0]]);
      let b = new Matrix([[-3.0, -8.0, 3.0], [-2.0, 1.0, 4.0]]);
      let m = a.times(b).toString();

And actually check the string value because that's easier for now.

      assert(m == "-7.0, -6.0, 11.0\n-17.0, -20.0, 25.0");
    }

    blah();

    export let blah(): Void | Bubble {
      let values = do {
        let values = new ListBuilder<List<Float64>>();
        for (var i = 0; i < 1e7.toIntUnsafe(); i += 1) {
          let x = i.toFloat64Unsafe();
          let xyz = [x / 3.0, x / 5.0, x / 7.0].map { (x): Float64;;
            (x % 1.0) orelse 0.0
          };
          values.add(xyz);
        }
        values.toList()
      };
      console.log(values.length.toString());
      let big = new Matrix(values.toList());
      let product = big.times(new Matrix([[1.0], [1.0], [1.0]]));
      let sum(values: Listed<Float64>): Float64 {
        values.reduceFrom(0.0) { (sum: Float64, x): Float64;; sum + x }
      }
      let total = sum(product.data.map { (x): Float64;; x.getOr(0, 0.0) });
      console.log(total.toString());
    }

## Implementation

    export class Matrix(

Data has to be public in some fashion, or else you can't access from another
instance for multiplication.

      public data: List<List<Float64>>,
    ) {
      public times(b: Matrix): Matrix | Bubble {

For now, just flatten out flat matrices, but error on mismatch.

        if (nrows == 0 || b.ncols == 0) { return new Matrix([]) }
        if (ncols != b.nrows) { bubble() }

And just do the triple loop. It would be nice to support capacity in
ListBuilder.

        let result = new ListBuilder<ListBuilder<Float64>>();
        for (var i = 0; i < nrows; i += 1) {
          let row = new ListBuilder<Float64>();
          for (var j = 0; j < b.ncols; j += 1) {
            var sum = 0.0;
            for (var k = 0; k < b.nrows; k += 1) {
              sum += data[i][k] * b.data[k][j];
            }
            row.add(sum);
          }
          result.add(row);
        }

Return is required here due to some compiler bug.

        return new Matrix(result.map { (row): List<Float64>;; row.toList() });
      }

Provide conveniences.

      public get ncols(): Int {
        data[0].length orelse 0
      }

      public get nrows(): Int {
        data.length
      }

      public toString(): String {
        data.join("\n") { (row);; row.join(", ") { (it);; it.toString() } }
      }
    }
