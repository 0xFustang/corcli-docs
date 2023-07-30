---
hide:
  - navigation
---

# Getting started

## Installation
---

### with pip <small>recommended</small>

`corcli` is published as a [Python package] and can be installed with `pip`, ideally by using a [virtual environment]. Open up a terminal and install corcli with:


=== "Latest"

    ```sh
    pip install corcli
    ```

=== "1.x"

    ```sh
    pip install corcli=="1.*"
    ```

It will automatically install all dependencies: inquirer, cortex4py, colorama and toml.

[Python package]: https://pypi.org/project/corcli/
[virtual environment]: https://realpython.com/what-is-pip/#using-pip-in-a-python-virtual-environment

### using Docker

A [docker image] is available from the repository and comes with all dependencies pre-installed. Open up a terminal and pull the image with:

=== "Latest"

    ```sh
    docker pull ghcr.io/0xfustang/corcli:1.0.0 
    ```

=== "1.x"

    ```sh
    docker pull ghcr.io/0xfustang/corcli:1.x
    ```

[docker image]: https://pypi.org/project/corcli/

## Configuration
---

`corcli` can use a configuration file containing information about the Cortex instances and aliases. Feel free to use the example below or the one from the [code repository]. Just copy the `.example` file into `myconfigfile.toml` to get started.

```toml
title = "corcli configuration file"

[cortex-instance]

[cortex-instance.default]
url = "https://cortex.local"
verify_cert = true

hashlookup = 'CIRCLHashlookup_1_1'
malbazaar = 'MalwareBazaar_1_0'
eml = 'EmlParser_2_1'
vt = 'VirusTotal_GetReport_3_1'
doh = 'GoogleDNS_resolve_1_0_0'
misp = 'MISP_2_1'
octi = 'OpenCTI_SearchObservables_2_0'

[cortex-instance.dev]
url = "https://cortex-dev.local"
verify_cert = true

octi = 'OpenCTI_SearchObservables_2_0'

[cortex-instance.qa]
url = "https://cortex-qa.local/"
verify_cert = false
```

???+ note

    `corcli` uses TOML configuration file.

???+ warning

    Do not change `cortex-instance.default`, `corcli` won't be able to read the default instance config

Now that you have a configuration file, use the option `-cf` or `--config-file`.

[code repository]: https://github.com/0xFustang/corcli/blob/main/ccli_config.toml.example

### API key

`corcli` can use the environment variables for the API key to provide or just use the `-k` or `--api-key` argument. If none of these options are used, you will be prompted to add the API key.

=== "Using the environment variables"

    ```sh
    export CORTEX_CLI_API="API_KEY"
    corcli -cf ~/corcli_config/corcli.toml -d google.com
    ```

=== "Using argument"

    ```powershell
    corcli -cf ~/corcli_config/corcli.toml -k API_KEY -d google.com
    ```

## Submit your first job

To submit a job to Cortex use the following:

=== "With a configuration file"

    ```sh
    corcli -cf ~/corcli_config/corcli.toml -d google.com
    ```

=== "Without a configuration file"

    ```sh
    corcli -u https://cortex.afterlife.local -d google.com
    ```

You will find more use cases in the [Usage] page.

[Usage]: /usage

## Tips
---

### `corcli` aliases

Take advantage of the aliases for your favorites analyzers by configuring your [configuration file], otherwise `corcli` will prompt you to select one of the enabled Cortex's analyzers.

???+ note

    If the analysers present in your configuration file gets updated you will need to
    manually apply the changes.

=== "One analyzers"

    ```sh
    corcli -cf ~/corcli_config/corcli.toml -d google.com -a eml
    ```

=== "Multiple analyzers"

    ```sh
    corcli -u https://cortex.afterlife.local -d google.com -a eml -a hashlookup -a doh
    ```

[configuration file]: /getting-started/#configuration

### sh alias

You can set a bash or zsh alias to call `corcli` with your regular configuration file. 

=== "Python virtual environment"

    ```sh
    alias corcli='source /path/to/your_virtual_env/bin/activate && python -m corcli -cf ~/corcli_configs/corcli.toml'
    ```

=== "Docker"

    ```sh
    alias corcli='docker run -ti -e CORTEX_CLI_API=$CORTEX_CLI_API --rm -v $CONFIG_PATH:/app/config/ -v $(pwd):/app/ ghcr.io/0xfustang/corcli:1.0.0 corcli -cf config/corcli.toml'
    ```

