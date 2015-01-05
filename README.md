# Chameleon Crawler

Browser automation for [Chameleon](https://github.com/ghostwords/chameleon).


## Setup

- Install Chromium, chromedriver, python3 and xvfb. On Ubuntu:
```
sudo apt-get install chromium-browser chromium-chromedriver python3 xvfb
```

- Install the project's Python dependencies (documented in [requirements.txt](requirements.txt)). You might do this with `virtualenv` and `pip`, or maybe Docker. Note this is a Python 3 project.

- Make sure `chromedriver` is in your $PATH. It's not on Ubuntu, so we have to fix that:
```
sudo ln -s /usr/lib/chromium-browser/chromedriver /usr/local/bin/chromedriver
```

- If using Ubuntu 14.04, [fix chromedriver's shared libraries error](http://stackoverflow.com/questions/25695299/chromedriver-on-ubuntu-14-04-error-while-loading-shared-libraries-libui-base):
```
echo "/usr/lib/chromium-browser/libs" | sudo tee --append /etc/ld.so.conf.d/chrome_lib.conf >/dev/null
sudo ldconfig
```

- Finally, generate a Chameleon CRX package [by following development setup steps 1 and 4 in Chameleon's checkout](https://github.com/ghostwords/chameleon#development-setup).


## Usage

Run `./src/run.py /path/to/chameleon.crx` to perform a crawl, or `./src/run.py -h` to see the optional arguments:

```
$ ./src/run.py -h
usage: run.py [-h] [-n {1,2,3,4,5,6,7,8}] [--headless | --no-headless]
              [-t SECONDS] [--urls URL_FILE_PATH]
              CHAMELEON_CRX_FILE_PATH

positional arguments:
  CHAMELEON_CRX_FILE_PATH
                        path to Chameleon CRX package

optional arguments:
  -h, --help            show this help message and exit
  -n {1,2,3,4,5,6,7,8}  parallel browser processes to use (default: 2)
  --headless            use a virtual display (default)
  --no-headless
  -t SECONDS, --timeout SECONDS
                        seconds to wait for pages to finish before timing out
                        (default: 20)
  --urls URL_FILE_PATH  path to URL list file (default: urls.txt)
```

## Roadmap

1. Save results to SQLite.
2. Compile list of URLs.
3. Crawl URLs, manually analyze results to flag fingerprinters.
4. Tweak the heuristic to minimize false negatives/positives.


## Code license

Mozilla Public License Version 2.0
