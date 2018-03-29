---
title: Note sulla versione di NuGet 1.2 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Note sulla versione per NuGet 1.2, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
keywords: NuGet 1.2 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0d95f41c5bc5d490764c9f128ee621e1037cef66
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-12-release-notes"></a>Note sulla versione 1.2 di NuGet

[Note sulla versione 1.0 e 1.1 di NuGet](../release-notes/nuget-1.1.md) | [note sulla versione 1.3 NuGet](../release-notes/nuget-1.3.md)

NuGet 1.2 è stata rilasciata il 30 marzo 2011.

## <a name="new-features"></a>Nuove funzionalità

### <a name="framework-profile-support"></a>Supporto del profilo di Framework

Dall'inizio, NuGet è supportata con le librerie di diversi framework di destinazione. Ma ora pacchetti possono contenere assembly destinati a profili specifici ad esempio il profilo di Windows Phone. Per un profilo specifico di un framework di destinazione, aggiungere un trattino seguito dall'abbreviazione del profilo. Per impostare come destinazione SilverLight in esecuzione in un Windows Phone (anche noto come Windows Phone 7), ad esempio, è possibile inserire un assembly nella cartella 3 wp, come illustrato nella schermata seguente.

![Framework profilo cartella Layout](./media/framework-profile-support.png)

Si potrebbe chiedere perché è stato solo scelto di non utilizzare "wp7" come moniker. È in parte, stiamo prevedendo che Windows Phone 7 è possibile eseguire una versione più recente di Silverlight in futuro, nel qual caso è necessario essere più specifici sui quali framework profilo che si è interessati a.

### <a name="automatically-add-binding-redirects"></a>Aggiungere automaticamente i reindirizzamenti di associazione

Quando si installa un pacchetto con assembly con nome sicuro, NuGet può ora rilevare i casi in cui il progetto richiede da aggiungere al file di configurazione in ordine per il progetto in compilazione e li aggiunge automaticamente i reindirizzamenti di associazione. Parte 3 di serie di post di blog di David Ebbo al controllo delle versioni NuGet intitolata "[unificazione tramite associazione reindirizza](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" descrive lo scopo di questa funzionalità in ulteriori dettagli.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Specifica i riferimenti ad Assembly Framework (GAC)

In alcuni casi, un pacchetto può dipendere da un assembly in .NET Framework. In teoria, non è sempre necessario che il consumer del pacchetto di fare riferimento all'assembly di framework. Ma in alcuni casi, è importante, ad esempio quando lo sviluppatore deve rispetto ai tipi nell'assembly di codice per utilizzare il pacchetto. Il nuovo `frameworkAssemblies` elemento, un elemento figlio dell'elemento dei metadati, è possibile specificare un set di `frameworkAssembly` gli elementi che punta a un assembly del Framework nella GAC. Si noti l'enfasi assembly Framework.
Questi assembly non sono inclusi nel pacchetto come questi sono considerati in ogni computer come parte di .NET Framework. Nella tabella seguente sono elencati gli attributi del `frameworkAssembly` elemento.


|Attributo |Descrizione|
|----------------|-----------|
|**assemblyName**|*Richiesto*. Nome dell'assembly, ad esempio `System.Net`.|
|**targetFramework**|*Parametro facoltativo*. Consente di specificare un nome di profilo e framework (o alias) che l'assembly framework si applica a, ad esempio "net40" o "sl4". Usa lo stesso formato descritto in [che supporta più Framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet.exe ora è in grado di archiviare le credenziali di chiave API

Quando si utilizza lo strumento da riga di comando nuget.exe, è ora possibile utilizzare il comando SetApiKey per archiviare la chiave API. In questo modo, non è necessario specificarla ogni volta che si esegue il push un pacchetto. Per ulteriori informazioni su come salvare la chiave API con nuget.exe, [leggere la documentazione sulla pubblicazione di un pacchetto](../create-packages/publish-a-package.md).

### <a name="package-explorer"></a>Esplora pacchetti
Esplora pacchetti è stato aggiornato per il supporto di NuGet 1.2. Per ulteriori informazioni, consultare il [note sulla versione di Esplora pacchetti](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Altre funzionalità e correzioni

L'elenco precedente sono più rilevanti delle numerose funzionalità sono implementati e i bug risolti. Tutto, è implementato/fixed [gli elementi di lavoro 59](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in questa versione.

## <a name="known-issues"></a>Problemi noti

* **1.2 pacchetto incompatibilità**: pacchetti compilati con la versione più recente dello strumento della riga di comando, nuget.exe (1.2 >) non funzionerà con le versioni precedenti di Visual Studio NuGet aggiuntivo (ad esempio 1.1). In caso di un messaggio di errore indicante un elemento sullo schema incompatibile, si è verificato l'errore. Aggiornare NuGet alla versione più recente.
* **Incompatibilità NuGet.Server**: se si ospita un feed utilizzando il progetto NuGet.Server di NuGet interno, è necessario aggiornare il progetto con la versione più recente di NuGet.Server.
* **Errore di mancata corrispondenza di firma**: se si esegue un errore durante l'aggiornamento con un messaggio su una firma non corrispondente, è necessario disinstallare prima NuGet e quindi installarlo. Viene riportata nel nostro [pagina problemi noti](../release-notes/known-issues.md) che fornisce ulteriori dettagli. Il problema solo influisce su quelli in esecuzione Visual Studio 2010 SP1 e dispone di una versione 1.0 di NuGet installato che è stato firmato in modo non corretto. In questa versione viene reso disponibile dal sito Web CodePlex per un breve periodo in modo da questo problema non riguarda Troppi utenti.