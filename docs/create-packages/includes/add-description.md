---
ms.openlocfilehash: b615bcb78ad2eaf8524bfbf17864d4652e546ff1
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/24/2020
ms.locfileid: "80151362"
---
La descrizione facoltativa del pacchetto, visualizzata nella pagina NuGet.org del pacchetto, viene estratta dal `<description></description>` usato nel file di `.csproj` o inserito tramite il `$description` nel [file nuspec](../../reference/nuspec.md).

Un esempio di un campo di _Descrizione_ è illustrato nel testo XML seguente del file di `.csproj` per un pacchetto .NET:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <PackageId>Azure.Storage.Blobs</PackageId>
    <Version>12.4.0</Version>
    <PackageTags>Microsoft Azure Storage Blobs;Microsoft;Azure;Blobs;Blob;Storage;StorageScalable</PackageTags>
    <Description>
      This client library enables working with the Microsoft Azure Storage Blob service for storing binary and text data.
      For this release see notes - https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/README.md and https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/CHANGELOG.md
      in addition to the breaking changes https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/BreakingChanges.txt
      Microsoft Azure Storage quickstarts and tutorials - https://docs.microsoft.com/en-us/azure/storage/
      Microsoft Azure Storage REST API Reference - https://docs.microsoft.com/en-us/rest/api/storageservices/
      REST API Reference for Blob Service - https://docs.microsoft.com/en-us/rest/api/storageservices/blob-service-rest-api
    </Description>
  </PropertyGroup>
</PropertyGroup>
```
