---
title: NuGet CLI verificare comando | Documenti Microsoft
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il nuget.exe verificare comando
keywords: Verificare il riferimento, verificare di comando di NuGet
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 2747491eb35d8685a44e86fcc1b572013982c754
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2018
---
# <a name="verify-command-nuget-cli"></a>Verificare di comando (CLI NuGet)

**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** 4.6 +

Verifica di un pacchetto.

## <a name="usage"></a>Utilizzo

```cli
nuget verify <package(s)> [options]
```

dove `<package(s)>` uno o più `.nupkg` file.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Tutti | Specifica che tutte le verifiche possibili devono essere eseguite in per i pacchetti. |
| CertificateFingerprint | Specifica uno o più SHA-256 certificato le impronte digitali di certificati (s), i pacchetti firmati devono essere firmati con. Un'impronta digitale certificato SHA-256 è un hash SHA-256 del certificato. Più input devono essere separati da virgola. |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ForceEnglishOutput | Nuget.exe forza l'esecuzione utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| NonInteractive | Elimina richieste per l'input dell'utente o le conferme. |
| Firme | Specifica che deve essere eseguita la verifica della firma del pacchetto. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

## <a name="examples"></a>Esempi

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```