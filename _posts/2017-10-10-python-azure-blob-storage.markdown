---
layout: post
title: "Solved: Azure Storage Library for Python returns Not Found"
excerpt: "The problem: Using the Azure Storage Library for Python
I could list blob contents, but downloading them would fail with `Resource not found`, although the file was there with right permissions in place. TLDR: generate a SAS url + use urllib."
category: Azure
tags: [python, azure-blob-storage, sas-token]
comments: true
image:
  feature: python-blob/cover.jpg
---
The usual way to make large files available to an Azure Cloud Service is to put them into blob storage and then 
cache in the local storage of the VM. I recently had to do it for a Python 3.6-based service. Using the Azure Storage Library for Python [[1]]
I could list blob contents, but downloading them would fail with `Resource not found`, although the file was there with right permissions in place.

## Shared access signature (SAS)

A shared access signature (SAS) is
 a way to grant limited access to your storage account,
  without exposing your account key [[2]]. Among other things, you can use
  SAS to generate an access url to a certain file. 

  To do so, you use the format `http://{storageaccounturl.com}/{container name}/{blob name}?{SAS token}`

## Downloading blobs with Python
The example below assumes using local Azure Storage emulator.

{% highlight python %}

    from urllib.request import urlretrieve

    def download_blob(blob_name, local_path):
        container_name = "TheContainer"
        blob_uri = "http://127.0.0.1:10000/devstoreaccount1/" 
            + container_name 
            + "/" 
            + blob_name 
            + sas_token

        urlretrieve(blob_uri, local_path)
{% endhighlight %}


[1]: https://github.com/Azure/azure-storage-python
[2]: https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1

