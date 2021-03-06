`tdcli` lets you export transactions from your [TD Direct Investing](http://www.tddirectinvesting.co.uk/) account.

## Issues

 * fixup stock symbols properly (not just wholesale prepending of `LON:`)
 * requires a 100x as TD exports pounds, Google finance imports pence
 * prompt for password

# Pre-flight

`tdcli` requires [Perl 5.14 or higher](https://www.perl.org/) and the following libraries:

 * [Config::Tiny](http://search.cpan.org/~rsavage/Config-Tiny/lib/Config/Tiny.pm)
 * [WWW::Mechanize](http://search.cpan.org/~ether/WWW-Mechanize/lib/WWW/Mechanize.pm)
 * [URI](http://search.cpan.org/~ether/URI/lib/URI.pm)
 * [JSON](http://search.cpan.org/~makamaka/JSON/lib/JSON.pm)
 * [Date::Calc](http://search.cpan.org/~stbey/Date-Calc/lib/Date/Calc.pod)
 * [Text::CSV](http://search.cpan.org/~makamaka/Text-CSV/lib/Text/CSV.pm)
 * [HTML::Parser](http://search.cpan.org/dist/HTML-Parser/Parser.pm)

Start off by fetching the source which requires you to [have git installed on your workstation](http://git-scm.com/book/en/Getting-Started-Installing-Git):

    git clone https://github.com/jimdigriz/tdcli.git
    cd tdcli

## Debian

    sudo apt-get update
    sudo apt-get install -yy --no-install-recommends perl libconfig-tiny-perl libwww-mechanize-perl liburi-perl libjson-perl libdate-calc-perl libtext-csv-perl libhtml-parser-perl

# Configuration

You need to create a configuration file with your account details in it:

    mkdir ~/.tdcli
    chmod 0700 ~/.tdcli
    
    cp example.config ~/.tdcli/config
    chmod 0600 ~/.tdcli/config

Now edit the file `~/.tdcli/config`:

 * **`debug` [optional]:** if set to anything (not commented out) then the HTTP requests will be printed to `STDERR`
 * **`from` [optional]:** include your e-mail address in the HTTP requests made
 * **`user`:** your login
 * **`pass`:** your password
 * **`stepup` section:** your memorable word, year and place goes here which is used to authenticate you from a new workstation

**N.B.** after running this tool, you will find `acct` is added, you should not edit this

# Usage

Just running the tool with no parameters will list your accounts:

    $ ./tdcli
    Accounts (01234567890):
     * 1234567 {ISA}: isa
     * 0987654 {TRADING}: trading

To download a copy of your transactions you can use (this can take minutes to complete!):

    $ ./tdcli -a 1234567 -T -f 2013-01-01 -t 2015-04-01 | tee transactions.csv

**N.B.** periods longer than 18 months *are* supported

The tool has some basic built in help to show and explain its functionality:

    $ ./tdcli --help
    ./tdcli version 0.1 calling Getopt::Std::getopts (version 1.06),
    running under Perl version 5.14.2.
    Usage: ./tdcli [ -h | -v | -a 1234 [ -P | -T [ -f YYYY-MM-DD ] [ -t YYYY-MM-DD ] ] ]
    Export transactions from your TD Direct Investing account.
    
      -a ID                    select account number
    
      -P                       output CSV of portfolio
    
      -T                       output CSV of transactions
      -f YYYY-MM-DD            transactions from date (default: first of current month)
      -t YYYY-MM-DD            transactions until date (default: today)
    
      --help                   display this help and exit
      --version                output version information and exit
