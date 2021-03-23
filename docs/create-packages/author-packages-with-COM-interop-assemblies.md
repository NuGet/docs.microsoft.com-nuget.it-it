---
title: Creare pacchetti con assembly di interoperabilità COM
description: Descrive come creare pacchetti che contengono assembly di interoperabilità COM
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b12672e81a974e113ffbda80560c9d3eede9c69d
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859122"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Creare pacchetti NuGet contenenti assembly di interoperabilità COM

I pacchetti che contengono gli assembly di interoperabilità COM devono includere un [file di destinazioni](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) appropriato in modo che i metadati `EmbedInteropTypes` corretti vengano aggiunti ai progetti usando il formato PackageReference. Per impostazione predefinita, i metadati `EmbedInteropTypes` sono sempre false per tutti gli assembly quando viene usato PackageReference, quindi il file di destinazioni aggiunge i metadati in modo esplicito. Per evitare conflitti, il nome della destinazione deve essere univoco. L'ideale è usare una combinazione del nome del pacchetto dell'assembly che viene incorporato, sostituendo `{InteropAssemblyName}` nell'esempio riportato di seguito con tale valore. Per un esempio, vedere anche [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop).

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Si noti che, quando si usa il formato di gestione `packages.config`, l'aggiunta di riferimenti agli assembly dai pacchetti fa sì che NuGet e Visual Studio cerchino gli assembly di interoperabilità COM e impostino `EmbedInteropTypes` su true nel file di progetto. In questo caso, viene eseguito l'override delle destinazioni.

Per impostazione predefinita inoltre gli [asset di compilazione non vengono trasferiti in modo transitivo](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). I pacchetti creati come descritto qui funzionano diversamente quando ne viene eseguito il pull come dipendenza transitiva da un progetto al riferimento al progetto. L'utente del pacchetto ne può consentire il trasferimento modificando il valore predefinito di PrivateAssets in modo che non includa la compilazione.

<a name="creating-the-package"></a>