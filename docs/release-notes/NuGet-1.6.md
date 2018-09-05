---
title: Note sulla versione 1.6 di NuGet
description: Note sulla versione per NuGet 1.6 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549012"
---
 # <a name="nuget-16-release-notes"></a>Note sulla versione 1.6 di NuGet

[Note sulla versione di NuGet 1.5](../release-notes/nuget-1.5.md) | [note sulla versione di NuGet 1.7](../release-notes/nuget-1.7.md)

NuGet 1.6 è stato rilasciato il 13 dicembre 2011.

## <a name="known-installation-issue"></a>Problema di installazione noti
Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.

Per risolvere il problema è sufficiente disinstallare NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Per altre informazioni, vedere [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Nota: Se Visual Studio non consentirà di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), quindi probabile che sia necessario riavviare Visual Studio tramite "Esegui come amministratore".

## <a name="features"></a>Funzionalità

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Supporto per Versionamento semantico e i pacchetti di versione non definitivo
NuGet 1.6 introduce il supporto per Versionamento semantico (SemVer). Per altre informazioni su come viene utilizzato SemVer, leggere il [documentazione di controllo delle versioni](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Usare NuGet senza il controllo nei pacchetti (ripristino dei pacchetti)
NuGet 1.6 ha ora supporto avanzato per il flusso di lavoro in cui NuGet pacchetti non vengono aggiunti al controllo del codice sorgente, ma invece vengono ripristinati in fase di compilazione se mancante. Per altre informazioni, vedere la [tramite NuGet senza eseguire il commit di pacchetti al controllo del codice sorgente](../consume-packages/packages-and-source-control.md) argomento.

### <a name="item-templates-that-install-nuget-packages"></a>Modelli di elemento di installazione dei pacchetti NuGet
Compila il lavoro per supportare i pacchetti NuGet preinstallati ai modelli di progetto di Visual Studio, NuGet 1.6 aggiunge anche il supporto per i modelli di elemento di Visual Studio. È possibile associare i pacchetti NuGet vengono installati quando viene richiamato il modello in modelli di elemento.

Per altre informazioni su come modificare un modello di progetto/elemento per installare i pacchetti NuGet, vedere la [pacchetti di modelli di Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) argomento.

### <a name="support-for-disabling-package-sources"></a>Supporto per la disabilitazione di origini dei pacchetti
Quando vengono configurate più origini dei pacchetti, NuGet avrà un aspetto in ognuno di essi per i pacchetti durante l'installazione di un pacchetto e le relative dipendenze. Origine pacchetto che non è attivo per qualche motivo possa gravemente rallentare NuGet.

Prima di NuGet 1.6, è possibile rimuovere l'origine del pacchetto, ma è necessario tenere presente i dettagli per quando si desidera aggiungerlo di nuovo.

NuGet 1.6 consente deselezionando un'origine pacchetto per disabilitarla, ma deve rimanere disponibile.

![La disabilitazione di un pacchetto](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 1.6 era un totale di 106 fisso di elementi di lavoro. 95 di questi sono stati classificati sotto forma di bug e 10 di quelli erano le funzionalità.

Per un elenco completo di lavoro gli elementi corretti in NuGet 1.6, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
