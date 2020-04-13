---
title: Risoluzione delle dipendenze dei pacchetti NuGet
description: Dettagli del processo tramite cui le dipendenze di un pacchetto NuGet vengono risolte e installate in NuGet 2.x e NuGet 3.x+.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 4b95251e4b055523a9533b4125589b2650be932d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428828"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Risoluzione delle dipendenze dei pacchetti in NuGet

Ogni volta che un pacchetto viene installato o reinstallato, compresa l'installazione nell'ambito di un processo di [ripristino](../consume-packages/package-restore.md), NuGet installa anche eventuali altri pacchetti da cui dipende questo primo pacchetto.

Tali dipendenze immediate potrebbero quindi avere anche dipendenze proprie, che possono continuare fino a una profondità arbitraria. Ciò produce un cosiddetto *grafico dipendenze*, che descrive le relazioni tra i pacchetti a tutti i livelli.

Quando più pacchetti hanno la stessa dipendenza, lo stesso ID di pacchetto può essere visualizzato nel grafico più volte, potenzialmente con limitazioni delle versioni diverse. Tuttavia, solo una versione di un determinato pacchetto può essere usata in un progetto, pertanto NuGet deve scegliere quale versione usare. Il processo esatto dipende dal formato di gestione dei pacchetti in uso.

## <a name="dependency-resolution-with-packagereference"></a>Risoluzione delle dipendenze con PackageReference

Quando si installano pacchetti in progetti usando il formato PackageReference, NuGet aggiunge riferimenti a un grafico di pacchetto semplice nel file appropriato e risolve i conflitti in anticipo. Questo processo è noto come *ripristino transitivo*. La reinstallazione o il ripristino dei pacchetti è quindi un processo di download dei pacchetti elencati nel grafico, che genera compilazioni più veloci e più prevedibili. È inoltre possibile sfruttare le versioni mobili, ad esempio 2.8.You can also take advantage of floating versions, such as 2.8. \*, per evitare di modificare il progetto per utilizzare la versione più recente di un pacchetto.

