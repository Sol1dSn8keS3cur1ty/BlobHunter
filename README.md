[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# BlobHunter-Lite

This is a modified version of https://github.com/cyberark/BlobHunter. 

## Differences

Unlike the original BlobHunter, BlobHunter-Lite only requires an account with the "Reader" role assigned to identify misconfigured containers within Azure Blob Storage. BlobHunter-Lite will not list the individual files found within misconfigured containers.

I wrote a blog on how you can use an account with the "Reader" role to identify misconfigured Blob Storage containers, and then access the data within them anonymously. [An Intro to Azure Blob Storage and Abusing the Reader Role to Access Data](https://sol1dsn8kes3cur1ty.github.io/blog/An%20Intro%20to%20Azure%20Blob%20Storage%20and%20Abusing%20the%20Reader%20Role%20to%20Access%20Data.html
)

## Description

An opensource tool for scanning Azure blob storage accounts for publicly opened blobs.  
BlobHunter is a part of  "Hunting Azure Blobs Exposes Millions of Sensitive Files" research:  
https://www.cyberark.com/resources/threat-research-blog/hunting-azure-blobs-exposes-millions-of-sensitive-files  
  
## Overview

BlobHunter helps you identify Azure blob storage containers which store files that are publicly available to anyone with an internet connection.  

The tool will help mitigate risk by identifying poorly configured containers that store sensitive data, which is specifically helpful in larger scale Azure subscriptions where there are a significant number of storage accounts that could be hard to track.  
BlobHunter produces an informative csv result file that provides important details on each publicly opened container in the scanned environment.

## Requirements

1. Python 3.5+

2. Azure CLI

3. [`requirements.txt`](requirements.txt) packages

4. Azure user with one of the following [built-in roles](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles):

   -	[Owner](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#owner)  
   -  [Contributor](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#contributor)  
   -	[Storage Account Contributor](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#storage-account-contributor)  

   Or any Azure user with a role that allows to perform the following Azure actions:

   ```
   Microsoft.Resources/subscriptions/read
   Microsoft.Resources/subscriptions/resourceGroups/read
   Microsoft.Storage/storageAccounts/read
   Microsoft.Storage/storageAccounts/listkeys/action
   Microsoft.Storage/storageAccounts/blobServices/containers/read
   Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read
   ```

## Build

#### Example for installation on Ubuntu:

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

```bash
pip3 install -r requirements.txt
```

## Usage

Simply run

```
python3 BlobHunter.py
```

If you are not logged in in the Azure CLI, a browser window will be prompted at you for inserting your Azure user credentials.

## Demo
![BlobHunter](https://github.com/cyberark/BlobHunter/blob/assets/BlobHunterDemo.gif)

## References

For any question or feedback, please contact [Daniel Niv](https://github.com/DanielNiv), [Asaf Hecht](https://twitter.com/Hechtov) and CyberArk Labs.

## License

Copyright (c) 2021 CyberArk Software Ltd. All rights reserved.  
Licensed under the MIT License.  
For the full license text see [`LICENSE`](LICENSE).
