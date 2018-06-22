---
title: Note sulla versione di NuGet 2.7.2
description: Note sulla versione per l'inclusione di NuGet 2.7.2 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0cb99e4e1ae9238286dc4fab7b8d34e5b117ed64
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820235"
---
# <a name="nuget-272-release-notes"></a>Note sulla versione di NuGet 2.7.2

[Note sulla versione di NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md)

È stata rilasciata NuGet 2.7.2 11 novembre 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Funzionalità e correzioni di Bug importanti

### <a name="license-text"></a>Testo di licenza
Per un certo periodo di tempo, Microsoft ha inserito i pacchetti NuGet per diverse librerie open source più diffusi come parte dei modelli predefiniti per i progetti di applicazione Web in Visual Studio. jQuery è probabilmente l'esempio più noto di questo tipo di libreria. A causa di contratto di supporto associato ai componenti che vengono recapitati insieme a un prodotto, i file di script del pacchetto contiene il testo di licenze diverso rispetto al file di script trovato nello stesso pacchetto nella raccolta di nuget.org pubblico. Questa differenza nel testo è possibile impedire aggiornamenti pacchetto di procedere a causa di blocchi di testo di licenze diverso causando per i valori hash del contenuto diverso i file di script (e pertanto per essere considerate come modificati all'interno del progetto).

Per evitare questo problema, NuGet 2.7.2 consente all'autore di script includere il blocco di testo licenza all'interno di una sezione contrassegnato in modo speciale che è simile al seguente.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Durante l'aggiornamento di pacchetti con contenuto di file che contengono questo blocco, NuGet non suddividere il contenuto del blocco nel confronto con la versione della raccolta NuGet e possono pertanto eliminare e aggiornare il file di contenuto come se corrisponde a quella originale.

Questo blocco è identificato dal testo "NUGET: iniziare licenza TEXT" e "NUGET: fine licenza" in corso in qualsiasi punto all'inizio e fine righe.  Nessun altro requisito formattazione esiste, consentendo di questa funzionalità utilizzabile con qualsiasi tipo di file di testo, indipendentemente dal linguaggio.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Aggiungere reindirizzamenti di associazione di assembly non Framework
Per gli assembly che fanno parte di .NET Framework, NuGet Ignora aggiungere reindirizzamenti di associazione nel file di configurazione dell'applicazione durante l'aggiornamento del pacchetto. Gli indirizzi di questa correzione di una regressione in NuGet 2.7 in base al quale i reindirizzamenti di associazione non viene aggiunti per alcuni assembly, anche se tali assembly non sono considerati parte di .NET Framework. NuGet 2.7.2 Ripristina la precedente di NuGet 2.5 e comportamento 2.6 e aggiunge i reindirizzamenti di associazione.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Installare le librerie portabili con strumenti Xamarin installati
Quando gli strumenti di sviluppo di Xamarin sono installati in un computer, modificare i dati di configurazione del Framework supportati per specificare la compatibilità tra combinazioni di framework di destinazione esistenti e il framework di Xamarin. Con la versione 2.7.2, ora è a conoscenza di queste regole implicite compatibilità NuGet e pertanto semplifica per gli sviluppatori di Xamarin piattaforme di destinazione installare le librerie portabili che sono compatibili con Xamarin, ma non esplicitamente contrassegnato come tale nel pacchetto metadati stessi.

### <a name="machine-wide-configuration-settings-honored"></a>Impostazioni di configurazione a livello di computer rispettate
Quando si utilizza gerarchici file NuGet. config, la chiave repositoryPath non è stata viene rispettata per NuGet. config file più vicini alla radice della soluzione. In Visual Studio 2013, NuGet installa un file NuGet. config personalizzato in %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config per aggiungere l'origine del pacchetto "E Microsoft.NET". Di conseguenza, la soluzione alternativa per l'utilizzo di un repositoryPath personalizzato in una soluzione era eliminare NuGet. config a livello di computer - che anche la rimozione di origine del pacchetto "E Microsoft.NET". NuGet 2.7.2 rispetta le regole di precedenza per repositoryPath ora quando si utilizzano file NuGet. config gerarchici.

## <a name="all-changes"></a>Tutte le modifiche
Per un elenco completo di lavoro gli elementi corretti in NuGet, 2.7.2 visualizzazione di [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
