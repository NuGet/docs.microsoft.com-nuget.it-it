---
title: NuGet CLI aggiungere comandi
description: Riferimento per il nuget.exe Aggiungi comando
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a4201a321ffe0f7fb61f4e98012a1a2d7d8fda4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="add-command-nuget-cli"></a>aggiungere il comando (CLI NuGet)

**Si applica a**: la pubblicazione del pacchetto &bullet; **versioni supportate**: 3.3 +

Aggiunge un pacchetto specifico a un'origine del pacchetto non HTTP (una cartella o un percorso UNC) in un layout organizzato gerarchicamente, in cui vengono create le cartelle per il numero di ID e la versione del pacchetto. Ad esempio:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Durante il ripristino o l'aggiornamento in base all'origine del pacchetto, layout organizzato gerarchicamente fornisce un miglioramento significativo delle prestazioni.

Per espandere tutti i file del pacchetto all'origine del pacchetto di destinazione, utilizzare il `-Expand` passare. Ciò comporta in genere nelle sottocartelle aggiuntive nella destinazione, ad esempio `tools` e `lib`.

## <a name="usage"></a>Utilizzo

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

dove `<packagePath>` sia il percorso per il pacchetto da aggiungere, e `<sourcePath>` specifica l'origine del pacchetto basati sulla cartella in cui verrà aggiunto il pacchetto. Origini HTTP non sono supportate.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
| Expand | Aggiunge tutti i file del pacchetto per l'origine del pacchetto. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
