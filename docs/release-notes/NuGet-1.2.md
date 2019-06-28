---
title: Note sulla versione 1.2 di NuGet
description: Note sulla versione per NuGet 1.2, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426194"
---
# <a name="nuget-12-release-notes"></a>Note sulla versione 1.2 di NuGet

[Note sulla versione 1.0 e 1.1 di NuGet](../release-notes/nuget-1.1.md) | [note sulla versione di NuGet 1.3](../release-notes/nuget-1.3.md)

1\.2 di NuGet è stato rilasciato il 30 marzo 2011.

## <a name="new-features"></a>Nuove funzionalità

### <a name="framework-profile-support"></a>Supporto del profilo di Framework

Dall'inizio, NuGet supportati con le librerie di diversi framework di destinazione. Ma ora i pacchetti possono contenere assembly destinati a profili specifici, ad esempio il profilo di Windows Phone. Per un profilo specifico di un framework di destinazione, aggiungere un trattino seguito usando l'abbreviazione del profilo. Ad esempio, per impostare come destinazione SilverLight in esecuzione in un Windows Phone (noto anche come Windows Phone 7), è possibile inserire un assembly nella cartella 3 wp come illustrato nello screenshot seguente.

![Layout cartella del profilo di Framework](./media/framework-profile-support.png)

Si potrebbe chiedere perché abbiamo semplicemente non sceglie di usare "wp7" il moniker. È in parte, stiamo prevedendo che Windows Phone 7 è possibile eseguire una versione più recente di Silverlight in futuro, nel qual caso si potrebbe essere necessario essere più specifici sulla quale framework profilo che si sta destinata ad.

### <a name="automatically-add-binding-redirects"></a>Aggiungere automaticamente i reindirizzamenti di associazione

Quando si installa un pacchetto con assembly con nome sicuro, NuGet può ora rilevare i casi in cui il progetto richiede da aggiungere al file di configurazione affinché il progetto per la compilazione e le aggiunge automaticamente i reindirizzamenti di associazione. Parte 3 di serie di post di blog di David Ebbo sul controllo delle versioni NuGet intitolata "[unificazione tramite associazione reindirizza](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" descrive lo scopo di questa funzionalità in modo più dettagliato.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Specifica i riferimenti ad Assembly di Framework (GAC)

In alcuni casi, un pacchetto può dipendere da un assembly incluso in .NET Framework. In teoria, non è sempre necessario che il consumer del pacchetto di fare riferimento all'assembly di framework. Ma in alcuni casi, è importante, ad esempio quando lo sviluppatore deve rispetto ai tipi nell'assembly di codice per usare il pacchetto. Il nuovo `frameworkAssemblies` elemento, un elemento figlio dell'elemento dei metadati, consente di specificare un set di `frameworkAssembly` gli elementi che punta a un assembly di Framework nella GAC. Si noti l'accento su assembly del Framework.
Questi assembly non vengono inclusi nel pacchetto come questi sono considerati in ogni computer come parte di .NET Framework. La tabella seguente elenca gli attributi del `frameworkAssembly` elemento.


|Attributo |Descrizione|
|----------------|-----------|
|**assemblyName**|*Obbligatorio*. Nome dell'assembly, ad esempio `System.Net`.|
|**targetFramework**|*Facoltativo*. Consente di specificare un nome di profilo e framework (o alias) che l'assembly di framework si applica a, ad esempio "net40" o "sl4". Usa lo stesso formato descritto nella [che supportano più Framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet.exe ora è in grado di archiviare le credenziali di chiave API

Quando si usa lo strumento da riga di comando nuget.exe, è ora possibile usare il comando SetApiKey per archiviare la chiave API. In questo modo, non sarà necessario specificarla ogni volta che si attiva un pacchetto. Per altre informazioni su come salvare la chiave API con nuget.exe, [leggere la documentazione sulla pubblicazione di un pacchetto](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Esplora pacchetti
Esplora pacchetti è stata aggiornata per il supporto di NuGet 1.2. Per altre informazioni, consultare il [note sulla versione di Package Explorer](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Altre funzionalità e correzioni

Nell'elenco precedente sono stati i più evidenti delle molte nuove funzionalità sono stati implementati i bug sono stati corretti. Tutto sommato, abbiamo implementato/risolto [elementi di lavoro 59](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in questa versione.

## <a name="known-issues"></a>Problemi noti

* **1.2 creare il pacchetto incompatibilità**: I pacchetti compilati con la versione più recente dello strumento della riga di comando, nuget.exe (1.2 >) non funzionerà con le versioni precedenti di Visual Studio NuGet aggiuntivo (ad esempio 1.1). Se si verifica un messaggio di errore che indica che qualcosa sullo schema incompatibile, si eseguono in alcuni casi questo errore. Eseguire l'aggiornamento di NuGet alla versione più recente.
* **Incompatibilità di NuGet. server**: Se si ospita un feed utilizzando il progetto NuGet. server interno in NuGet, è necessario aggiornare il progetto con la versione più recente di NuGet. Server.
* **Errore di mancata corrispondenza della firma**: Se si verifica un errore durante l'aggiornamento con un messaggio su una firma di mancata corrispondenza, è necessario innanzitutto disinstallare NuGet e quindi installarlo. Questa opzione è presente nel nostro [pagina dei problemi noti](../release-notes/known-issues.md) fornisce ulteriori dettagli. Il problema interessa quelli che eseguono Visual Studio 2010 SP1 solo e dispone di una versione di NuGet 1.0 installato che è stato firmato in modo non corretto. Questa versione è stata resi disponibile solo dal sito Web CodePlex per un breve periodo di tempo in modo che questo problema non hanno impatto su troppi utenti.