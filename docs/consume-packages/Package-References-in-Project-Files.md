---
title: Formato PackageReference NuGet (riferimenti a pacchetti nei file di progetto)
description: Informazioni dettagliate su PackageReference NuGet nei file di progetto, come supportato da NuGet 4.0 +, Visual Studio 2017 e .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 61f447877459764906cf9a2b88b32a8bc0553689
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817671"
---
# <a name="package-references-packagereference-in-project-files"></a>Riferimenti a pacchetti (PackageReference) nei file di progetto

I riferimenti ai pacchetti, tramite il nodo `PackageReference`, consentono di gestire le dipendenze di NuGet direttamente all'interno di file di progetto, invece di dover ricorrere a un file `packages.config` separato. L'uso di PackageReference non influenza altri aspetti di NuGet. Ad esempio le impostazioni nei file `NuGet.Config` (incluse le origini dei pacchetti) vengono comunque applicate come illustrato in [Configurazione del comportamento di NuGet](configuring-nuget-behavior.md).

Con PackageReference è anche possibile usare condizioni MSBuild per scegliere i riferimenti ai pacchetti in base a framework di destinazione, configurazione, piattaforma o altri raggruppamenti. Consente anche un controllo più capillare delle dipendenze e del flusso del contenuto. (Per altri dettagli, vedere [Pack e restore di NuGet come destinazioni MSBuild ](../reference/msbuild-targets.md).)

Per impostazione predefinita, PackageReference viene usato per i progetti .NET Core, i progetti .NET Standard e i progetti UWP destinati a Windows 10 Build 15063 (Creators Update) e versioni successive, con l'eccezione dei progetti UWP C++. I progetti .NET Framework completi supportano PackageReference, ma usano attualmente `packages.config` per impostazione predefinita. Per usare PackageReference, eseguire la migrazione delle dipendenze da `packages.config` nel file di progetto e quindi rimuovere packages.config.

## <a name="adding-a-packagereference"></a>Aggiunta di PackageReference

Aggiungere una dipendenza nel file di progetto usando la sintassi seguente:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Controllo della versione della dipendenza

La convenzione per specificare la versione di un pacchetto è uguale quando si usa `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Nell'esempio precedente, 3.6.0 significa qualsiasi versione > = 3.6.0 con preferenza per la versione più bassa, come descritto in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Uso di PackageReference per un progetto senza PackageReference
Avanzato: se non si hanno pacchetti installati in un progetto (nessun PackageReference nel file di progetto e nessun file packages.config), ma si vuole ripristinare il progetto con stile PackageReference, è possibile impostare una proprietà del progetto RestoreProjectStyle su PackageReference nel file di progetto.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
Questa opzione può essere utile se si fa riferimento a progetti con stile PackageReference (progetti con stile SDK o csproj esistenti). In questo modo, sarà possibile fare riferimento "in modo transitivo" dal progetto ai pacchetti a cui fanno riferimento tali progetti.

## <a name="floating-versions"></a>Versioni mobili

Le [versioni mobili](../consume-packages/dependency-resolution.md#floating-versions) sono supportate con `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Controllo degli asset delle dipendenze

È possibile che si usi una dipendenza esclusivamente come strumento di sviluppo e che non si voglia esporla nei progetti che utilizzano il pacchetto. In questo scenario, è possibile usare i metadati `PrivateAssets` per controllare questo comportamento.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

I tag di metadati seguenti controllano gli asset delle dipendenze:

| Tag | Descrizione | Valore predefinito |
| --- | --- | --- |
| IncludeAssets | Questi asset verranno utilizzati | tutti |
| ExcludeAssets | Questi asset non verranno utilizzati | none |
| PrivateAssets | Questi asset verranno utilizzati, ma non verranno trasferiti al progetto padre | contentfiles;analyzers;build |

I valori consentiti per questi tag sono i seguenti, con più valori separati da un punto e virgola, ad eccezione di `all` e `none` che devono essere usati da soli:

| Valore | Descrizione |
| --- | ---
| compile | Contenuti della cartella `lib`. Controlla se il progetto può essere compilato in base agli assembly nella cartella |
| runtime | Contenuti delle cartelle `lib` e `runtimes`. Controlla se questi assembly verranno copiati nella directory di output build |
| contentFiles | Contenuto della cartella `contentfiles` |
| build | Proprietà e destinazioni nella cartella `build` |
| analyzers | Analizzatori .NET |
| native | Contenuto della cartella `native` |
| none | Non viene usato alcuno dei valori precedenti. |
| tutti | Tutti i valori precedenti (ad eccezione di `none`) |

Nell'esempio seguente, il progetto utilizzerà tutti gli elementi tranne i file di contenuto dal pacchetto e tutti gli elementi, tranne gli analizzatori e i file di contenuto, verranno trasferiti al progetto padre.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Si noti che dato che `build` non è incluso in `PrivateAssets`, le destinazioni e le proprietà *verranno trasferite* al progetto padre. Si consideri, ad esempio, che il riferimento precedente viene usato in un progetto che compila un pacchetto NuGet chiamato AppLogger. AppLogger può utilizzare le destinazioni e le proprietà da `Contoso.Utility.UsefulStuff`, analogamente ai progetti che utilizzano AppLogger.

## <a name="adding-a-packagereference-condition"></a>Aggiunta di una condizione PackageReference

È possibile usare una condizione per controllare se un pacchetto è incluso e le condizioni possono usare qualsiasi variabile di MSBuild o una variabile definita nel file delle destinazioni o delle proprietà. Tuttavia, attualmente è supportata solo la variabile `TargetFramework`.

Ad esempio, si supponga di usare `netstandard1.4` e `net452` come destinazione, ma di avere una dipendenza applicabile solo per `net452`. In questo caso non si vuole che un progetto `netstandard1.4` che utilizza il pacchetto aggiunta tale dipendenza non necessaria. Per evitarlo, è possibile specificare una condizione in `PackageReference` come segue:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Un pacchetto compilato con questo progetto indicherà che Newtonsoft.json è incluso come dipendenza solo per una destinazione `net452`:

![Risultato dell'applicazione di una condizione per PackageReference con VS2017](media/PackageReference-Condition.png)

Le condizioni possono essere applicate anche al livello `ItemGroup` e verranno applicate a tutti gli elementi `PackageReference` figlio:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
