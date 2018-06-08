---
title: Panoramica e flusso di lavoro della creazione di pacchetti NuGet
description: Panoramica del processo di creazione e pubblicazione di un pacchetto NuGet, con collegamenti ad altre parti specifiche del processo.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: 1e2a7299be64d33bd0d697522cf5febb2022e0ee
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817014"
---
# <a name="package-creation-workflow"></a>Flusso di lavoro della creazione di pacchetti

La creazione di un pacchetto ha inizio con la scelta del codice compilato (in genere assembly .NET) che si intende inserire in un pacchetto e condividere con altri utenti, tramite la raccolta nuget.org pubblica o una raccolta privata all'interno dell'organizzazione. Il pacchetto può includere anche file aggiuntivi, ad esempio un file Leggimi da visualizzare quando viene installato il pacchetto, e può includere trasformazioni per determinati file di progetto.

Un pacchetto può essere usato anche solo per eseguire il pull di un numero qualsiasi di altre dipendenze, senza contenere codice proprio. Un pacchetto di questo tipo costituisce una soluzione efficiente per fornire un SDK costituito da più pacchetti indipendenti. In altri casi, un pacchetto può contenere solo file di simboli (con estensione `.pdb`) per supportare il debug.

> [!Note]
> Quando si crea un pacchetto per l'uso da parte di altri sviluppatori, è importante comprendere che si crea anche una dipendenza dal proprio lavoro. In quanto tale, la creazione e la pubblicazione di un pacchetto implica anche un impegno a correggere bug e rilasciare altri aggiornamenti o per lo meno a rendere disponibile il pacchetto come open source in modo che altri utenti possano contribuire alla gestione.

In entrambi i casi, la creazione di un pacchetto ha inizio con la scelta degli assembly e degli altri file da inserire nel pacchetto. Si crea quindi un file manifesto, noto come file `.nuspec`, per descrivere il contenuto del pacchetto insieme al relativo identificatore, al numero di versione, alle informazioni sul copyright, alle proprietà e alle destinazioni MSBuild e molto altro ancora.

Dopo avere preparato tutti i file necessari nelle cartelle appropriate e avere creato il file `.nuspec` appropriato, è possibile usare il comando `nuget pack` (o la [destinazione del pacchetto MSBuild](../reference/msbuild-targets.md)) per assemblare tutti gli elementi in un file `.nupkg`. A questo punto, si è pronti per distribuire il pacchetto in qualsiasi host che lo renda disponibile ad altri sviluppatori.

> [!Tip]
> Un pacchetto NuGet con l'estensione `.nupkg` è semplicemente un file ZIP. Per esaminare facilmente il contenuto di qualsiasi pacchetto, modificarne l'estensione in `.zip` ed espanderne normalmente il contenuto. Assicurarsi di modificare nuovamente l'estensione in `.nupkg` prima di tentare di caricarlo in un host.

Per saperne di più sul processo di creazione, iniziare dall'articolo [Creazione di un pacchetto](../create-packages/creating-a-package.md), che illustra i processi di base comuni a tutti i pacchetti.

Per continuare, sono disponibili diverse altre opzioni per i pacchetti:

- [Supporto di più framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md) descrive come creare un pacchetto con più varianti per diverse versioni di .NET Framework.
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md) descrive come strutturare un pacchetto con più risorse di lingua e come usare pacchetti satellite localizzati distinti.
- [Pacchetti in versione non definitiva](../create-packages/prerelease-packages.md) illustra come rilasciare pacchetti versione alfa, beta e rc ai clienti interessati.
- [Trasformazioni di codice sorgente e file di configurazione](../create-packages/source-and-config-file-transformations.md) descrive come eseguire sostituzioni di token unidirezionali nei file che vengono aggiunti a un progetto e modificare `web.config` e `app.config` con impostazioni che vengono escluse quando si disinstalla il pacchetto.
- [Pacchetti di simboli](../create-packages/symbol-packages.md) offre le informazioni necessarie per fornire simboli per la libreria che consentono ai consumer di eseguire l'istruzione nel codice durante il debug.
- [Controllo delle versioni dei pacchetti](../reference/package-versioning.md) illustra come identificare le versioni esatte consentite per le dipendenze (altri pacchetti utilizzati dal pacchetto).
- [Pacchetti nativi](../create-packages/native-packages.md) descrive il processo di creazione di un pacchetto per i consumer C++.
- [Firma dei pacchetti](../create-packages/sign-a-package.md) descrive il processo per l'aggiunta di una firma digitale a un pacchetto.

Quando si è pronti per pubblicare un pacchetto su nuget.org, seguire la semplice procedura riportata in [Pubblicare un pacchetto](../create-packages/publish-a-package.md).

Se si intende usare un feed privato invece di nuget.org, vedere [Panoramica dell'hosting dei pacchetti](../hosting-packages/overview.md).
