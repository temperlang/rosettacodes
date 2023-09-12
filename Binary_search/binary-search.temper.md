# Binary search

## Recursive

### Tests

    test("recursive") {

Binary search expects an ordered list.

      let nums = [-1, 0, 2, 15, 30, 100];

And we provide a comparator so we can operator on any type.

      let compareInts(a: Int, b: Int): Int { a - b }
      let findInt(value: Int): Int {

And provide -1 for missing in this context.

        binarySearchRecursive(nums, value, compareInts) orelse -1
      }

Check some found cases, including edges.

      assert(findInt(-1) == 0) { "wrong index" }
      assert(findInt(2) == 2) { "wrong index" }
      assert(findInt(100) == 5) { "wrong index:" }

Now check some missing cases, including past edges.

      assert(findInt(-2) == -1) { "expected missing" }
      assert(findInt(1) == -1) { "expected missing" }
      assert(findInt(101) == -1) { "expected missing" }

Callback block version has an error in TmpL:

      // let i = binarySearchRecursive(nums, 5) { (a: Int, b: Int);; a - b };

```plain
An operation is not implemented: Translate via value path.  Block/toplevel should handle translation as part of a declaration at TmpLTranslator.kt:1041
21: hRecursive(nums, 6) { (a: Int, b: Int);; a - b };
                        ┗━━━━━━━━━━━━━━━━━━━━━━━━━━┛
[-work//Binary_search/binary-search.temper.md+440-468]: Cannot translate An operation is not implemented: Translate via value path.  Block/toplevel should handle translation as part of a declaration: ❎
```

    }

### Implementation

We need an ordered list, a value to look for, and a way to compare values.

    export let binarySearchRecursive<T>(
      list: Listed<T>,
      value: T,
      compare: fn (T, T): Int,
    ): Int | Bubble {

Use an internal closure to recurse on edges while having access to main params.

      let search(lo: Int, hi: Int): Int | Bubble {

See if we ran out of options.

        if (hi < lo) { bubble() }

Otherwise compare the midpoint against our value. Temper int division truncates.

        let mid = (lo + hi) / 2;
        let comparison = compare(list[mid], value);

Pick which side we're on, or see if we have the exact value.

        if (comparison > 0) {
          search(lo, mid - 1)
        } else if (comparison < 0) {
          search(mid + 1, hi)
        } else {
          mid
        }
      }

Start with the whole list.

      search(0, list.length - 1)
    }
