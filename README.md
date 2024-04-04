# rosettacodes

Some rosettacode.org problem implementations in Temper

Each example is in its own directory which has the rosettacode.org path so
rosettacode.org/wiki/Averages/Arithmetic_mean corresponds to the
sub-directory `Averages/Arithmetic_mean`

Each example should be imported by `config.temper.md` so that one
library definition can be used by `temper build` to compile them all.

TODO: A CI run that runs `temper build`

## Translations

If you translate an example from another language, please ensure the source
`*.temper.md` file includes the URL of the original and the source code in a fenced
code block.

``````markdown
<details><summary>This Temper code was adapted from https://url/to/original</summary>

```py
original source code in a fenced code block
```

</details>
``````

## Contributing

Just add a directory for your example following the convention above
and send a PR.

If you want to add a second implementation of an existing coding
problem just add another file to the same directory.
You'll probably need to name your exports slightly differently.

Feel free to take credit in the file commentary.
