---
title: NuGet CLI verificare comando
description: Informazioni di riferimento per il nuget.exe verificare comando
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545213"
---
# <a name="verify-command-nuget-cli"></a>Comando verify (interfaccia della riga di comando di NuGet)

**Si applica a:** consumo del pacchetto &bullet; **le versioni supportate:** 4.6 e versioni successive

Verifica di un pacchetto.

Verifica dei pacchetti firmati non è ancora supportata in .NET Core, in Mono, o su piattaforme non Windows.

## <a name="usage"></a>Utilizzo

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

in cui `<package(s)>` è uno o più `.nupkg` file.

## <a name="nuget-verify--all"></a>NuGet verifica - tutto

Specifica che tutte le verifiche possibili devono essere eseguite sui pacchetti.

## <a name="nuget-verify--signatures"></a>NuGet verifica - firme

Specifica che deve essere eseguita la verifica della firma del pacchetto.

## <a name="options-for-verify--signatures"></a>Opzioni per "verificare - firme"

| Opzione | Descrizione |
| --- | --- |
| CertificateFingerprint | Specifica uno o più SHA-256 certificato le impronte digitali dei quali pacchetti firmati devono essere firmati con certificati (s). Un'impronta digitale certificato SHA-256 è un hash SHA-256 del certificato. Più input deve essere delimitato da punto e virgola. |

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| ForceEnglishOutput | Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

## <a name="examples"></a>Esempi

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```