---
title: Informazioni di riferimento sul file packages.config NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: In alcuni tipi di progetto, il file packages.config include l'elenco aggiornato dei pacchetti NuGet usati nel progetto.
keywords: File packages.config NuGet, riferimenti a pacchetti NuGet, dipendenze NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 38d4724d25476d372a936cb8ebf08e2b53fcf9f4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="packagesconfig-reference"></a>Informazioni di riferimento su packages.config

Il file `packages.config` viene usato in alcuni tipi di progetto per gestire l'elenco dei pacchetti a cui fa riferimento il progetto. In questo modo NuGet può ripristinare facilmente le dipendenze del progetto quando il progetto devono essere trasportato in un computer diverso, ad esempio un server di compilazione, senza tutti i pacchetti.

## <a name="schema"></a>Schema

Lo schema è semplice. Dopo l'intestazione XML standard è presente un singolo nodo `<packages>` che contiene uno o più elementi `<package>`, uno per ogni riferimento. Ogni elemento `<package>` può avere gli attributi seguenti:

| Attributo | Obbligatorio | Descrizione |
| --- | --- | --- |
| ID | Yes | Identificatore del pacchetto, ad esempio Newtonsoft.json o Microsoft.AspNet.Mvc. | 
| version | Yes | Versione esatta del pacchetto da installare, ad esempio 3.1.1 o 4.2.5.11-beta. La stringa di versione deve includere almeno tre numeri. Il quarto numero è facoltativo, così come un suffisso di versione non definitiva. Non sono consentiti intervalli. | 
| targetFramework | No | [Moniker del framework di destinazione (TFM)](target-frameworks.md) da applicare durante l'installazione del pacchetto. Viene inizialmente impostato sulla destinazione del progetto quando viene installato un pacchetto. Ne consegue che elementi `<package>` diversi possono avere moniker del framework di destinazione differenti. Ad esempio, se si crea un progetto destinato a .NET 4.5.2, i pacchetti installati in quel punto useranno il moniker del framework di destinazione net452. Se in un secondo momento si imposta .NET 4.6 come destinazione del progetto e si aggiungono altri pacchetti, questi useranno il moniker del framework di destinazione net46. In caso di mancata corrispondenza tra la destinazione del progetto e gli attributi `targetFramework`, verranno generati avvisi e in tal caso è possibile reinstallare i pacchetti interessati. | 
| allowedVersions | No | Intervallo di versioni consentite per questo pacchetto applicate durante l'aggiornamento del pacchetto (vedere [Limitazione delle versioni per l'aggiornamento](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Questo attributo *non* influisce sul pacchetto installato durante un'operazione di installazione o di ripristino. Per la sintassi, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards). Anche l'interfaccia utente di Gestione pacchetti disabilita tutte le versioni non comprese nell'intervallo consentito. | 
| developmentDependency | No | Se il progetto stesso che utilizza il pacchetto crea un pacchetto NuGet, l'impostazione di questo attributo su `true` per una dipendenza impedisce l'inclusione di tale pacchetto quando viene creato il pacchetto utilizzato. Il valore predefinito è `false`. | 

## <a name="examples"></a>Esempi

Il file `packages.config` seguente fa riferimento a due dipendenze:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Il file `packages.config` seguente fa riferimento a nove pacchetti, ma `Microsoft.Net.Compilers` non verrà incluso durante la compilazione del pacchetto utilizzato a causa dell'attributo `developmentDependency`. Il riferimento a Newtonsoft.Json limita inoltre gli aggiornamenti solo alle versioni 8.x e 9.x.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
