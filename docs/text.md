# Dumping the text of a page

The `shot-scraper text` command dumps out the final display text of a page (using innerText) after all JavaScript has run.

    shot-scraper text https://datasette.io/

Use `-o filename.text` to write the output to a file instead of displaying it.

    shot-scraper text https://datasette.io/ -o index.txt

Add `--javascript SCRIPT` to execute custom JavaScript before taking the HTML snapshot.

    shot-scraper text https://datasette.io/ \
      --javascript "document.querySelector('h1').innerText = 'Hello, world!'"

## Retrieving the HTML for a specific element

You can use the `-s SELECTOR` option to capture just the HTML for one specific element on the page, identified using a CSS selector:

    shot-scraper text https://datasette.io/ -s h2

This outputs:

    Exploratory data analysis                                                                                                                                                                          

## `shot-scraper html --help`

Full `--help` for this command:

<!-- [[[cog
import cog
from shot_scraper import cli
from click.testing import CliRunner
runner = CliRunner()
result = runner.invoke(cli.cli, ["text", "--help"])
help = result.output.replace("Usage: cli", "Usage: shot-scraper")
cog.out(
    "```\n{}\n```\n".format(help.strip())
)
]]] -->
```
Usage: shot-scraper text [OPTIONS] URL

  Output the final display text (using innerText) of the specified page

  Usage:

      shot-scraper text https://datasette.io/

  Use -o to specify a filename:

      shot-scraper text https://datasette.io/ -o index.txt

Options:
  -a, --auth FILENAME             Path to JSON authentication context file
  -o, --output FILE
  -j, --javascript TEXT           Execute this JS prior to saving the text
  -s, --selector TEXT             Return innerText of first element matching
                                  this CSS selector
  --wait INTEGER                  Wait this many milliseconds before taking
                                  the snapshot
  --log-console                   Write console.log() to stderr
  -b, --browser [chromium|firefox|webkit|chrome|chrome-beta]
                                  Which browser to use
  --browser-arg TEXT              Additional arguments to pass to the browser
  --user-agent TEXT               User-Agent header to use
  --fail                          Fail with an error code if a page returns an
                                  HTTP error
  --skip                          Skip pages that return HTTP errors
  --bypass-csp                    Bypass Content-Security-Policy
  --silent                        Do not output any messages
  --auth-password TEXT            Password for HTTP Basic authentication
  --auth-username TEXT            Username for HTTP Basic authentication
  --help                          Show this message and exit.
```
<!-- [[[end]]] -->
