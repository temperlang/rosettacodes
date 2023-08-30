# rosettacodes

Some rosettacode.org problem implementations in Temper

Each example is in its own directory which has the rosettacode.org path so
rosettacode.org/wiki/Averages/Arithmetic_mean corresponds to the
sub-directory `Averages/Arithmetic_mean`

Each example should be imported by `config.temper.md` so that one
library definition can be used by `temper build` to compile them all.

TODO: A CI run that runs `temper build`

## Contributing

Just add a directory for your example following the convention above
and send a PR.

If you want to add a second implementation of an existing coding
problem just add another file to the same directory.
You'll probably need to name your exports slightly differently.

Feel free to take credit in the file commentary.
