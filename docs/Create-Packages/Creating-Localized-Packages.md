---
title: Come creare un pacchetto NuGet localizzato | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Informazioni dettagliate sui due modi per creare pacchetti NuGet localizzati, ovvero includendo tutti gli assembly in un singolo pacchetto o pubblicando assembly separati.
keywords: localizzazione di pacchetti NuGet, assembly satellite NuGet, creazione di pacchetti localizzati, convenzioni di localizzazione NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1ce8cff07bf629fcdeeaace901a185f2446b077a
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="creating-localized-nuget-packages"></a>Creazione di pacchetti localizzati NuGet

Le versioni localizzate di una libreria possono essere create in due modi:

1. Includere tutti gli assembly di risorse localizzate in un singolo pacchetto.
1. Creare pacchetti satellite localizzati separati (NuGet 1.8 e versioni successive), in base a una serie di rigide convenzioni.

Entrambi i metodi presentano vantaggi e svantaggi, illustrati nelle sezioni seguenti.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Assembly di risorse localizzate in un singolo pacchetto

Includere gli assembly di risorse localizzate in un singolo pacchetto è in genere l'approccio più semplice. A questo scopo, creare in `lib` cartelle per la lingua supportata diversa da quella predefinita del pacchetto (presumendo che sia en-us). In queste cartelle è possibile inserire assembly di risorse e file XML IntelliSense localizzati.

La struttura di cartelle seguente, ad esempio, supporta tedesco (de), italiano (it), giapponese (ja), russo (ru), cinese (semplificato) (zh-Hans) e cinese (tradizionale) (zh-Hant):

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

È possibile osservare che tutte le lingue sono elencate sotto la cartella del framework di destinazione `net40`. Se si [supportano più framework](../create-packages/supporting-multiple-target-frameworks.md), si avrà una cartella sotto `lib` per ogni variante.

Con queste cartelle si può quindi fare riferimento a tutti i file presenti in `.nuspec`:

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

