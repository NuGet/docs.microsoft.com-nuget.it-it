---
title: Formato PackageReference NuGet (riferimenti a pacchetti nei file di progetto)
description: Informazioni dettagliate su PackageReference NuGet nei file di progetto, come supportato da NuGet 4.0 +, Visual Studio 2017 e .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237640"
---
# <a name="package-references-packagereference-in-project-files"></a>Riferimenti a pacchetti (PackageReference) nei file di progetto

I riferimenti ai pacchetti, tramite il nodo `PackageReference`, consentono di gestire le dipendenze di NuGet direttamente all'interno di file di progetto, invece di dover ricorrere a un file `packages.config` separato. L'uso di PackageReference non influenza altri aspetti di NuGet. Ad esempio le impostazioni nei file `NuGet.config` (incluse le origini dei pacchetti) vengono comunque applicate come illustrato in [Configurazione comuni di NuGet](configuring-nuget-behavior.md).

Con PackageReference è inoltre possibile utilizzare le condizioni di MSBuild per scegliere i riferimenti ai pacchetti per ogni Framework di destinazione o altri raggruppamenti. Consente anche un controllo più capillare delle dipendenze e del flusso del contenuto. (Per altri dettagli, vedere [Pack e restore di NuGet come destinazioni MSBuild ](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Supporto dei tipi di progetto

Per impostazione predefinita, PackageReference viene usato per i progetti .NET Core, i progetti .NET Standard e i progetti UWP destinati a Windows 10 Build 15063 (Creators Update) e versioni successive, con l'eccezione dei progetti UWP C++. I progetti .NET Framework supportano PackageReference, ma usano attualmente `packages.config` per impostazione predefinita. Per usare PackageReference, [eseguire la migrazione](../consume-packages/migrate-packages-config-to-package-reference.md) delle dipendenze da `packages.config` nel file di progetto, quindi rimuovere packages.config.

Le app ASP.NET destinate a .NET Framework includono solo un [supporto limitato](https://github.com/NuGet/Home/issues/5877) per PackageReference. I tipi di progetto C++ e JavaScript non sono supportati.

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

Nell'esempio precedente, 3.6.0 significa qualsiasi versione > = 3.6.0 con preferenza per la versione più bassa, come descritto in [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md#version-ranges).

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

## <a name="packagereference-and-sources"></a>PackageReference e origini

Nei progetti PackageReference le versioni delle dipendenze transitive vengono risolte in fase di ripristino. Di conseguenza, nei progetti PackageReference è necessario che tutte le origini siano disponibili per tutti i ripristini. 

## <a name="floating-versions"></a>Versioni mobili

Le [versioni mobili](../concepts/dependency-resolution.md#floating-versions) sono supportate con `PackageReference`:

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
| IncludeAssets | Questi asset verranno utilizzati | all |
| ExcludeAssets | Questi asset non verranno utilizzati | Nessuno |
| PrivateAssets | Questi asset verranno utilizzati, ma non verranno trasferiti al progetto padre | contentfiles;analyzers;build |

I valori consentiti per questi tag sono i seguenti, con più valori separati da un punto e virgola, ad eccezione di `all` e `none` che devono essere usati da soli:

| Valore | Descrizione |
| --- | ---
| compile | Contenuti della cartella `lib`. Controlla se il progetto può essere compilato in base agli assembly nella cartella |
| runtime | Contenuti delle cartelle `lib` e `runtimes`. Controlla se questi assembly verranno copiati nella directory di output build |
| contentFiles | Contenuto della cartella `contentfiles` |
| build | `.props` e `.targets` nella cartella `build` |
| buildMultitargeting | *(4.0)* `.props` e `.targets` nella cartella `buildMultitargeting` per più framework di destinazione |
| buildTransitive | *(5.0 +)* `.props` e `.targets` nella cartella `buildTransitive` per gli asset che si propagano in modo transitivo a qualsiasi progetto che gli utilizza. Vedere la pagina delle [funzionalità](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior). |
| analyzers | Analizzatori .NET |
| nativi | Contenuto della cartella `native` |
| Nessuno | Non viene usato alcuno dei valori precedenti. |
| all | Tutti i valori precedenti (ad eccezione di `none`) |

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

> [!NOTE]
> Quando `developmentDependency` è impostato su `true` in un file `.nuspec`, un pacchetto viene contrassegnato come dipendenza solo per lo sviluppo, impedendo in tal modo che il pacchetto venga incluso come dipendenza in altri pacchetti. Con PackageReference *(NuGet 4.8 +)* , questo flag indica anche che gli asset in fase di compilazione verranno esclusi dalla compilazione. Per altre informazioni, vedere [Supporto di DevelopmentDependency per PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

## <a name="adding-a-packagereference-condition"></a>Aggiunta di una condizione PackageReference

È possibile usare una condizione per controllare se un pacchetto è incluso e le condizioni possono usare qualsiasi variabile di MSBuild o una variabile definita nel file delle destinazioni o delle proprietà. Tuttavia, attualmente è supportata solo la variabile `TargetFramework`.

Ad esempio, si supponga di usare `netstandard1.4` e `net452` come destinazione, ma di avere una dipendenza applicabile solo per `net452`. In questo caso non si vuole che un progetto `netstandard1.4` che utilizza il pacchetto aggiunta tale dipendenza non necessaria. Per evitarlo, è possibile specificare una condizione in `PackageReference` come segue:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Un pacchetto compilato con questo progetto indica che Newtonsoft.Json è incluso come dipendenza solo per una destinazione `net452`:

![Risultato dell'applicazione di una condizione per PackageReference con VS2017](media/PackageReference-Condition.png)

Le condizioni possono essere applicate anche al livello `ItemGroup` e verranno applicate a tutti gli elementi `PackageReference` figlio:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Questa funzionalità è disponibile con NuGet **5,0** o versione successiva e con Visual Studio 2019 **16,0** o versione successiva.

A volte è consigliabile fare riferimento a file in un pacchetto da una destinazione MSBuild.
Nei `packages.config` progetti basati, i pacchetti vengono installati in una cartella relativa al file di progetto. In PackageReference, tuttavia, i pacchetti vengono [utilizzati](../concepts/package-installation-process.md) dalla cartella *Global-Packages* , che può variare da computer a computer.

Per colmare tale lacuna, NuGet ha introdotto una proprietà che punta al percorso da cui verrà utilizzato il pacchetto.

Esempio:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

NuGet genera inoltre automaticamente le proprietà per i pacchetti contenenti una cartella degli strumenti.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

Le proprietà di MSBuild e le identità dei pacchetti non hanno le stesse restrizioni, pertanto l'identità del pacchetto deve essere modificata in un nome descrittivo di MSBuild, preceduto dalla parola `Pkg` .
Per verificare il nome esatto della proprietà generata, esaminare il file [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) generato.

## <a name="nuget-warnings-and-errors"></a>Avvisi ed errori di NuGet

*Questa funzionalità è disponibile con NuGet **4,3** o versione successiva e con Visual Studio 2017 **15,3** o versione successiva.*

Per molti scenari di Pack e ripristino, tutti gli avvisi e gli errori di NuGet vengono codificati e iniziano con `NU****` . Tutti gli avvisi e gli errori di NuGet sono elencati nella documentazione di [riferimento](../reference/errors-and-warnings.md) .

NuGet osserva le seguenti proprietà di avviso:

- `TreatWarningsAsErrors`, considera tutti gli avvisi come errori
- `WarningsAsErrors`, considera gli avvisi specifici come errori
- `NoWarn`, nascondere avvisi specifici, sia a livello di progetto che a livello di pacchetto.

Esempi:

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>Eliminazione degli avvisi di NuGet

Sebbene sia consigliabile risolvere tutti gli avvisi di NuGet durante le operazioni di Pack e ripristino, in determinate situazioni la relativa eliminazione è garantita.
Per evitare l'avviso di un intero progetto, provare a eseguire le operazioni seguenti:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

A volte gli avvisi si applicano solo a un determinato pacchetto nel grafico. È possibile scegliere di sopprimere l'avviso in modo più selettivo aggiungendo un oggetto nell' `NoWarn` elemento PackageReference. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Eliminazione degli avvisi del pacchetto NuGet in Visual Studio

In Visual Studio è anche possibile disattivare gli [avvisi](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) tramite l'IDE.

## <a name="locking-dependencies"></a>Blocco delle dipendenze

*Questa funzionalità è disponibile con NuGet **4.9** o versione successiva e con Visual Studio 2017 **15.9** o versione successiva.*

L'input per il ripristino NuGet è un set di riferimenti al pacchetto dal file di progetto (dipendenze dirette o di primo livello) e l'output è una chiusura completa di tutte le dipendenze del pacchetto, incluse le dipendenze transitive. NuGet prova a produrre sempre la stessa chiusura completa di dipendenze del pacchetto se l'elenco PackageReference di input non è stato modificato. Esistono tuttavia alcuni scenari in cui non è possibile farlo. Ad esempio:

* Quando si usano versioni mobili, ad esempio `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. Anche se in questo caso la finalità è il passaggio alla versione più recente a ogni ripristino dei pacchetti, esistono scenari in cui gli utenti richiedono che il grafo venga bloccato su una determinata versione più recente e passi a una versione successiva, se disponibile, in caso di movimento esplicito.
* Viene pubblicata una versione più recente del pacchetto che risponde ai requisiti di versione di PackageReference. ad esempio 

  * Giorno 1: si è specificato `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, ma le versioni disponibili nei repository NuGet erano 4.1.0, 4.2.0 e 4.3.0. In questo caso, NuGet restituirebbe 4.1.0 (la versione minima più vicina)

  * Giorno 2: viene pubblicata la versione 4.0.0. NuGet troverà ora la corrispondenza esatta e inizierà a restituire 4.0.0

* Una versione del pacchetto specifica viene rimossa dal repository. Anche se nuget.org non consente l'eliminazione dei pacchetti, non tutti i repository di pacchetti presentano questo vincolo. NuGet trova di conseguenza la corrispondenza migliore quando non può restituire la versione eliminata.

### <a name="enabling-lock-file"></a>Abilitazione del file di blocco

Per rendere persistente la chiusura completa delle dipendenze del pacchetto, è possibile acconsentire esplicitamente alla funzionalità di file di blocco impostando la proprietà MSBuild `RestorePackagesWithLockFile` per il progetto:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Se questa proprietà viene impostata, il ripristino NuGet genererà un file di blocco, il file `packages.lock.json`, nella directory radice del progetto, che elenca tutte le dipendenze del pacchetto. 

> [!Note]
> Quando nella directory radice di un progetto è presente il file `packages.lock.json`, il file di blocco viene sempre usato con il ripristino anche se la proprietà `RestorePackagesWithLockFile` non è impostata. Un altro modo per acconsentire esplicitamente a questa funzionalità è quindi quello di creare un file `packages.lock.json` fittizio vuoto nella directory radice del progetto.

### <a name="restore-behavior-with-lock-file"></a>Comportamento di `restore` con il file di blocco
Se un file di blocco è presente per il progetto, NuGet lo usa per eseguire `restore`. NuGet esegue un rapido controllo per verificare se sono state apportate modifiche alle dipendenze del pacchetto indicate nel file di progetto (o nei file dei progetti dipendenti) e, se non sono presenti modifiche, si limita a ripristinare i pacchetti indicati nel file di blocco. Non viene eseguita alcuna rivalutazione delle dipendenze del pacchetto.

Se NuGet rileva una modifica nelle dipendenze definite indicate nei file di progetto, rivaluta il grafo del pacchetto e aggiorna il file di blocco in modo da riflettere la nuova chiusura del pacchetto per il progetto.

Per CI/CD e altri scenari in cui non si vogliono modificare le dipendenze del pacchetto immediatamente, è possibile farlo impostando `lockedmode` su `true`:

Per dotnet.exe, eseguire:

```
> dotnet.exe restore --locked-mode
```

Per msbuild.exe, eseguire:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

È anche possibile impostare questa proprietà MSBuild condizionale nel file di progetto:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Se la modalità di blocco è `true`, verranno ripristinati i pacchetti esatti elencati nel file di blocco. Il ripristino avrà invece esito negativo se le dipendenze del pacchetto definite per il progetto sono state aggiornate dopo la creazione del file di blocco.

### <a name="make-lock-file-part-of-your-source-repository"></a>Rendere il file di blocco parte del repository di origine
Se si compila un'applicazione, un file eseguibile e il progetto in questione sono alla inizio della catena di dipendenze, quindi archiviare il file di blocco nel repository di codice sorgente in modo che NuGet possa usarlo durante il ripristino.

Se tuttavia il progetto è un progetto libreria che non viene distribuito o un progetto di codice comune da cui dipendono altri progetti, **non è consigliabile** archiviare il file di blocco come parte del codice sorgente. È possibile mantenere il file di blocco, ma le dipendenze del pacchetto bloccato per il progetto di codice comune, elencate nel file di blocco, non possono essere usate durante il ripristino o la compilazione di un progetto che dipende da questo progetto di codice comune.

Ad esempio:

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Se `ProjectA` ha una dipendenza da `PackageX` versione `2.0.0` e fa anche riferimento a `ProjectB` che dipende da `PackageX` versione `1.0.0`, il file di blocco per `ProjectB` elencherà una dipendenza da `PackageX` versione `1.0.0`. Tuttavia, quando `ProjectA` viene compilato, il file di blocco conterrà una dipendenza dalla `PackageX` versione **`2.0.0`** e **non** `1.0.0` come elencato nel file di blocco per `ProjectB` . Di conseguenza, il file di blocco di un progetto di codice comune ha poca influenza sui pacchetti risolti per i progetti che dipendono da esso.

### <a name="lock-file-extensibility"></a>Estendibilità di file di blocco

È possibile controllare diversi comportamenti di ripristino con file di blocco, come descritto di seguito:

| Opzione NuGet.exe | opzione DotNet | Opzione MSBuild equivalente | Descrizione |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Optare per l'utilizzo di un file di blocco. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Abilita la modalità di blocco per il ripristino. Questa operazione è utile negli scenari CI/CD in cui si desiderano compilazioni ripetibili.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | Questa opzione è utile con i pacchetti con la versione mobile definita nel progetto. Per impostazione predefinita, NuGet Restore non aggiornerà automaticamente la versione del pacchetto a ogni ripristino, a meno che non si esegua Restore con questa opzione. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Definisce un percorso di file di blocco personalizzato per un progetto. Per impostazione predefinita, NuGet supporta `packages.lock.json` nella directory radice. Se nella stessa directory sono presenti più progetti, NuGet supporta il file di blocco `packages.<project_name>.lock.json` specifico del progetto |
