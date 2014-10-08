flint
=====

flint is a advanced python client for 360 passivedns HTTP API.   
The associated web interface is http://www.passivedns.cn


## basic rrset query example
=======

```
$ flint rrset 360.cn A
360.cn A In rrset
-------
Record times: 2014-08-05 15:21:23 -- 2014-09-23 12:39:22
Count: 1793790
360.cn  A       111.206.61.131

Record times: 2014-08-06 14:39:07 -- 2014-09-23 11:31:12
Count: 801
360.cn  A       101.4.60.193

Record times: 2014-08-05 15:21:39 -- 2014-09-23 11:24:23
Count: 4758929
360.cn  A       106.120.167.66


>>> All Done
```

## basic rdata query example

```
$ flint rdata 101.4.60.193
101.4.60.193 All Type In rdata
--------
360.cn          101.4.60.193    2014-09-23 11:31:12
www.360.cn      101.4.60.193    2014-09-23 10:20:28

>>> All Done
```

## Usage

```
Usage: ./flint [<rrset>|<rdata>] [<domain>|<ip>] [type] [options]
    ./flint rrset www.360.cn
    ./flint rdata 101.4.60.193 A
    ./flint rrset 360.cn -l 100
    ./flint rrset 360.cn --sort='time_first'
    ./flint rrset 360.cn --before='2014-10-01' --after='2014-08-01 13:12:21'


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

rrset and rdata support some advanced grammer in use

#### rrset
subdomain match
>flint rrset *.360.cn


sort
>flint rrset 360.cn -s count

  sort filed support: time_first, time_last, count

reverse sort
>flint rrset 360.cn -s count -R

filter as first_seen and last_seen
>flint rrset 360.cn --before='2014-10-01' --after='2014-08-01 13:12:21'

before and after support three date format: 

  * 2014-08-01
  * 2014-08-01 13:12:21
  * 1408107600 (utc timestamp)

#### rdata
CIDR formatting
>flint rdata 106.120.167.66/24  

the netmask must be >=24



## How to run this script

Use this script to access 360 passivedns database, you must apply an api authentication key first.

1. Email passivedns@360.cn to apply the API_ID & API_KEY
2. Modify the flint.conf use the API_KEY and API_ID we allocate for you
3. Copy flint.conf to ~/.flint.conf or /etc/flint.conf



