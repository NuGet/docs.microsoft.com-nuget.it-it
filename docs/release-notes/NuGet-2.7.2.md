---
title: Note sulla versione di NuGet 2.7.2
description: Note sulla versione per NuGet 2.7.2 inclusi noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550070"
---
# <a name="nuget-272-release-notes"></a>Note sulla versione di NuGet 2.7.2

[Note sulla versione di NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md)

11 novembre 2013 è stato rilasciato NuGet 2.7.2.

## <a name="noteworthy-bug-fixes-and-features"></a>Funzionalità e correzioni di Bug importanti

### <a name="license-text"></a>Testo di licenza
Per un certo periodo, Microsoft ha inserito i pacchetti NuGet per varie librerie open source più diffusi come parte dei modelli predefiniti per i progetti applicazione Web in Visual Studio. jQuery è probabilmente quello più noto di questo tipo di libreria. A causa il contratto di supporto associato ai componenti che vengono recapitati insieme a un prodotto, file di script del pacchetto contiene testo di licenza diversi rispetto al file di script disponibile nello stesso pacchetto nella raccolta nuget.org pubblica. Questa differenza di testo può impedire gli aggiornamenti dei pacchetti di procedere a causa di blocchi di testo di licenze diverso invalidando i file di script hanno valori hash del contenuto diverso e quindi per essere considerate come modificate all'interno del progetto.

Per attenuare questo problema, NuGet 2.7.2 consente all'autore di script includere il blocco di testo di licenze all'interno di una sezione contrassegnato in modo speciale che è simile al seguente.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Quando si aggiornano i pacchetti con contenuto file che contengono questo blocco, NuGet non prendere in considerazione il contenuto del blocco nel confronto con la versione nella raccolta NuGet e può quindi eliminare e aggiornare il file di contenuto come se corrisponde a quella originale.

Questo blocco è identificato dal testo "NUGET: iniziare a licenza TEXT" e "NUGET: fine licenza" che si verificano in qualsiasi punto nell'inizio e fine righe.  Nessun altro requisito formattazione esiste, consentendo di questa funzionalità da usare in qualsiasi tipo di file di testo, indipendentemente dal linguaggio.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Aggiungere reindirizzamenti di associazione di assembly non Framework
Per gli assembly che fanno parte di .NET Framework, NuGet ignora i reindirizzamenti di binding aggiunta nel file di configurazione dell'applicazione quando si aggiorna il pacchetto. Gli indirizzi di questa correzione di una regressione in NuGet 2.7 in base al quale i reindirizzamenti di associazione non viene aggiunti per alcuni assembly, anche se tali assembly non sono considerati parte di .NET Framework. 2.7.2 NuGet Ripristina il precedente di NuGet 2.5 e 2.6 comportamento e aggiunge i reindirizzamenti di associazione.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Installazione di librerie portabili con gli strumenti Xamarin installato
Quando gli strumenti di sviluppo di Xamarin sono installati in un computer, modificare i dati di configurazione i Framework supportati per specificare la compatibilità tra i framework di Xamarin e combinazioni di framework di destinazione esistente. Con la versione 2.7.2, adesso è a conoscenza di queste regole di compatibilità implicita, NuGet e pertanto semplifica per gli sviluppatori Xamarin piattaforme di destinazione installare le librerie portabili sono compatibili con Xamarin, ma non esplicitamente contrassegnati come tali nel pacchetto metadati stessi.

### <a name="machine-wide-configuration-settings-honored"></a>Impostazioni di configurazione a livello di computer rispettate
Quando si usano file gerarchici di NuGet. config, la chiave repositoryPath non viene rispettata per i file NuGet. config più vicini alla radice della soluzione. In Visual Studio 2013, NuGet installa un file NuGet. config personalizzato in %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config per aggiungere l'origine del pacchetto "E Microsoft.NET". Di conseguenza, la soluzione alternativa per l'uso di un repositoryPath personalizzata in una soluzione era eliminare il file NuGet. config a livello di computer - che intendono anche la rimozione dell'origine del pacchetto "E Microsoft.NET". NuGet 2.7.2 ora rispetta le regole sulla precedenza per repositoryPath quando si usano file gerarchici di NuGet. config.

## <a name="all-changes"></a>Tutte le modifiche
Per un elenco completo di lavoro gli elementi corretti in NuGet, 2.7.2, vista la [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
