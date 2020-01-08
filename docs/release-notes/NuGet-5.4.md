---
title: Note sulla versione di NuGet 5,4
description: Note sulla versione per NuGet 5,4, incluse nuove funzionalità, correzioni di bug e DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384111"
---
# <a name="nuget-54-release-notes"></a>Note sulla versione di NuGet 5,4

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core

## <a name="summary-whats-new-in-54"></a>Riepilogo: novità di 5,4

* Tempo di caricamento della soluzione più veloce: il sovraccarico del codice NuGet durante il primo caricamento della soluzione è stato ridotto tramite un NGen parziale per ridurre i costi JIT [#6007](https://github.com/NuGet/Home/issues/6007)

* Nuova funzione helper: dato un elenco di ID e versioni del pacchetto, ottenere i pacchetti di livello superiore probabili. - [#8316](https://github.com/NuGet/Home/issues/8316)

* Nuova azione [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) per l'installazione e la configurazione di NuGet. exe nelle [azioni di GitHub](https://github.com/features/actions). - [#8818](https://github.com/NuGet/Home/issues/8818)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* Plug-in: la precisione dell'ora di registrazione è disattivata in Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)

* L'eliminazione di un plug-in può talvolta generare e interrompere l'intera operazione. - [#8732](https://github.com/NuGet/Home/issues/8732)

* Interrompi la visualizzazione dei duplicati della versione nell'elenco delle versioni consentite e bloccate in PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)

* Il file di blocco non è stato generato correttamente. l'ordinamento del Framework non dovrebbe avere alcun effetto sul ripristino con lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)

* La convalida LockFile non riesce per i progetti con <RuntimeIdentifiers> impostati nell'SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)

* La convalida della firma ora rifiuterà correttamente le firme con timestamp con due valori nello stesso OID- [#8629](https://github.com/NuGet/Home/issues/8629)

* Aggiornare l'elenco di licenze- [#8544](https://github.com/NuGet/Home/issues/8544)

**DCR**

* Onboarding dei file di diagnostica in IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)

**[Elenco di tutti i problemi risolti in questa versione-5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
