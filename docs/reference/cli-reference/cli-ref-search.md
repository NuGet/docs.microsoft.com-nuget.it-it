---
title: Comando di ricerca CLI NuGet
description: Riferimento per il comando di ricerca di nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779157"
---
# <a name="search-command-nuget-cli"></a>comando Search (interfaccia della riga di comando di NuGet)

**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 5.8 +

Esegue la ricerca di una determinata origine utilizzando la stringa di query specificata. Se non viene specificata alcuna origine, vengono utilizzate tutte le origini definite in% AppData% \NuGet\NuGet.config.

## <a name="usage"></a>Utilizzo

```cli
nuget search [search terms] [options]
```

dove vengono applicati i termini di ricerca ai nomi di pacchetti, tag e descrizioni del pacchetto come quando si usano in nuget.org.

## <a name="options"></a>Opzioni

| Nome | Descrizione | Utilizzo |
| ---  |     ---     |  :-:  |
| PreRelease | I pacchetti di versioni non definitive non sono inclusi per impostazione predefinita, ma possono essere inclusi usando questo argomento | -Versione preliminare |
| Source (Sorgente) | Origini pacchetti specifiche in cui eseguire la ricerca anziché eseguire query sulle origini predefinite in __nuget.config__ | -Origine `<Source URL>`|
| Take | Numero di risultati da restituire. Il valore predefinito è 20. | -Take `<positive integer>` |
| Livello di dettaglio | Livello di dettaglio da visualizzare nell'output. Il valore predefinito è _Normal_. (Vedere la nota di seguito)  | -Livello di dettaglio `<quiet|normal|detailed>` |
| Guida | Visualizza le informazioni della Guida per il comando | -Guida |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

> [!NOTE] 
> Livelli di dettaglio:
> * _quiet_ -ID pacchetto, versione
> * _normale_ -ID pacchetto, versione, download, anteprima della descrizione
> * _Dettagli_ -ID pacchetto, versione, download, descrizione completa, altre informazioni, ad esempio l'URL della query

## <a name="examples"></a>Esempi

Cercare i pacchetti correlati alla *registrazione* da origini predefinite:
```
nuget search logging
```
Cercare i pacchetti correlati alla *registrazione* con un livello di dettaglio dettagliato:
```
nuget search logging -Verbosity detailed
```
Cercare i pacchetti correlati alla *registrazione* e visualizzare solo i primi 5 risultati:
```
nuget search logging -Take 5
```
Cercare i pacchetti correlati a *JSON*, incluse le versioni non definitive, dall'origine/feed specificati:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Cercare pacchetti correlati a *JSON* da più origini/feed:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
