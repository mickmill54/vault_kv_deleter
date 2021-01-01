# Vault kv delete tool

**Author: Mick Miller**

**Date: 2020-12-23**

 ---

This bash script was built primarily to delete key values from a  given path.  For example if you have a series of key values in the path kv/fu/bar you can delete all the keys under say "bar" or the keys under "fu". All the keys and sub directories will be deleted under the give path.

## Contents

1. The config.json file
2. Installation instructions
3. Running the script
4. Acknowledgements

A couple of notes before diving in: 

* Back up your source secrets engine(s) Before you run this command. 
* Understand what this script is doing before you run it and tweak as needed.
* You will need to configure the config.json file for your specific use case.

> NOTE: You may notice the pattern `# echo "DEBUG ${LINENO}: "Some string"` in the script. This is used for debugging the script. I left them in for you in case you wanted to trace the code; sorry if it irritates you.

---

## 1. The config_delete.json file

This configuration file is used to reduce the amount of command line arguments and limit the arguments to:

* The path to find the secrets and the path; and
* Not storing the tokens in the configurations or code.

config_delete.json

```
{ 
    "type_val": "kv",
    "vault_url": "https://vault.example.com",
    "tmp_file": "./tmp.json",
}
```

### Explanation of keys and values

| Key           | Value                                                                           |
| ---           | -----                                                                           |
| `type_value`  | The type of secrets engine type                        |
| `vault_url`     | The vault instance URL                                                   |
| `tmp_file`    | The name of the output temp JSON file; you should not need to change this value |

---

## 2. Installation instructions

The code assumes that both the Hashi Vault client and jq are installed before you start and tests for the presence of both.

### Installing Vault and jq

If you are using the Homebrew package manager on mac OS, run the following:

```
 # For macOS
 $ brew install jq
 $ brew install vault
```

This script has not been tested on Windows or Linux, only macOS 10.x and 11.x. I will test Ubuntu at some point and refactor as needed.

### Installing the script

```
# Clone the repo and then change to the directory.
$ git clone <this repo url>
$ cd vault_kv_deleter

```

---

## 3. Running the script

Command line arguments description

```
$ vault_kv_deleter.sh \ 
  -s "${VAULT_TOKEN}" \
  -p "${VAULT_PATH_TO_DELETE}"
Usage:
  Format : ./vault_kv_migrator.sh {source token} {path}
  Example: ./vault_kv_migrator.sh -s xxxxxxx -p /kv/cnn/
  Note   : A trailing slash in path is required."
```  

---

## 4. Acknowledgements

Many thanks to the following folks:

* agaudreault-jive (https://github.com/hashicorp/vault/issues/5275)
* user2599522 (https://stackoverflow.com/a/61000422)
* kir4h (https://github.com/kir4h/rvault)
