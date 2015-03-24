`tdcli` lets you pull data from your [TD Direct Investing](http://www.tddirectinvesting.co.uk/) account.

# Pre-flight

`tdcli` requires [Perl 5.14 or higher](https://www.perl.org/) and the following libraries:

 * [Config::Tiny](http://search.cpan.org/~rsavage/Config-Tiny/lib/Config/Tiny.pm)
 * [WWW::Mechanize](http://search.cpan.org/~ether/WWW-Mechanize/lib/WWW/Mechanize.pm)
 * [URI](http://search.cpan.org/~ether/URI/lib/URI.pm)
 * [JSON](http://search.cpan.org/~makamaka/JSON/lib/JSON.pm)
 * [Date::Parse](http://search.cpan.org/~gbarr/TimeDate/lib/Date/Parse.pm)

Start off by fetching the source which requires you to [have git installed on your workstation](http://git-scm.com/book/en/Getting-Started-Installing-Git):

    git clone https://github.com/jimdigriz/tdcli.git
    cd tdcli

## Debian 'wheezy' 7.x

    sudo apt-get update
    sudo apt-get install -yy --no-install-recommends perl libconfig-tiny-perl libwww-mechanize-perl liburi-perl libjson-perl libtimedate-perl

# Configuration

You need to create a configuration file with your account details in it:

    mkdir ~/.tdcli
    chmod 0700 ~/.tdcli
    
    cp example.config ~/.tdcli
    chmod 0600 ~/.tdcli

Now edit the file:

 * **`debug`:** if set to anything (not commented out) then the HTTP requests will be printed to `STDERR`
 * **`from`:** optionally include your e-mail address in the HTTP requests made
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

The tool has some basic built in help to show its other functionality:

    $ ./tdcli --help
    Usage: tdcli [ -a 1234 [ -p | -t [ -f YYYY-MM-DD ] [ -t YYYY-MM-DD ] ] ]
    Pull data from your TD Direct Investing account.
    
      -a ID                    select account number
      -p                       show portfolio
      -t                       list transactions
      -f YYYY-MM-DD            from date (default: 1st of current month)
      -t YYYY-MM-DD            to date (default: today)
