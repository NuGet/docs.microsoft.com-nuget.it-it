---
title: Comando di ricerca dell'interfaccia della riga di comando di NuGet
description: Informazioni di riferimento per il nuget.exe di ricerca
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323661"
---
# <a name="search-command-nuget-cli"></a>Comando search (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo del pacchetto &bullet; **Versioni supportate:** 5.8+

Cerca in un'origine specificata usando la stringa di query fornita. Se non viene specificata alcuna origine, vengono usate tutte le origini definite in %AppData%\NuGet\NuGet.Config.

## <a name="usage"></a>Utilizzo

```cli
nuget search [search terms] [options]
```

in cui i termini di ricerca vengono applicati ai nomi dei pacchetti, dei tag e delle descrizioni dei pacchetti esattamente come quando vengono utilizzati in nuget.org.

## <a name="options"></a>Opzioni

| Nome | Descrizione | Utilizzo |
| ---  |     ---     |  :-:  |
| Preliminare | I pacchetti di versioni non definitiva non sono inclusi per impostazione predefinita, ma possono essere inclusi usando questo argomento | -PreRelease |
| Origine | Origini del pacchetto specifiche in cui eseguire la ricerca anziché eseguire query nelle origini predefinite __nuget.config__ | -Source `<Source URL>`|
| Take | Numero di risultati da restituire. Il valore predefinito è 20. | -Take `<positive integer>` |
| Livello di dettaglio | Livello di dettaglio da visualizzare nell'output. Il valore predefinito è _normale._ (Vedere la nota seguente)  | -Verbosity `<quiet|normal|detailed>` |
| Help | Visualizza le informazioni della Guida per il comando | -Help |

Vedere anche [Variabili di ambiente](cli-ref-environment-variables.md)

> [!NOTE] 
> Livelli di dettaglio:
> * _quiet_ - ID pacchetto, versione
> * _normal_ - ID pacchetto, versione, download, anteprima della descrizione
> * _detailed_ : ID pacchetto, versione, download, descrizione completa, altre informazioni, ad esempio l'URL della query

## <a name="examples"></a>Esempio

Cercare i *pacchetti* correlati alla registrazione dalle origini predefinite:
```
nuget search logging
```
Cercare i *pacchetti* correlati alla registrazione con un livello di dettaglio dettagliato:
```
nuget search logging -Verbosity detailed
```
Cercare i *pacchetti* correlati alla registrazione e visualizzare solo i primi 5 risultati:
```
nuget search logging -Take 5
```
Cercare i pacchetti correlati a *JSON,* incluse le versioni non definitiva, dall'origine/feed specificato:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Cercare pacchetti correlati a *JSON* da più origini/feed:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
