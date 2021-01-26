---
title: Impatto di project.json sugli autori di pacchetti NuGet
description: Informazioni dettagliate su come l'implementazione di project.json in NuGet 3.x abbia effetto sugli autori di pacchetti, ad esempio con funzionalità, contenuto e formato dei pacchetti non supportati.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 82b7ce7962ecccc9559ae25a8fe35a3820238049
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775393"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Impatto di project.json durante la creazione di pacchetti

> [!Important]
> Questo contenuto è deprecato. I progetti devono usare i formati `packages.config` o PackageReference.

Il sistema `project.json` usato in NuGet 3+ ha effetto sugli autori di pacchetti in diversi modi, come illustrato nelle sezioni seguenti.

## <a name="changes-affecting-existing-packages-usage"></a>Modifiche che hanno effetto sull'utilizzo dei pacchetti esistenti

I tradizionali pacchetti NuGet supportano un set di funzionalità che non passano nella sfera transitiva.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Gli script di installazione e disinstallazione vengono ignorati

Il modello di ripristino transitivo, illustrato in [Risoluzione delle dipendenze](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), non contempla il concetto di "fase di installazione dei pacchetti". Un pacchetto è presento o non presente, ma non esiste un processo coerente eseguito quando viene installato un pacchetto.

Gli script di installazione inoltre erano supportati solo in Visual Studio. Gli altri IDE dovevano simulare l'API di estendibilità di Visual Studio per provare a supportare tali script e nessun supporto era disponibile negli editor e negli strumenti da riga di comando comuni.

### <a name="content-transforms-are-not-supported"></a>Le trasformazioni di contenuto non sono supportate

Analogamente agli script di installazione, le trasformazioni vengono eseguite durante l'installazione dei pacchetti e in genere non sono idempotenti. Poiché non esiste più una fase di installazione, la trasformazione XDT e funzionalità simili non sono supportate e vengono ignorate se un pacchetto di questo tipo viene usato in uno scenario transitivo.

### <a name="content"></a>Content

Nei tradizionali pacchetti NuGet sono disponibili file di contento, ad esempio codice sorgente e file di configurazione, che in genere vengono usati in due scenari:

1. File iniziali rilasciati nel progetto in modo che l'utente possa modificarli successivamente. Un esempio comune sono i file di configurazione predefiniti.

1. File di contenuto usati come complemento degli assembly installati nel progetto. In questo caso l'esempio può essere l'immagine di un logo usata da un assembly.

Il supporto per il contenuto è attualmente disabilitato per motivi simili a quelli degli script e delle trasformazioni, ma ne è in corso la progettazione.

I file di contenuto possono comunque essere inseriti nei pacchetti anche se attualmente vengono ignorati, tuttavia l'utente finale può comunque copiarli nella posizione corretta.

È possibile visualizzare una delle proposte per riportare i file di contenuto e seguirne lo stato di avanzamento, qui: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627) .

## <a name="impact-for-package-authors"></a>Impatto per gli autori di pacchetti

I pacchetti che usano le funzionalità indicate sopra devono usare un meccanismo diverso. Il meccanismo di norma più utile prevede l'uso dei file di destinazioni/proprietà MSBuild che sono ancora pienamente supportati. Il sistema di compilazione può scegliere di selezionare altre convenzioni nel pacchetto. In questo modo vengono supportate le destinazioni MSBuild, oltre agli analizzatori Roslyn. È possibile compilare pacchetti che supportano destinazioni e analizzatori per scenari `packages.config` e `project.json`.

I pacchetti che provano a modificare il progetto per semplificare l'avvio in genere funzionano in un set molto limitato di scenari e devono fornire un file leggimi o linee guida su come usare il pacchetto.

La maggior parte dei pacchetti esistenti non dovrà usare il formato descritto sotto.

Il formato consente il contenuto nativo come scenario di prima classe. Gli assembly gestiti dipendono quindi da implementazioni collegate all'hardware per l'invio di implementazioni binarie unitamente agli assembly gestiti in base alla piattaforma di destinazione. Il pacchetto System.IO.Compression, ad esempio, utilizza questa tecnologia. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

In sintesi, se la funzionalità illustrata sopra non è assolutamente necessaria, è consigliabile continuare a usare il formato di pacchetto esistente, perché il formato descritto qui è supportato solo da NuGet 3.x+.

Anche se è possibile compilare pacchetti che funzionino in scenari sia `packages.config` che `project.json` tramite l'esecuzione di shim, spesso è più semplice limitarsi a strutturare i pacchetti nel modo tradizionale, senza le funzionalità deprecate citate sopra.

## <a name="3x-package-format"></a>Formato del pacchetto 3.x

Il formato del pacchetto 3.x consente di usare diverse funzionalità aggiuntive oltre a quelle di NuGet 2.x:

1. Definizione di un assembly di riferimento usato per la compilazione e di un set di assembly di implementazioni usati per il runtime in diverse piattaforme o dispositivi. Ciò consente di sfruttare le API specifiche della piattaforma fornendo al contempo una superficie di attacco comune agli utenti. In particolare risulta semplificata la scrittura di librerie portabili intermedie.

1. I pacchetti possono basarsi sulle piattaforme, ad esempio sistemi operativi o architettura CPU.

1. È consentita la separazione di implementazioni specifiche delle piattaforme nei pacchetti complementari.

1. Supporto delle dipendenze native come oggetto di prima classe.
