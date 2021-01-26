---
title: Note sulla versione di NuGet 1,6
description: Note sulla versione per NuGet 1,6, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777016"
---
 # <a name="nuget-16-release-notes"></a>Note sulla versione di NuGet 1,6

Note sulla versione di [NuGet 1,5](../release-notes/nuget-1.5.md)  |  [Note sulla versione di NuGet 1,7](../release-notes/nuget-1.7.md)

NuGet 1,6 è stato rilasciato il 13 dicembre 2011.

## <a name="known-installation-issue"></a>Problema di installazione noto
Se si esegue VS 2010 SP1, potrebbe essere rilevato un errore di installazione quando si tenta di aggiornare NuGet se è installata una versione precedente.

La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Per altre informazioni, vedere <https://support.microsoft.com/kb/2581019>.

Nota: se Visual Studio non consente di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), probabilmente è necessario riavviare Visual Studio usando "Esegui come amministratore".

## <a name="features"></a>Funzionalità

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Supporto per i pacchetti di versioni non definitive e semantiche
NuGet 1,6 introduce il supporto per il controllo delle versioni semantico (SemVer). Per ulteriori informazioni sull'utilizzo di SemVer, vedere la [documentazione relativa al controllo delle versioni](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Uso di NuGet senza archiviare i pacchetti (ripristino dei pacchetti)
NuGet 1,6 dispone ora del supporto di prima classe per il flusso di lavoro in cui i pacchetti NuGet non vengono aggiunti al controllo del codice sorgente, ma vengono ripristinati in fase di compilazione se mancanti. Per altri dettagli, vedere l'argomento [uso di NuGet senza eseguire il commit dei pacchetti nel controllo del codice sorgente](../consume-packages/packages-and-source-control.md) .

### <a name="item-templates-that-install-nuget-packages"></a>Modelli di elemento che installano pacchetti NuGet
Basandosi sul lavoro per supportare il pacchetto NuGet preinstallato nei modelli di progetto di Visual Studio, NuGet 1,6 aggiunge anche il supporto per i modelli di elemento di Visual Studio. Ai modelli di elemento possono essere associati pacchetti NuGet installati quando il modello viene richiamato.

Per altri dettagli su come modificare un modello di progetto o di elemento per installare i pacchetti NuGet, vedere l'argomento [pacchetti in modelli di Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) .

### <a name="support-for-disabling-package-sources"></a>Supporto per la disabilitazione delle origini dei pacchetti
Quando vengono configurate più origini di pacchetti, NuGet cercherà i pacchetti durante l'installazione di un pacchetto e le relative dipendenze. Un'origine del pacchetto inattiva per qualche motivo può rallentare gravemente NuGet.

Prima di NuGet 1,6, era possibile rimuovere l'origine del pacchetto, ma è necessario ricordare i dettagli relativi al momento in cui si vuole aggiungerlo di nuovo.

NuGet 1,6 consente di deselezionare un'origine del pacchetto per disabilitarla, ma è possibile mantenerla.

![Disabilitazione di un pacchetto](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 1,6 aveva un totale di 106 elementi di lavoro corretti. 95 di questi elementi sono stati classificati come bug e 10 di questi sono funzionalità.

Per un elenco completo degli elementi di lavoro corretti in NuGet 1,6, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
