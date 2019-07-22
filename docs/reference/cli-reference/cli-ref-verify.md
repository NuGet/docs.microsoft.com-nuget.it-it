---
title: Comando di verifica CLI di NuGet
description: Informazioni di riferimento sul comando NuGet. exe verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327498"
---
# <a name="verify-command-nuget-cli"></a>Comando verify (interfaccia della riga di comando di NuGet)

**Si applica a:** &bullet; **versioni supportate** per l'utilizzo di pacchetti: 4.6 +

Verifica un pacchetto.

La verifica dei pacchetti firmati non è ancora supportata in .NET Core, in mono o in piattaforme non Windows.

## <a name="usage"></a>Utilizzo

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

dove `<package(s)>` è uno o più `.nupkg` file.

## <a name="nuget-verify--all"></a>Verifica NuGet-tutto

Specifica che tutte le verifiche possibili devono essere eseguite sui pacchetti.

## <a name="nuget-verify--signatures"></a>Verifica NuGet-firme

Specifica che deve essere eseguita la verifica della firma del pacchetto.

## <a name="options-for-verify--signatures"></a>Opzioni per "Verifica-firme"

| Opzione | Descrizione |
| --- | --- |
| CertificateFingerprint | Specifica una o più impronte digitali del certificato SHA-256 dei certificati i cui pacchetti firmati devono essere firmati. Un'impronta digitale SHA-256 del certificato è un hash SHA-256 del certificato. Più input devono essere separati da punto e virgola. |

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| ? | Visualizza le informazioni della Guida per il comando. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

## <a name="examples"></a>Esempi

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```