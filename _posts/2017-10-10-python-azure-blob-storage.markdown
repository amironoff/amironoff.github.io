---
layout: post
title: "Solved: Azure Storage Library for Python returns Not Found"
excerpt: "A recent case: Using the Azure Storage Library for Python
I could list blob contents, but downloading them would fail with `Resource not found`. The files were there with right permissions in place. TLDR: generate a SAS url + use urllib."
category: Azure
tags: [python, azure-blob-storage, sas-token]
comments: true
image:
  feature: python-blob/cover.jpg
---
The usual way to make large files available to an Azure Cloud Service is to put them into blob storage and then 
cache in the local storage of the VM. I recently had to do it for a Python 3.6-based service that relied on a couple of ~2GB machine learning models. Using the Azure Storage Library for Python [[1]]
I could list blob contents, but downloading them would fail with `Resource not found`, although the file was there with right permissions in place.

## Shared access signature (SAS)

A shared access signature (SAS) is
 a way to grant limited access to your storage account,
  without exposing your account key [[2]]. Among other things, you can use
  SAS to generate an access url to a certain file. To do so, you use the following format:
  
{% highlight python %}

   http://{storageaccounturl.com}/{container name}/{blob name}?{SAS token}

{% endhighlight %}

After failing to access blob storage, using the SDK, I tried downloading the file using the raw SAS-based URL in the browser and succeeded.
So I figured that the way around this is going back to the basics.

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

## Conclusion

SDKs are great because they usually save us a lot of effort. Except when they don't work :) In such cases
it's useful to know your options and, if necessary, go down a level to solve the task on time.

[1]: https://github.com/Azure/azure-storage-python
[2]: https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1

