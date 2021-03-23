---
title: Selezionare gli assembly cui i progetti fanno riferimento
description: Rendere un subset di assembly nel pacchetto disponibile per il compilatore mentre tutti gli assembly sono disponibili al runtime.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859031"
---
# <a name="select-assemblies-referenced-by-projects"></a>Selezionare gli assembly cui i progetti fanno riferimento

I riferimenti espliciti agli assembly consentono a un subset di assembly di essere usato per IntelliSense e per la compilazione mentre tutti gli assembly sono disponibili per il runtime. `PackageReference` e `packages.config` funzionano in modo diverso e di conseguenza gli autori di pacchetti devono fare attenzione a creare il pacchetto in modo che sia compatibile con entrambi i tipi di progetto.

> [!Note]
> I riferimenti espliciti agli assembly sono correlati ad assembly .NET. Non è un metodo per distribuire assembly nativi chiamati tramite PInvoke da un assembly gestito.

## <a name="packagereference-support"></a>Supporto di `PackageReference`

Quando un progetto usa un pacchetto con `PackageReference` e il pacchetto contiene una directory `ref\<tfm>\`, NuGet classificherà tali assembly come asset di compilazione, mentre gli assembly `lib\<tfm>\` sono classificati come asset di runtime. Gli assembly in `ref\<tfm>\` non vengono usati al runtime. Ciò significa che qualsiasi assembly in `ref\<tfm>\` deve avere un assembly corrispondente in `lib\<tfm>\` o in una directory `runtime\` pertinente, in caso contrario potrebbero verificarsi errori di runtime. Poiché gli assembly in `ref\<tfm>\` non vengono usati al runtime, possono essere [assembly di soli metadati](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) in modo da ridurre le dimensioni del pacchetto.

> [!Important]
> Se un pacchetto contiene l'elemento `<references>` nuspec (usato da `packages.config`, vedere di seguito) e non contiene assembly in `ref\<tfm>\`, NuGet annuncerà gli assembly elencati nell'elemento `<references>` nuspec sia come asset di compilazione che come asset di runtime. Ciò significa che vi saranno eccezioni di runtime quando gli assembly cui si fa riferimento dovranno caricare qualsiasi altro assembly nella directory `lib\<tfm>\`.

> [!Note]
> Se il pacchetto contiene una directory `runtime\`, NuGet non può usare gli asset nella directory `lib\`.

## <a name="packagesconfig-support"></a>Supporto di `packages.config`

I progetti che usano `packages.config` per gestire i pacchetti NuGet in genere aggiungono riferimenti a tutti gli assembly nella directory `lib\<tfm>\`. La directory `ref\` è stata aggiunta per supportare `PackageReference` e pertanto non viene considerata quando si usa `packages.config`. Per impostare in modo esplicito gli assembly a cui viene fatto riferimento per i progetti che utilizzano `packages.config` , il pacchetto deve utilizzare l' [ `<references>` elemento nel file nuspec](../reference/nuspec.md#explicit-assembly-references). Ad esempio:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> Il progetto `packages.config` usa un processo denominato [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) per copiare gli assembly nella directory di output `bin\<configuration>\`. L'assembly del progetto viene copiato, il sistema di compilazione esamina il manifesto dell'assembly per individuare gli assembly di riferimento e quindi copia gli assembly e ripete l'operazione in modo ricorsivo per tutti gli assembly. Questo significa che se uno degli assembly nella directory `lib\<tfm>\` non è elencato come una dipendenza nel manifesto di qualsiasi altro assembly (se l'assembly viene caricato al runtime usando `Assembly.Load`, MEF o un altro framework di inserimento delle dipendenze), potrebbe non essere copiato nella directory di output `bin\<configuration>\` del progetto pur trovandosi in `bin\<tfm>\`.

## <a name="example"></a>Esempio

Il pacchetto conterrà tre assembly, `MyLib.dll`, `MyHelpers.dll` e `MyUtilities.dll`, destinati a .NET Framework 4.7.2. `MyUtilities.dll` contiene le classi destinate a essere usate solo dagli altri due assembly, pertanto l'utente non vuole che le classi vengano rese disponibili in IntelliSense o in fase di compilazione per i progetti che usano il pacchetto. Il file `nuspec` deve contenere gli elementi XML seguenti:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

e i file nel pacchetto saranno i seguenti:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