Un pacchetto di esempio che usa questo approccio è [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Vantaggi e svantaggi (assembly di risorse localizzati)

La creazione di bundle che includono tutte le lingue in un singolo pacchetto presenta alcuni svantaggi:

1. **Metadati condivisi**: poiché un pacchetto NuGet può contenere un solo file `.nuspec`, è possibile fornire i metadati per una sola lingua, ovvero NuGet non supporta i metadati localizzati.
1. **Dimensioni del pacchetto**: a seconda del numero di lingue supportate, le dimensioni della libreria possono aumentare considerevolmente e rallentare di conseguenza l'installazione e il ripristino del pacchetto.
1. **Rilasci simultanei**: quando si creano bundle che includono i file localizzati in un solo pacchetto, è necessario rilasciare tutti gli asset di tale pacchetto simultaneamente e non è possibile rilasciare separatamente ogni localizzazione. Qualsiasi aggiornamento di qualsiasi localizzazione, inoltre, richiede una nuova versione dell'intero pacchetto.

Esistono tuttavia anche alcuni vantaggi:

1. **Semplicità**: gli utenti del pacchetto ottengono tutte le lingue supportate in una singola installazione, invece di dover installare separatamente ogni lingua. Un pacchetto singolo è anche più facile da trovare su nuget.org.
1. **Versioni accoppiate**: poiché tutti gli assembly di risorse sono nello stesso pacchetto dell'assembly primario, condividono tutti lo stesso numero di versione e non corrono il rischio di venire erroneamente disaccoppiati.

## <a name="localized-satellite-packages"></a>Pacchetti satellite localizzati

Analogamente al supporto di assembly satellite in .NET Framework, questo metodo separa le risorse localizzate e i file XML IntelliSense in pacchetti satellite.

Il pacchetto primario usa di conseguenza la convenzione di denominazione `{identifier}.{version}.nupkg` e contiene l'assembly per la lingua predefinita (ad esempio, en-US). `ContosoUtilities.1.0.0.nupkg`, ad esempio, conterrà la struttura seguente:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Un assembly satellite usa quindi la convenzione di denominazione `{identifier}.{language}.{version}.nupkg`, ad esempio `ContosoUtilities.de.1.0.0.nupkg`. L'identificatore **deve** corrispondere esattamente a quello del pacchetto primario.

Essendo un pacchetto separato, ha il proprio file `.nuspec` contenente i metadati localizzati. Tenere presente che la lingua in `.nuspec` **deve** corrispondere a quella usata nel nome file.

L'assembly satellite **deve** anche dichiarare una versione esatta del pacchetto primario come dipendenza, usando la notazione di versione []. Vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md). `ContosoUtilities.de.1.0.0.nupkg`, ad esempio, deve dichiarare una dipendenza da `ContosoUtilities.1.0.0.nupkg` usando la notazione `[1.0.0]`. Il pacchetto satellite può ovviamente avere un numero di versione diverso da quello del pacchetto primario.

La struttura del pacchetto satellite deve quindi includere l'assembly di risorse e il file IntelliSense XML in una sottocartella che corrisponde all'elemento `{language}` del nome file del pacchetto:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Nota**: a meno che non siano necessarie impostazioni cultura secondarie specifiche, ad esempio `ja-JP`, usare sempre l'identificatore lingua di livello superiore, ad esempio `ja`.

In un assembly satellite NuGet riconoscerà **solo** i file nella cartella che corrisponde all'elemento `{language}` del nome file. Tutti gli altri vengono ignorati.

Quando tutte queste convenzioni sono soddisfatte, NuGet riconoscerà il pacchetto come pacchetto satellite e installerà i file localizzati nella cartella `lib` del pacchetto primario, come se in origine ne fosse stato creato un bundle. La disinstallazione del pacchetto satellite rimuoverà i file provenienti dalla stessa cartella.

Gli assembly satellite aggiuntivi verranno creati nello stesso modo per ogni lingua supportata. Per un esempio, esaminare il set di pacchetti MVC ASP.NET:

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (inglese primario)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (tedesco)
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (giapponese)
- [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (cinese semplificato)
- [Microsoft.AspNet.Mvc.zh-Hany](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (cinese tradizionale)

### <a name="summary-of-required-conventions"></a>Riepilogo delle convenzioni obbligatorie

- Il pacchetto primario deve essere denominato `{identifier}.{version}.nupkg`
- Un pacchetto satellite deve essere denominato `{identifier}.{language}.{version}.nupkg`
- Il file `.nuspec` di un pacchetto satellite deve specificare la lingua in modo che corrisponda al nome file.
- Un pacchetto satellite deve dichiarare una dipendenza da una versione esatta di quello primario usando la notazione [] nel file `.nuspec`. Gli intervalli non sono supportati.
- Un pacchetto satellite deve inserire i file nella cartella `lib\[{framework}\]{language}` che corrisponde esattamente all'elemento `{language}` del nome file.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Vantaggi e svantaggi (pacchetti satellite)

L'uso di pacchetti satellite presenta alcuni vantaggi:

1. **Dimensioni del pacchetto**: il footprint complessivo del pacchetto primario è ridotto al minimo e agli utenti vengono addebitati solo i costi di ogni lingua che vogliono usare.
1. **Metadati separati**: ogni pacchetto satellite ha il proprio file `.nuspec` e quindi i propri metadati localizzati. In questo modo alcuni utenti possono trovare più facilmente i pacchetti cercando i termini localizzati in nuget.org.
1. **Rilasci disaccoppiati**: gli assembly satellite possono essere rilasciati nel corso del tempo, invece che tutti insieme. In questo modo è possibile distribuire le attività di localizzazione.

I pacchetti satellite tuttavia presentano una serie di svantaggi:

1. **Confusione**: invece di un singolo pacchetto, ne esistono diversi, che possono generare un numero eccessivo di risultati della ricerca su nuget.org e un lungo elenco di riferimenti in un progetto di Visual Studio.
1. **Convenzioni rigide**. I pacchetti satellite devono seguire esattamente le convenzioni, altrimenti le versioni localizzate non verranno selezionate correttamente.
1. **Controllo delle versioni**: ogni pacchetto satellite deve avere una dipendenza della versione esatta dal pacchetto primario. Per aggiornare il pacchetto primario, potrebbe quindi essere necessario aggiornare anche tutti i pacchetti satellite, anche se le risorse non sono state modificate.
