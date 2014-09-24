flint
=====

flint is a advanced python client for 360 passivedns HTTP API.   
The associated web interface is http://www.passivedns.cn



## Usage

```
Usage: ./flint [<rrset>|<flinyrdara>] [<domain>|<ip>] [type] [options]
    ./flint rrset www.360.cn
    ./flint rdata 101.4.60.193 A
    ./flint rrset 360.cn -l 100
    ./flint rrset 360.cn --sort='time_first'


Options:
  -h, --help            show this help message and exit
  -v, --verbose
  -V, --version
  -j, --json            output in json format
  -l LIMIT, --limit=LIMIT
                        limit number of results. [default: 1000]
  -s SORT, --sort=SORT  time_last|time_first|count [default: time_last]
  -R, --reverse         reverse sort
  --before=BEFORE       only output results seen before this time
  --after=AFTER         only output results seen after this time
```

Some advanced features

* rrset support subdomain match
> flint rrset *.360.cn

* rdata support CIDR formatting
> flint rdata 106.120.167.66/24  

notice: the netmask must be >=24


## Basic Example

```
$ flint rrset 360.cn A

360.cn A In rrset
-------
Record times: 2014-08-06 20:39:07 -- 2014-09-06 13:37:52
Count: 522
360.cn  A   101.4.60.193

Record times: 2014-08-05 21:21:39 -- 2014-09-06 12:14:38
Count: 4637054
360.cn  A   106.120.167.66

Record times: 2014-08-05 21:21:23 -- 2014-09-06 12:06:11
Count: 1688982
360.cn  A   111.206.61.131
```

please notice: The output format is not yet completely compliant with the
[Passive DNS Common Output Format](http://tools.ietf.org/html/draft-dulaunoy-kaplan-passive-dns-cof-01).
But we plan to support that in the near future.

## Apply Access

Use this script to access 360 passivedns database, you must modify the script and assign the API address and API key
we allocated for you. How to apply a key? Please email passivedns@360.cn for more details.

