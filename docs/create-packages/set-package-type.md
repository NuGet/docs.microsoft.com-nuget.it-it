---
title: Impostare un tipo di pacchetto NuGet
description: Descrizione dei tipi di pacchetto con indicazione dell'uso previsto.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774361"
---
# <a name="set-a-nuget-package-type"></a>Impostare un tipo di pacchetto NuGet

Con NuGet 3.5+, i pacchetti possono essere contrassegnati con uno specifico *tipo di pacchetto* per indicarne l'uso previsto. I pacchetti non contrassegnati con un tipo, inclusi tutti i pacchetti creati con versioni precedenti di NuGet, usano il tipo `Dependency` per impostazione predefinita.

- I pacchetti di tipo `Dependency` aggiungono asset in fase di compilazione o di esecuzione ad applicazioni e librerie e possono essere installati in qualsiasi tipo di progetto, presupponendo che siano compatibili.

- I pacchetti di tipo `DotnetTool` sono estensioni dell'[interfaccia della riga di comando dotnet](/dotnet/articles/core/tools/index) e vengono richiamati dalla riga di comando. Tali pacchetti possono essere installati solo nei progetti .NET Core e non hanno effetto sulle operazioni di ripristino. Per altre informazioni su queste estensioni in base al progetto, vedere la documentazione sull'[estendibilità in .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).

- `Template` i pacchetti di tipi forniscono [modelli personalizzati](/dotnet/core/tools/custom-templates) che possono essere usati per creare file o progetti come un'app, un servizio, uno strumento o una libreria di classi.

- I pacchetti di tipo personalizzato usano un identificatore di tipo arbitrario che è conforme alle stesse regole di formato degli ID dei pacchetti. I tipi diversi da `Dependency` e `DotnetTool`, tuttavia, non vengono riconosciuti da Gestione pacchetti NuGet in Visual Studio.

I tipi di pacchetto vengono impostati nel file `.nuspec`. Per la compatibilità con le versioni precedenti è meglio *non* impostare in modo esplicito il tipo `Dependency` e basarsi invece sul fatto che NuGet presuppone questo tipo quando non viene specificato alcun tipo.

- `.nuspec`: indica il tipo di pacchetto in un nodo `packageTypes\packageType` sotto l'elemento `<metadata>`:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