Quando il processo di ripristino di NuGet viene eseguito prima di una compilazione, risolve prima le dipendenze in memoria, quindi scrive il grafico risultante in un file denominato `project.assets.json`. Scrive anche le dipendenze risolte in un file di blocco denominato `packages.lock.json`, se la [funzionalità di file di blocco è abilitata](../consume-packages/package-references-in-project-files.md#locking-dependencies).
Il file di asset si trova in `MSBuildProjectExtensionsPath`, che per impostazione predefinita corrisponde alla cartella "obj" del progetto. MSBuild legge quindi questo file e lo converte in un set di cartelle in cui sono disponibili riferimenti potenziali, aggiungendoli quindi all'albero del progetto in memoria.

Il file `project.assets.json` è temporaneo e non deve essere aggiunto al controllo del codice sorgente. Viene elencato per impostazione predefinita in `.gitignore` e `.tfignore`. Vedere [Pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Regole per la risoluzione delle dipendenze

Il ripristino transitivo applica quattro regole principali per risolvere le dipendenze: versione più bassa applicabile, versioni mobili, prevalenza della versione più vicina e dipendenze prossime.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Versione più bassa applicabile

La regola della versione più bassa applicabile ripristina la versione più bassa possibile di un pacchetto come definito dalle relative dipendenze. Si applica anche alle dipendenze per l'applicazione o la libreria di classi a meno che non siano dichiarate [mobili](#floating-versions).

Nella figura seguente, ad esempio, la versione beta 1.0 viene considerata inferiore alla versione 1.0, pertanto NuGet sceglie la versione 1.0:

![Scelta della versione più bassa applicabile](media/projectJson-dependency-1.png)

Nella figura successiva la versione 2.1 non è disponibile nel feed ma dal momento che la limitazione per la versione è >=2.1, NuGet sceglie la versione più bassa successiva che riesce a trovare, in questo caso la versione 2.2:

![Scelta della versione più bassa successiva disponibile nel feed](media/projectJson-dependency-2.png)

Quando un'applicazione specifica un numero di versione esatto, ad esempio 1.2, che non è disponibile nel feed, NuGet genera un errore durante il tentativo di installare o ripristinare il pacchetto:

![NuGet genera un errore quando non è disponibile un numero di versione esatto del pacchetto](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-versions"></a>Versioni mobili

Una versione a virgola mobile \* viene specificata con il carattere. Ad esempio: `6.0.*`. Questa specifica di versione dice "utilizzare l'ultima versione 6.0.x"; `4.*` significa "usare l'ultima versione 4.x". L'uso di una versione mobile riduce le modifiche al file di progetto, mantenendosi aggiornato con la versione più recente di una dipendenza.

Quando si usa una versione mobile, NuGet risolve la versione più `6.0.*` alta di un pacchetto che corrisponde al modello di versione, ad esempio ottiene la versione più alta di un pacchetto che inizia con 6.0:When using a floating version, NuGet resolves the highest version of a package that matches the version pattern, for example gets the highest version of a package that starts with 6.0:

![Scelta della versione 6.0.1 quando è richiesta una versione mobile 6.0.*](media/projectJson-dependency-4.png)

> [!Note]
> Per informazioni sul comportamento delle versioni mobili e delle versioni non definitive, vedere [Controllo delle versioni dei pacchetti](package-versioning.md#version-ranges).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Prevalenza della versione più vicina

Quando il grafico di pacchetto per un'applicazione contiene versioni diverse dello stesso pacchetto, NuGet sceglie il pacchetto più vicino all'applicazione nel grafico e ignora tutti gli altri. Questo comportamento consente a un'applicazione di eseguire l'override di qualsiasi versione del pacchetto specifica nel grafico dipendenze.

Nell'esempio seguente l'applicazione dipende direttamente dal pacchetto B con una limitazione della versione di >=2.0. L'applicazione dipende inoltre dal pacchetto A, che dipende a sua volta anche dal pacchetto B, ma con una limitazione di >=1.0. Poiché la dipendenza dal pacchetto B 2.0 è più vicina all'applicazione nel grafico, viene usata tale versione:

![Applicazione che usa la regola di prevalenza della versione più vicina](media/projectJson-dependency-5.png)

>[!Warning]
> La regola di prevalenza della versione più vicina può comportare un downgrade della versione del pacchetto, interrompendo pertanto potenzialmente altre dipendenze nel grafico. Di conseguenza questa regola viene applicata con un avviso per informare l'utente.

Questa regola comporta inoltre una maggiore efficienza con un grafico dipendenze di grandi dimensioni (come quelli con i pacchetti BCL) poiché una volta che una dipendenza specificata viene ignorata, NuGet ignora anche tutte le dipendenze rimanenti in quel ramo del grafico. Nel diagramma seguente, ad esempio, dal momento che viene usato il pacchetto C 2.0, NuGet ignora qualsiasi ramo nel grafico che faccia riferimento a una versione precedente del pacchetto C:

![Quando NuGet ignora un pacchetto nel grafico, ignora l'intero ramo](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Dipendenze prossime

Quando versioni diverse di un pacchetto vengono definite alla stessa distanza dall'applicazione nel grafico, NuGet usa la versione più bassa che soddisfa tutti i requisiti di versione (come con le regole della [versione più bassa applicabile](#lowest-applicable-version) e delle [versioni mobili](#floating-versions)). Nell'immagine seguente, ad esempio, la versione 2.0 del pacchetto B soddisfa l'altra limitazione >=1.0 e pertanto viene usata:

![Risoluzione delle dipendenze prossime tramite l'uso della versione più bassa che soddisfa tutte le limitazioni](media/projectJson-dependency-7.png)

In alcuni casi non è possibile soddisfare tutti i requisiti di versione. Come illustrato di seguito, se il pacchetto A richiede esattamente il pacchetto B 1.0 e il pacchetto C richiede il pacchetto B >=2.0, NuGet non riesce a risolvere le dipendenze e restituisce un errore.

![Dipendenze non risolvibili a causa di un requisito di versione esatto](media/projectJson-dependency-8.png)

In questi casi, il consumer di livello superiore (applicazione o pacchetto) deve aggiungere la propria dipendenza diretta dal pacchetto B, in modo che si applichi la regola della [prevalenza della versione più vicina](#nearest-wins).

## <a name="dependency-resolution-with-packagesconfig"></a>Risoluzione delle dipendenze con packages.config

Con `packages.config`, le dipendenze di un progetto vengono scritte in `packages.config` sotto forma di elenco semplice. Anche le eventuali dipendenze di questi pacchetti vengono scritte nello stesso elenco. Quando i pacchetti vengono installati, NuGet può anche modificare il file `.csproj`, `app.config`, `web.config` e altri file singoli.

Con `packages.config`, NuGet tenta di risolvere i conflitti di dipendenza durante l'installazione di ogni singolo pacchetto. Ovvero, se il pacchetto A viene installato e dipende dal pacchetto B e il pacchetto B è già elencato in `packages.config` come dipendenza di un altro elemento, NuGet confronta le versioni del pacchetto B richieste e tenta di trovare una versione che soddisfi tutte le limitazioni delle versioni. In particolare, NuGet seleziona la versione più bassa di *major.minor* che soddisfa le dipendenze.

Per impostazione predefinita, NuGet 2.8 cerca la versione di patch minima (vedere le [note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). È possibile controllare questa impostazione tramite l'attributo `DependencyVersion` in `Nuget.Config` e l'opzione `-DependencyVersion` della riga di comando.  

Il processo `packages.config` per la risoluzione delle dipendenze diventa complicato per grafici delle dipendenze di dimensioni più elevate. Ogni nuova installazione del pacchetto richiede un attraversamento dell'intero grafico e genera probabilità di conflitti di versione. Quando si verifica un conflitto, l'installazione viene interrotta, lasciando il progetto in uno stato indeterminato, in particolare con potenziali modifiche al file di progetto stesso. Questo non è un problema quando si usano altri formati di gestione dei pacchetti.

## <a name="managing-dependency-assets"></a>Gestione degli asset delle dipendenze

Quando si usa il formato PackageReference, è possibile controllare quali asset dalle dipendenze vengono inseriti nel progetto di primo livello. Per informazioni dettagliate, vedere [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Quando il progetto di primo livello è un pacchetto, è anche possibile avere il controllo di questo flusso usando gli attributi `include` e `exclude` con le dipendenze elencate nel file `.nuspec`. Vedere la [sezione Dipendenze delle informazioni di riferimento sul file .nuspec](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Esclusione dei riferimenti

Esistono scenari in cui agli assembly con lo stesso nome potrebbe essere fatto riferimento più volte in un progetto, generando errori in fase di progettazione e in fase di compilazione. Si consideri un progetto che contiene una versione personalizzata di `C.dll` e che fa riferimento al pacchetto C contenente anche `C.dll`. Al tempo stesso, il progetto dipende anche dal pacchetto B, che dipende anche dal pacchetto C e da `C.dll`. Di conseguenza, NuGet non riesce a determinare quale `C.dll` usare, ma è possibile rimuovere semplicemente la dipendenza del progetto dal pacchetto C perché anche il pacchetto B dipende da esso.

Per risolvere questa situazione, è necessario fare riferimento direttamente al `C.dll` desiderato (o usare un altro pacchetto che faccia riferimento a quello giusto) e quindi aggiungere una dipendenza dal pacchetto C che escluda tutti i relativi asset. Questa operazione viene eseguita come indicato di seguito a seconda del formato di gestione dei pacchetti in uso:

- [PackageReference](../consume-packages/package-references-in-project-files.md): aggiungere `ExcludeAssets="All"` nella dipendenza:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: rimuovere il riferimento al pacchetto C (PackageC) dal file `.csproj` in modo che faccia riferimento solo alla versione di `C.dll` desiderata.
    
## <a name="dependency-updates-during-package-install"></a>Aggiornamenti delle dipendenze durante l'installazione dei pacchetti 

Se una versione della dipendenza è già soddisfatta, la dipendenza non viene aggiornata durante le altre installazioni del pacchetto. Si consideri ad esempio il pacchetto A che dipende dal pacchetto B e specifica 1.0 per il numero di versione. Il repository di origine contiene le versioni 1.0, 1.1 e 1.2 del pacchetto B. Se il pacchetto A è installato in un progetto che contiene già la versione 1.0 del pacchetto B, il pacchetto B 1.0 rimane in uso perché soddisfa il vincolo di versione. Tuttavia, se un pacchetto A richiede la versione 1.1 o versioni successive del pacchetto B, verrà installata la versione 1.2 del pacchetto B. 

## <a name="resolving-incompatible-package-errors"></a>Risoluzione degli errori dei pacchetti incompatibili

Durante un'operazione di ripristino di un pacchetto, potrebbe essere visualizzato un errore analogo a "Uno o più pacchetti non sono compatibili..." o un avviso che un pacchetto "non è compatibile" con il framework di destinazione del progetto.

Questo errore si verifica quando uno o più dei pacchetti a cui si fa riferimento nel progetto non indicano che supportano il framework di destinazione del progetto, vale a dire il pacchetto non contiene una DLL appropriata nella relativa cartella `lib` per un framework di destinazione compatibile con il progetto (vedere [Framework di destinazione](../reference/target-frameworks.md) per un elenco). 

Ad esempio, se un progetto ha come destinazione `netstandard1.6` e si tenta di installare un pacchetto che contiene DLL solo nelle cartelle `lib\net20` e `\lib\net45`, vengono visualizzati messaggi simili al seguente per il pacchetto ed eventualmente i relativi dipendenti:

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

Per risolvere le incompatibilità, eseguire una delle operazioni seguenti:

- Ridestinare il progetto per un framework supportato dai pacchetti da usare.
- Contattare l'autore dei pacchetti e collaborare per aggiungere il supporto per il framework scelto. Nella pagina di presentazione di tutti i pacchetti su [nuget.org](https://www.nuget.org/) è incluso un collegamento **Contact Owners** (Contatta proprietari) a questo scopo.
