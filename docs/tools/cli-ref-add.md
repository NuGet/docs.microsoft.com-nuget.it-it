---
title: Comando Aggiungi NuGet CLI
description: Informazioni di riferimento per il nuget.exe Aggiungi comando
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545834"
---
# <a name="add-command-nuget-cli"></a>Comando add (interfaccia della riga di comando di NuGet)

**Si applica a**: pubblicazione del pacchetto &bullet; **le versioni supportate**: 3.3 +

Aggiunge un pacchetto specifico a un'origine di pacchetti non HTTP (una cartella o percorso UNC) in un layout organizzato gerarchicamente, in cui vengono create cartelle per il numero di ID e la versione del pacchetto. Ad esempio:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Durante il ripristino o l'aggiornamento in base all'origine del pacchetto, layout organizzato gerarchicamente offre prestazioni notevolmente migliori.

Per espandere tutti i file nel pacchetto per l'origine del pacchetto di destinazione, usare il `-Expand` passare. Ciò comporta in genere presenti nelle sottocartelle aggiuntive visualizzati nella destinazione, ad esempio `tools` e `lib`.

## <a name="usage"></a>Utilizzo

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

in cui `<packagePath>` è il nome del percorso al pacchetto da aggiungere, e `<sourcePath>` specifica l'origine del pacchetto basato sulla cartella in cui verrà aggiunto il pacchetto. Non sono supportate le origini HTTP.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| Expand | Aggiunge tutti i file nel pacchetto per l'origine del pacchetto. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| Help | Visualizza la Guida informazioni per il comando. |
| NonInteractive | Elimina richieste di input o conferme dell'utente. |
| Verbosity | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
