# loc-badge-action

![Lines-of-Code Badge](https://github.com/MikhailEpatko/code-lines-counter-action/blob/image-data/loc-badge.svg)
![Hits-of-Code Badge](https://github.com/MikhailEpatko/loc-badge-action/blob/hoc-badge/hoc-badge.svg)

GitHub action to count lines in the files excluding blank lines.

## Example of usage GitHub action

In this version, you use [posix-egrep](https://www.gnu.org/software/findutils/manual/html_node/find_html/posix_002degrep-regular-expression-syntax.html)
 to pass a regular expression to the action to exclude or include file lines counts.

To install action copy the workflow code into
 a .github/workflows/main.yml file in your repository

```yaml
on: [push]

jobs:
  lines_counter_job:
    runs-on: ubuntu-latest
    name: A job to count lines of code and generate a badge
    steps:
      - uses: actions/checkout@v4
      - id: counting
        uses: ./                   # write the action name instead
        with:
          # Directories to scan. Default: current directory
          # For this option we can use multiline strings if we want to pass multiple values.
          # In this case it's an important detail that we used '|' or '|-' in the YAML. 
          scan-directories: |
            src
            .github
          # Do not count lines in files of thees directories. Default: .git
          # For this option we can use multiline strings if we want to pass multiple values.
          # In this case it's an important detail that we used '|' or '|-' in the YAML. 
          exclude-directories: |
            .idea
            .git
          # Badge output directory. Default: output
          output-directory: output
          # Output filename. Default: loc-badge.svg
          output-filename: loc-badge.svg
          # Rounding mode:
          #  I - integers
          #  K - up to thousands
          #  M - up to millions
          #  G - up to billions
          # Default value: I
          rounding: I
          # Available colors: <https://pypi.org/project/anybadge/>
          # Default value: green
          color: green

```

Use whatever tool you prefer to upload it somewhere.
