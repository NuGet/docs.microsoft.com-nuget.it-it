---
title: Informazioni di riferimento sul file NuGet.Config | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Informazioni di riferimento sul file NuGet.Config, incluse le sezioni config, bindingRedirects, packageRestore, solution e packageSource.
keywords: File NuGet. config, informazioni di riferimento sulla configurazione NuGet, opzioni di configurazione NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: df602cb561a19f0eac085695de80db1fbaa1a313
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="nugetconfig-reference"></a>Informazioni di riferimento su NuGet.config

Il comportamento di NuGet è controllato da impostazioni in diversi file `NuGet.Config`, come descritto in [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md).

`NuGet.Config` è un file XML contenente un nodo `<configuration>` di livello superiore, che contiene a sua volta gli elementi per le sezioni descritte in questo argomento. Ogni sezione contiene zero o più elementi `<add>` con gli attributi `key` e `value`. Vedere il [file di configurazione di esempio](#example-config-file). Per i nomi delle impostazioni non viene fatta distinzione tra maiuscole e minuscole e per i valori si possono usare [variabili di ambiente](#using-environment-variables).

In questo argomento

- [Sezione config](#config-section)
- [Sezione bindingRedirects](#bindingredirects-section)
- [Sezione packageRestore](#packagerestore-section)
- [Sezione solution](#solution-section)
- [Sezioni per le origini dei pacchetti](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [Uso delle variabili di ambiente](#using-environment-variables)
- [File di configurazione di esempio](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Sezione config

Contiene varie impostazioni di configurazione, che possono essere impostate con il [comando `nuget config`](../tools/cli-ref-config.md).

Nota: `dependencyVersion` e `repositoryPath` si applicano solo ai progetti che usano `packages.config`. `globalPackagesFolder` si applica solo ai progetti utilizzando il formato PackageReference.

| Chiave | Valore |
| --- | --- |
| dependencyVersion (solo `packages.config`) | Valore `DependencyVersion` predefinito per l'installazione, il ripristino e l'aggiornamento del pacchetto, quando non viene specificata direttamente l'opzione `-DependencyVersion`. Questo valore viene usato anche dall'interfaccia utente di Gestione pacchetti NuGet. I valori sono `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (progetti che non usano `packages.config`) | Percorso della cartella dei pacchetti globale predefinita. L'impostazione predefinita è `%USERPROFILE%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac/Linux). È possibile usare un percorso relativo nei file `Nuget.Config` specifici del progetto. |
| repositoryPath (solo `packages.config`) | Percorso in cui installare i pacchetti NuGet invece della cartella `$(Solutiondir)/packages` predefinita. È possibile usare un percorso relativo nei file `Nuget.Config` specifici del progetto. |
| defaultPushSource | Identifica l'URL o il percorso dell'origine del pacchetto che deve essere usato come impostazione predefinita se non vengono trovate altre origini di pacchetti per un'operazione. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Impostazioni del proxy da usare per la connessione a origini di pacchetti. `http_proxy` deve essere nel formato `http://<username>:<password>@<domain>`. Le password vengono crittografate e non possono essere aggiunte manualmente. Per `no_proxy`, il valore è un elenco delimitato da virgole di domini per il bypass del server proxy. In alternativa, è possibile usare le variabili di ambiente http_proxy e no_proxy per questi valori. Per altri dettagli, vedere [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (Impostazioni del proxy NuGet) (skolima.blogspot.com). |

**Esempio**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a>Sezione bindingRedirects

Specifica se NuGet esegue o meno i reindirizzamenti di binding automatici quando viene installato un pacchetto.

| Chiave | Valore |
| --- | --- |
| skip | Valore booleano che indica se ignorare i reindirizzamenti di binding automatici. Il valore predefinito è false. |

**Esempio**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Sezione packageRestore

*Ignorata nella versione 2.7+*

Controlla il ripristino dei pacchetti durante le compilazioni.

| Chiave | Valore |
| --- | --- |
| enabled | Valore booleano che indica se NuGet può eseguire il ripristino automatico. È anche possibile impostare la variabile di ambiente `EnableNuGetPackageRestore` con il valore `True` invece di impostare questa chiave nel file di configurazione. |
| automatico | Valore booleano che indica se NuGet deve controllare se mancano pacchetti durante la compilazione. |

**Esempio**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Sezione solution

Controlla se la cartella `packages` di una soluzione è inclusa nel controllo del codice sorgente. Questa sezione funziona solo nei file `Nuget.Config` in una cartella della soluzione.

| Chiave | Valore |
| --- | --- |
| disableSourceControlIntegration | Valore booleano che indica se ignorare la cartella dei pacchetti quando si utilizza il controllo del codice sorgente. Il valore predefinito è false. |

**Esempio**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Sezioni per le origini dei pacchetti

Le sezioni `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` e `disabledPackageSources` interagiscono tutte per configurare il funzionamento di NuGet con i repository dei pacchetti durante le operazioni di installazione, ripristino e aggiornamento.

Il [comando `nuget sources`](../tools/cli-ref-sources.md) viene generalmente usato per gestire queste impostazioni, ad eccezione della sezione `apikeys` che viene gestita con il [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).

Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Elenca tutte le origini di pacchetti note. L'ordine viene ignorato durante le operazioni di ripristino e con qualsiasi progetto utilizzando il formato PackageReference. NuGet rispetta l'ordine delle origini per installare e aggiornare le operazioni con i progetti utilizzando `packages.config`.

| Chiave | Valore |
| --- | --- |
| (nome da assegnare all'origine di pacchetti) | Percorso o URL dell'origine di pacchetti. |

**Esempio**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Archivia i nomi utente e le password per le origini, in genere specificati con le opzioni `-username` e `-password` con `nuget sources`. Le password vengono crittografate per impostazione predefinita, a meno che non venga usata anche l'opzione `-storepasswordincleartext`.

| Chiave | Valore |
| --- | --- |
| nomeutente | Nome utente per l'origine in testo normale. |
| password | Password crittografata per l'origine. |
| cleartextpassword | Password non crittografata per l'origine. |

**Esempio:**

Nel file di configurazione, l'elemento `<packageSourceCredentials>` contiene i nodi figlio per ogni nome di origine applicabile (gli spazi nel nome vengono sostituiti con `_x0020+`). Per le origini denominate "Contoso" e "Test Source", il file di configurazione contiene quanto segue quando si usano password crittografate:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

Quando si usano password non crittografate:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

Archivia le chiavi per le origini che usano l'autenticazione con chiave API, in base alle impostazioni specificate con il [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).

| Chiave | Valore |
| --- | --- |
| (URL di origine) | Chiave API crittografata. |

**Esempio**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Identifica le origini attualmente disabilitate. Può essere vuoto.

| Chiave | Valore |
| --- | --- |
| (nome dell'origine) | Valore booleano che indica se l'origine è disabilitata. |

**Esempio:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(Solo versione 2.x; deprecata nella versione 3.x+)*

Identifica l'origine attualmente attiva o indica l'aggregazione di tutte le origini.

| Chiave | Valore |
| --- | --- |
| (nome dell'origine) o `All` | Se la chiave è il nome di un'origine, il valore è il percorso o l'URL dell'origine. Se `All`, il valore deve essere `(Aggregate source)` per combinare tutte le origini di pacchetti non disabilitate in altro modo. |

**Esempio**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a>Uso delle variabili di ambiente

È possibile usare variabili di ambiente nei valori `NuGet.Config` (NuGet 3.4 +) per applicare le impostazioni in fase di esecuzione.

Ad esempio, se la variabile di ambiente `HOME` in Windows è impostata su `c:\users\username`, il valore di `%HOME%\NuGetRepository` nel file di configurazione viene risolto in `c:\users\username\NuGetRepository`.

In modo analogo, se la variabile `HOME` in Mac/Linux è impostata su `/home/myStuff`, `$HOME/NuGetRepository` nel file di configurazione viene risolto in `/home/myStuff/NuGetRepository`.

Se non viene trovata una variabile di ambiente, NuGet usa il valore letterale dal file di configurazione.

## <a name="example-config-file"></a>File di configurazione di esempio

Di seguito è riportato un file `NuGet.Config` di esempio che illustra una serie di impostazioni:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>
</configuration>
```
