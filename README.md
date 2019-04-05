# Distibition-Check Version 0.2

This is a simple python script that checks a set of samples against more than 80
different distributions. See also
[www.aizac.info](http://www.aizac.info/simple-check-of-a-sample-against-80-distributions)
for more information.

## Requirements

* python 2.x or 3.x
* scipy
* joblib
* multiprocessing
* optparse
* and matplotlib

## Usage

Getting help:

```bash
$ python distribution_check.py --help
Usage: distribution-check.py [options]

Options:
  -h, --help            show this help message and exit
  -f FILE, --file=FILE  file with measurement data
  -v, --verbose         print all results immediately (default=False)
  -t TOP, --top=TOP     define amount of printed results (default=10)
  -p, --plot            plot the best result with matplotlib (default=False)
  -i ITERATIVE, --iterative=ITERATIVE
                        define number of iterative checks (default=1)
  -e EXCLUDE, --exclude=EXCLUDE
                        amount (in per cent) of exluded samples for each
                        iteration (default=10.0%)
  -n PROCESSES, --processes=PROCESSES
                        number of process used in parallel (default=1)
  -d, --densities       
  -g, --generate        generate an example file
```

An example file can be generated with the parameter `--generate`, it can be
tested afterwards with:

```bash
$ python3 distribution-check.py --file example-mielke.dat -i 1
reading data in file example-mielke.dat ... done
-------------------------------------------------------------------
Top 10 after 1 iteration(s)
-------------------------------------------------------------------
1    burr               p:  0.9890397036552685  D:  0.028114675350879414
2    mielke             p:  0.9890320941020523  D:  0.028116374302027514
3    ncf                p:  0.945997286512634   D:  0.03317887016083887
4    invgauss           p:  0.9192697203205987  D:  0.035005720645224
5    betaprime          p:  0.9170742596219682  D:  0.035139708447065376
6    f                  p:  0.917074235303842   D:  0.03513970992067561
7    lognorm            p:  0.9129036562067222  D:  0.03538916720361518
8    johnsonsu          p:  0.9011083690817155  D:  0.03606299467619778
9    powerlognorm       p:  0.8833927058902763  D:  0.0370040983598684
10   johnsonsb          p:  0.8809096890336684  D:  0.037130410098832
```

The mielke is only on the 2nd place. Since the applied "Kolmogorov-Smirnof one
sided test" is applied, which itself uses random generated values, the result
can be further relativized by a couple of iterations.

``` bash
$ python distribution_check.py --file example-mielke.dat -i 50
reading data in file example-mielke.dat ... done
-------------------------------------------------------------------
Top 10 after 50 iteration(s)
-------------------------------------------------------------------
1    mielke        p: 0.99249..  D: 0.02854..  var(p): 0.00028..  var(D): 1.167..e-05
2    burr          p: 0.99248..  D: 0.02853..  var(p): 0.00028..  var(D): 1.168..e-05
3    betaprime     p: 0.90766..  D: 0.03783..  var(p): 0.00352..  var(D): 1.501..e-05
4    f             p: 0.90766..  D: 0.03783..  var(p): 0.00352..  var(D): 1.501..e-05
5    invgauss      p: 0.90548..  D: 0.03800..  var(p): 0.00470..  var(D): 1.625..e-05
6    powerlognorm  p: 0.89967..  D: 0.03854..  var(p): 0.00499..  var(D): 1.764..e-05
7    lognorm       p: 0.89610..  D: 0.03794..  var(p): 0.00387..  var(D): 1.488..e-05
8    johnsonsu     p: 0.89355..  D: 0.03831..  var(p): 0.00395..  var(D): 1.481..e-05
9    johnsonsb     p: 0.89339..  D: 0.03854..  var(p): 0.00350..  var(D): 1.261..e-05
10   exponweib     p: 0.84332..  D: 0.04090..  var(p): 0.00594..  var(D): 1.700..e-05
```

The last two values represent the variance of the `p` and `D` value, their
thightness can also be used as an indicator vor the averaged values (of `p` and
`D`), the smaller the variance the more accurate should be the result.

Check out the other paramters ...
