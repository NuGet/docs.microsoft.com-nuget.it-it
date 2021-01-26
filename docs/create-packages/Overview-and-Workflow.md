---
title: Panoramica e flusso di lavoro della creazione di pacchetti NuGet
description: Panoramica del processo di creazione e pubblicazione di un pacchetto NuGet, con collegamenti ad altre parti specifiche del processo.
author: JonDouglas
ms.author: jodou
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: d34f8e73dce64a58393433637067651fced08173
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774681"
---
# <a name="package-creation-workflow"></a>Flusso di lavoro della creazione di pacchetti

La creazione di un pacchetto ha inizio con la scelta del codice compilato (in genere assembly .NET) che si intende inserire in un pacchetto e condividere con altri utenti, tramite la raccolta nuget.org pubblica o una raccolta privata all'interno dell'organizzazione. Il pacchetto può includere anche file aggiuntivi, ad esempio un file Leggimi da visualizzare quando viene installato il pacchetto, e può includere trasformazioni per determinati file di progetto.

Un pacchetto può essere usato anche solo per eseguire il pull di un numero qualsiasi di altre dipendenze, senza contenere codice proprio. Un pacchetto di questo tipo costituisce una soluzione efficiente per fornire un SDK costituito da più pacchetti indipendenti. In altri casi, un pacchetto può contenere solo file di simboli (con estensione `.pdb`) per supportare il debug.

> [!Note]
> Quando si crea un pacchetto per l'uso da parte di altri sviluppatori, è importante comprendere che si crea anche una dipendenza dal proprio lavoro. In quanto tale, la creazione e la pubblicazione di un pacchetto implica anche un impegno a correggere bug e rilasciare altri aggiornamenti o per lo meno a rendere disponibile il pacchetto come open source in modo che altri utenti possano contribuire alla gestione.

Qualunque sia il caso, la creazione di un pacchetto inizia con la scelta di identificatore, numero di versione, licenza, informazioni sul copyright e altri contenuti necessari. È poi possibile usare il comando "pack" per riunire tutti gli elementi in un file `.nupkg`. Questo file può essere pubblicato in un feed NuGet, ad esempio nuget.org.

> [!Tip]
> Un pacchetto NuGet con l'estensione `.nupkg` è semplicemente un file ZIP. Per esaminare facilmente il contenuto di qualsiasi pacchetto, modificarne l'estensione in `.zip` ed espanderne normalmente il contenuto. Assicurarsi di modificare nuovamente l'estensione in `.nupkg` prima di tentare di caricarlo in un host.

Per saperne di più sul processo di creazione, iniziare dall'articolo [Creazione di un pacchetto](../create-packages/creating-a-package.md), che illustra i processi di base comuni a tutti i pacchetti.

Per continuare, sono disponibili diverse altre opzioni per i pacchetti:

- [Supporto di più framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md) descrive come creare un pacchetto con più varianti per diverse versioni di .NET Framework.
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md) descrive come strutturare un pacchetto con più risorse di lingua e come usare pacchetti satellite localizzati distinti.
- [Pacchetti in versione non definitiva](../create-packages/prerelease-packages.md) illustra come rilasciare pacchetti versione alfa, beta e rc ai clienti interessati.
- [Trasformazioni di codice sorgente e file di configurazione](../create-packages/source-and-config-file-transformations.md) descrive come eseguire sostituzioni di token unidirezionali nei file che vengono aggiunti a un progetto e modificare `web.config` e `app.config` con impostazioni che vengono escluse quando si disinstalla il pacchetto.
- [Pacchetti di simboli](../create-packages/symbol-packages-snupkg.md) offre le informazioni necessarie per fornire simboli per la libreria che consentono ai consumer di eseguire l'istruzione nel codice durante il debug.
- [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md) illustra come identificare le versioni esatte consentite per le dipendenze (altri pacchetti utilizzati dal pacchetto).
- [Pacchetti nativi](../guides/native-packages.md) descrive il processo di creazione di un pacchetto per i consumer C++.
- [Firma dei pacchetti](../create-packages/sign-a-package.md) descrive il processo per l'aggiunta di una firma digitale a un pacchetto.

Quando si è pronti per pubblicare un pacchetto su nuget.org, seguire la semplice procedura riportata in [Pubblicare un pacchetto](../nuget-org/publish-a-package.md).

Se si intende usare un feed privato invece di nuget.org, vedere [Panoramica dell'hosting dei pacchetti](../hosting-packages/overview.md).
