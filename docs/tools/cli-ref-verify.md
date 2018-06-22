---
title: NuGet CLI verificare comando
description: Riferimento per il nuget.exe verificare comando
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2018
ms.locfileid: "34462852"
---
# <a name="verify-command-nuget-cli"></a>Comando verify (interfaccia della riga di comando di NuGet)

**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** 4.6 +

Verifica di un pacchetto.

Verifica dei pacchetti con segno non è ancora supportata in .NET Core, in Mono o su piattaforme non Windows.

## <a name="usage"></a>Utilizzo

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

dove `<package(s)>` uno o più `.nupkg` file.

## <a name="nuget-verify--all"></a>Verificare che NuGet - tutto

Specifica che tutte le verifiche possibili devono essere eseguite in per i pacchetti.

## <a name="nuget-verify--signatures"></a>Verificare di NuGet - firme

Specifica che deve essere eseguita la verifica della firma del pacchetto.

## <a name="options-for-verify--signatures"></a>Opzioni per "verificare - firme"

| Opzione | Descrizione |
| --- | --- |
| CertificateFingerprint | Specifica uno o più SHA-256 certificato le impronte digitali di certificati (s), i pacchetti firmati devono essere firmati con. Un'impronta digitale certificato SHA-256 è un hash SHA-256 del certificato. Più input devono essere separati da virgola. |

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
| ForceEnglishOutput | Nuget.exe forza l'esecuzione utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

## <a name="examples"></a>Esempi

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```