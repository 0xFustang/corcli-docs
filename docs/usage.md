---
hide:
  - navigation
---

# Usage

This page describes the various features of this project.

## Run analysis with one observable

=== "domain"

    ```sh
    corcli -d google.com
    ```

=== "url"

    ```sh
    corcli -u https://google.com
    ```

=== "ip"

    ```sh
    corcli -i 1.1.1.1
    ```

=== "hash"

    ```sh
    corcli -ha 8ED4B4ED952526D89899E723F3488DE4
    ```

=== "mail"

    ```sh
    corcli -m samurai@arasaka.io
    ```

=== "file"

    ```sh
    corcli -f ~/case78/suspicious.eml
    ```

???+ information

    - The observables will be submitted as TLP:AMBER and PAP:AMBER by default.
    - You can select one or more analysers using the selector or the aliases.

`corcli` will display by default the summary reports of the jobs:

```sh
$ corcli -cf corcli.toml -d google.com -a doh
Analysis in progress for google.com ....
---
Result for analyzer GoogleDNS_resolve_1_0_0:

- info / GoogleDNS:RecordsCount="30"
```

???+ warning

    Do not be fooled if the summary is empty for some analysers. For instance, the `URLhaus_2_0` analyser does not provide a summary report when a hit is positive but instead use -e option to extract the observables.

## Run analysis with multiple observables (bulk)

The bulk feature has the ability to submit to Cortex all observables contained in a file line by line. For instance, the hashes contained in `hash.txt` will be checked against CIRCL's hashlookup and VirusTotal.

=== "Using analysers selector"

    ```sh
    corcli -b hash.txt
    ```

=== "Using aliases"

    ```sh
    corcli -b hash.txt -a hashlookup -a vt
    ```

## Display extracted artifacts

Display only the result of the extracted artifacts. Simply use the option `-e`. For instance, you can list the URLs or domain names  extracted by `FileInfo` out of a malicious MS Office document.

=== "Using a single observable"

    ```sh
    corcli -f ~/eml/maldoc.xls -a fileinfo -e
    ```

=== "Using bulk feature"

    ```sh
    corcli -b hash.txt -a hashlookup -a vt -e
    ```

??? example "Example"

    Output should be like:

    ```sh
    $ corcli -cf corcli.toml -u <URL> -e
    No alias selected. Going to selector...
    [?] Select one or multiple analysers: 
    ◯ GoogleSafebrowsing_2_0
    ❯ ◉ URLhaus_2_0
    ◯ Urlscan_io_Search_0_1_1

    Analysis in progress for <URL> ....
    ---
    Result for analyzer URLhaus_2_0:

    - [hash]: fb8ae5afbca62ae62460f62e34b1ee5b
    - [url]: https://urlhaus-api.abuse.ch/v1/download/1c513007d30a3f3ab3afc3bcad825ddad14da7251de2d7df6b5ff627dd568ff9/
    - [hash]: 1c513007d30a3f3ab3afc3bcad825ddad14da7251de2d7df6b5ff627dd568ff9
    - [url]: https://urlhaus-api.abuse.ch/v1/download/be2ce0c619189917669d61d19e767702cf4c5e8da173a91a02342a2fe9958a9e/
    - [hash]: eac675648aa4f47ebc7ebec3b093699c
    - [url]: https://urlhaus-api.abuse.ch/v1/download/d689433260877df317a4627388481fc391380ea7056805b0edc9d5f140333a65/
    - [hash]: d689433260877df317a4627388481fc391380ea7056805b0edc9d5f140333a65
    - [hash]: 27aa481dc427fee7f30c8632539a785f
    - [hash]: be2ce0c619189917669d61d19e767702cf4c5e8da173a91a02342a2fe9958a9e
    - [url]: https://urlhaus-api.abuse.ch/v1/download/723ab6d0ccf063714557018bc6f2b06bae854143599b23971b476ebc985d94b5/
    ```

## Download a file attachment

You can download files extracted by Cortex. Use the option `-df` to download an attachment for instance.

```sh
corcli -f ./suspicious.eml -e eml -df
```

???+ information

    - The files will be dropped in the current file path.
    - The files will be zip password-protected with `malware`.

## Use another Cortex instance

You can use another Cortex instance included in your configuration file or by entering the URL.

=== "Using the config file"

    ```sh
    corcli -f ./suspicious.eml -e eml -ci dui
    ```

=== "Using option -c"

    ```sh
    corcli -d google.com -c https://pain.local
    ```

???+ information

    Using the option `-ci` we set precise the cortex instance name stated in the configuration file. For instance : [cortex-instance.**dev**]