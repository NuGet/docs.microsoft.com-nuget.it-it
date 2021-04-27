---
title: Impostare un tipo di pacchetto NuGet
description: Descrizione dei tipi di pacchetto con indicazione dell'uso previsto.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067278"
---
# <a name="set-a-nuget-package-type"></a>Impostare un tipo di pacchetto NuGet

I pacchetti possono essere contrassegnati con uno o *più tipi di pacchetto* per indicare l'utilizzo previsto.

## <a name="known-package-types"></a>Tipi di pacchetto noti

- I pacchetti di tipo `Dependency` aggiungono asset in fase di compilazione o di esecuzione ad applicazioni e librerie e possono essere installati in qualsiasi tipo di progetto, presupponendo che siano compatibili.

- `DotnetTool` I pacchetti di tipo sono strumenti .NET che possono essere installati dall'interfaccia della [riga di comando dotnet](/dotnet/articles/core/tools/index).

- `Template` I pacchetti di tipo [forniscono modelli](/dotnet/core/tools/custom-templates) personalizzati che possono essere usati per creare file o progetti come un'app, un servizio, uno strumento o una libreria di classi.

I pacchetti non contrassegnati con un tipo, inclusi tutti i pacchetti creati con versioni precedenti di NuGet, usano il tipo `Dependency` per impostazione predefinita.

> [!NOTE]
> Il supporto per i tipi di pacchetto è stato aggiunto in NuGet 3.5.
> Se non è necessario un tipo di pacchetto personalizzato, è meglio non *impostare* in modo esplicito il tipo di pacchetto.
> NuGet viene utilizzato per impostazione `Dependency` predefinita per il tipo quando non viene specificato alcun tipo.

## <a name="custom-package-types"></a>Tipi di pacchetto personalizzati

È possibile contrassegnare il pacchetto con uno o più tipi di pacchetto personalizzati se il relativo utilizzo non corrisponde ai [tipi di pacchetto noti](#known-package-types).

Si supponga, ad esempio, che i clienti `Contoso` dell'app possano installare le estensioni. L'app potrebbe richiedere agli autori di estensioni di usare il tipo di pacchetto personalizzato per identificare i pacchetti come `ContosoExtension` estensioni appropriate che seguono le convenzioni necessarie.

> [!WARNING]
> Un pacchetto con un tipo di pacchetto personalizzato non può essere installato Visual Studio o nuget.exe. Per [altre informazioni, vedere NuGet/Home#10468.](https://github.com/NuGet/Home/issues/10468)

# <a name="using-dotnet-cli"></a>[Uso dell'interfaccia della riga di comando dotnet](#tab/dotnet)

I tipi di pacchetto possono essere impostati nel file di progetto ( `.csproj` ):

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

I pacchetti con più usi specifici possono essere contrassegnati con più tipi di pacchetto usando `;` il delimitatore :

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

È possibile eseguire il controllo delle versioni dei tipi di pacchetto usando un `,` delimitatore tra il tipo di pacchetto e la relativa [`Version`](/dotnet/api/system.version) stringa:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[Uso di nuget.exe](#tab/nugetexe)

I tipi di pacchetto vengono impostati nel `.nuspec` file all'interno `packageTypes\packageType` di un nodo sotto `<metadata>` l'elemento :

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

I pacchetti con più usi specifici possono essere contrassegnati con più tipi di pacchetto:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

È possibile eseguire il controllo delle versioni dei tipi di pacchetto usando una [`Version`](/dotnet/api/system.version) stringa:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

Il formato di una stringa di tipo pacchetto è esattamente come un ID pacchetto. In altri casi, un tipo di pacchetto è una stringa senza distinzione tra maiuscole e minuscole corrispondente all'espressione regolare con almeno un carattere e al massimo `^\w+([_.-]\w+)*$` 100 caratteri.

Se specificato, la versione del tipo di pacchetto è una [`Version`](/dotnet/api/system.version) stringa. La versione del tipo di pacchetto è facoltativa e il valore predefinito è `0.0` .
