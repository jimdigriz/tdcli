`tdcli` lets you pull data from your [TD Direct Investing](http://www.tddirectinvesting.co.uk/) account.

# Pre-flight

`tdcli` requires [Perl 5.14 or higher](https://www.perl.org/) and the following libraries:

 * [Config::Tiny](http://search.cpan.org/~rsavage/Config-Tiny/lib/Config/Tiny.pm)
 * [WWW::Mechanize](http://search.cpan.org/~ether/WWW-Mechanize/lib/WWW/Mechanize.pm)
 * [URI](http://search.cpan.org/~ether/URI/lib/URI.pm)
 * [JSON](http://search.cpan.org/~makamaka/JSON/lib/JSON.pm)

Start off by fetching the source which requires you to [have git installed on your workstation](http://git-scm.com/book/en/Getting-Started-Installing-Git):

    git clone https://github.com/jimdigriz/tdcli.git
    cd tdcli

## Debian 'wheezy' 7.x

    sudo apt-get update
    sudo apt-get install -yy --no-install-recommends perl libconfig-tiny-perl libwww-mechanize-perl liburi-perl libjson-perl

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

At the moment, if you just run the tool it will log you in and print out a list of your accounts:

    tdcli
