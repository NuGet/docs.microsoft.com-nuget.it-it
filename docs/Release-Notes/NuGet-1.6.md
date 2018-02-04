---
title: Note sulla versione 1.6 NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 1.6 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "1.6 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
 # <a name="nuget-16-release-notes"></a>Note sulla versione 1.6 di NuGet

[Note sulla versione 1.5 NuGet](../release-notes/nuget-1.5.md) | [note sulla versione 1.7 di NuGet](../release-notes/nuget-1.7.md)

1.6 NuGet è stato rilasciato il 13 dicembre 2011.

## <a name="known-installation-issue"></a>Problema di installazione noti
Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.

La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Per altre informazioni, vedere [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Nota: Se Visual Studio non consente di disinstallare l'estensione (il pulsante di disinstallazione è disabilitato), quindi probabile che sia necessario riavviare Visual Studio utilizzando "Esegui come amministratore".

## <a name="features"></a>Funzionalità

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Supporto per il controllo delle versioni semantico e pacchetti della versione provvisoria
1.6 NuGet introduce il supporto per il controllo delle versioni semantico (SemVer). Per altre informazioni su come viene utilizzato SemVer, leggere la [documentazione di controllo delle versioni](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Uso di NuGet senza l'archiviazione di pacchetti (ripristino del pacchetto)
1.6 NuGet dispone ora di prima classe supporto per il flusso di lavoro in cui NuGet pacchetti non vengono aggiunti al controllo del codice sorgente, ma invece vengono ripristinati in fase di compilazione se mancante. Per altre informazioni, leggere la [tramite NuGet senza eseguire il commit di pacchetti di controllo del codice sorgente](../consume-packages/packages-and-source-control.md) argomento.

### <a name="item-templates-that-install-nuget-packages"></a>Modelli di elementi che consentono di installare i pacchetti NuGet
Compila il lavoro per supportare pacchetto NuGet preinstallato a modelli di progetto di Visual Studio, 1.6 NuGet aggiunge anche il supporto per i modelli di elemento di Visual Studio. Modelli di elemento possono essere associate a pacchetti NuGet a cui vengono installati quando il modello nella richiamata.

Per altre informazioni su come modificare un modello di progetto/elemento per installare i pacchetti NuGet, leggere la [pacchetti di modelli di Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) argomento.

### <a name="support-for-disabling-package-sources"></a>Supporto per la disabilitazione dell'origine del pacchetto
Quando sono configurate più origini del pacchetto, NuGet avrà un aspetto in ognuno di essi per i pacchetti durante l'installazione di un pacchetto e le relative dipendenze. Origine pacchetto che per qualche motivo può provocare gravi rallentare NuGet non è attivo.

Prima di NuGet 1.6, è possibile rimuovere l'origine del pacchetto, ma è necessario ricordare i dettagli per quando si desidera aggiungerlo nuovamente.

1.6 NuGet consente di deselezionare per disabilitarlo, mantenendolo intorno a un'origine del pacchetto.

![La disabilitazione di un pacchetto](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correzioni di bug
1.6 NuGet era un totale di 106 fissati di elementi di lavoro. 95 di questi sono stati classificati come bug e 10 di questi sono funzionalità.

Per un elenco completo di lavoro gli elementi corretti in NuGet 1.6,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
