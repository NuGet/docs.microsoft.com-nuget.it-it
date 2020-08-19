---
title: Comando di verifica CLI di NuGet
description: Riferimento per il comando nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622603"
---
# <a name="verify-command-nuget-cli"></a>comando Verify (interfaccia della riga di comando di NuGet)

**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 4.6 +

Verifica un pacchetto.

La verifica dei pacchetti firmati non è ancora supportata in .NET Core, in mono o in piattaforme non Windows.

## <a name="usage"></a>Uso

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

dove `<package(s)>` è uno o più `.nupkg` file.

## <a name="nuget-verify--all"></a>Verifica NuGet-tutto

Specifica che tutte le verifiche possibili devono essere eseguite sui pacchetti.

## <a name="nuget-verify--signatures"></a>Verifica NuGet-firme

Specifica che deve essere eseguita la verifica della firma del pacchetto.

## <a name="options-for-verify--signatures"></a>Opzioni per "Verifica-firme"

- **`-CertificateFingerprint`**

  Specifica una o più impronte digitali del certificato SHA-256 dei certificati i cui pacchetti firmati devono essere firmati. Un'impronta digitale SHA-256 del certificato è un hash SHA-256 del certificato. Più input devono essere separati da punto e virgola.

## <a name="options"></a>Opzioni

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

## <a name="examples"></a>Esempi

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```