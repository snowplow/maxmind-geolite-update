# maxmind-geolite-update

## Overview

A Python script to regularly update the free MaxMind geo databases. Closely based on Boris from MaxMind's [Perl script] [perlscript] to accomplish the same.

## Installing

Grab the whole repo down and link the Python file into your path:

    git clone git@github.com:psychicbazaar/maxmind-geolite-update.git
    cd maxmind-geolite-update
    sudo ln s ./maxmind-geolite-update.py /usr/bin/local/maxmind-geolite-update

Git should preserve the script's execute permission. If it doesn't:

    chmod +x ./maxmind-geolite-update.py

## Configuring

By default maxmind-geolite-update reads the `config.cfg` configuration file in the same folder. Update its contents as required:

    [Local]
    download-dir: /usr/local/share/GeoIP/download
    destination-dir: /usr/local/share/GeoIP 

If you subscribe to the commercial MaxMind GeoIP Country database and/or GeoIPCity database, then make sure to comment out the first two lines in the `[Files]` section, to avoid clashing with MaxMind's `ipupdate` tool:

    [Files]
    ; GeoIP.dat.gz: GeoLiteCountry/GeoIP.dat.gz ; DELETE this line if you are a subscriber
    ; GeoIPCity.dat.gz: GeoLiteCity.dat.gz ; DELETE this line if you are a subscriber.

If you want to change the path for the configuration file, you can specify this on the command line like so:

    ./maxmind-geolite-update.py --config=~/maxmind.cfg

## Scheduling

Assuming you're using the excellent [cronic] [cronic] as a wrapper for your cronjobs, add the following to your crontab:

    34 15 * * * cronic /usr/local/bin/maxmind-geolite-update

This will check the MaxMind server daily for new files.

[perlscript]: http://forum.maxmind.com/viewtopic.php?f=13&t=1453
[cronic]: http://habilis.net/cronic/

## License

Copyright (C) 2012 Psychic Bazaar Ltd

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
