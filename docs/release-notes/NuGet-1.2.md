---
title: Note sulla versione di NuGet 1,2
description: Note sulla versione per NuGet 1,2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237186"
---
# <a name="nuget-12-release-notes"></a>Note sulla versione di NuGet 1,2

Note sulla versione [di NuGet 1,0 e 1,1](../release-notes/nuget-1.1.md)  |  [Note sulla versione di NuGet 1,3](../release-notes/nuget-1.3.md)

NuGet 1,2 è stato rilasciato il 30 marzo 2011.

## <a name="new-features"></a>Nuove funzioni e caratteristiche

### <a name="framework-profile-support"></a>Supporto del profilo di Framework

Dall'inizio, NuGet supportava le librerie che hanno come destinazione Framework diversi. Ma ora i pacchetti possono contenere assembly destinati a profili specifici, ad esempio il profilo Windows Phone. Per fare riferimento a un profilo specifico di un Framework, aggiungere un trattino seguito dall'abbreviazione del profilo. Ad esempio, per specificare come destinazione SilverLight in esecuzione su un Windows Phone (noto anche come Windows Phone 7), è possibile inserire un assembly nella cartella SL3-WP come illustrato nello screenshot seguente.

![Layout delle cartelle del profilo del Framework](./media/framework-profile-support.png)

È possibile chiedersi perché non è stato semplicemente scelto di usare "WP7" come moniker. In parte, si prevede che Windows Phone 7 potrebbe eseguire una versione più recente di Silverlight in futuro. in questo caso potrebbe essere necessario essere più specifici del profilo del Framework destinazione.

### <a name="automatically-add-binding-redirects"></a>Aggiungere automaticamente i reindirizzamenti di binding

Quando si installa un pacchetto con assembly con nome sicuro, NuGet può ora rilevare i casi in cui il progetto richiede l'aggiunta di reindirizzamenti di binding al file di configurazione affinché il progetto venga compilato e aggiunto automaticamente. La parte 3 della serie di post di Blog di David Ebbo sul controllo delle versioni di NuGet, denominata "[unificazione tramite reindirizzamenti di binding](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)", illustra lo scopo di questa funzionalità in altri dettagli.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Specifica di riferimenti ad assembly Framework (GAC)

In alcuni casi, un pacchetto può dipendere da un assembly presente nell'.NET Framework. In modo rigoroso, non è sempre necessario che l'utente del pacchetto faccia riferimento all'assembly del Framework. In alcuni casi, tuttavia, è importante, ad esempio quando lo sviluppatore deve codificare i tipi in tale assembly per poter utilizzare il pacchetto. Il nuovo `frameworkAssemblies` elemento, un elemento figlio dell'elemento metadata, consente di specificare un set di `frameworkAssembly` elementi che puntano a un assembly del Framework nella GAC. Si noti l'enfasi sull'assembly del Framework.
Questi assembly non sono inclusi nel pacchetto perché si presuppone che si trovino in ogni computer come parte del .NET Framework. Nella tabella seguente sono elencati gli attributi dell' `frameworkAssembly` elemento.


|Attributo |Descrizione|
|----------------|-----------|
|**assemblyName**|*Obbligatorio*. Nome dell'assembly, ad esempio `System.Net` .|
|**targetFramework**|*Facoltativo*. Consente di specificare un Framework e un nome di profilo (o alias) a cui si applica questo assembly del Framework, ad esempio "net40" o "SL4". USA lo stesso formato descritto in [supporto di più framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe ora è in grado di archiviare le credenziali della chiave API

Quando si usa lo strumento da riga di comando nuget.exe, è ora possibile usare il comando SetApiKey per archiviare la chiave API. In questo modo, non sarà necessario specificarlo ogni volta che si esegue il push di un pacchetto. Per altre informazioni sul salvataggio della chiave API con nuget.exe, [vedere la documentazione relativa alla pubblicazione di un pacchetto](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Esplora pacchetti
Esplora pacchetti è stato aggiornato per supportare NuGet 1,2. Per ulteriori informazioni, vedere le [Note sulla versione di Esplora pacchetti](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Altre funzionalità/correzioni

L'elenco precedente è stato il più evidente tra le numerose funzionalità implementate e i bug corretti. In tutti gli elementi di lavoro sono stati implementati/corretti [59 elementi di lavoro](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in questa versione.

## <a name="known-issues"></a>Problemi noti

* **1,2 incompatibilità dei pacchetti** : i pacchetti compilati con la versione più recente dello strumento da riga di comando nuget.exe (> 1,2) non funzioneranno con le versioni precedenti del componente aggiuntivo NuGet vs (ad esempio 1,1). Se si esegue un messaggio di errore che informa sullo schema incompatibile, si è verificato questo errore. Aggiornare NuGet alla versione più recente.
* **Incompatibilità di NuGet. Server** : se si ospita un feed NuGet interno usando il progetto NuGet. Server, sarà necessario aggiornare il progetto con la versione più recente di NuGet. Server.
* **Errore di mancata corrispondenza della firma** : se si è rilevato un errore durante un aggiornamento con un messaggio relativo a una mancata corrispondenza di firma, è necessario disinstallare prima NuGet e quindi installarlo. Questa pagina è elencata nella [pagina problemi noti](../release-notes/known-issues.md) che fornisce ulteriori dettagli. Il problema riguarda solo quelli che eseguono Visual Studio 2010 SP1 ed è installata una versione di NuGet 1,0 che è stata firmata in modo non corretto. Questa versione è stata resa disponibile dal sito Web CodePlex solo per un breve periodo di tempo, quindi questo problema non dovrebbe influire su troppe persone.