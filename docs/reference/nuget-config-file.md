---
title: riferimento a un File NuGet. config
description: Informazioni di riferimento sul file NuGet.Config, incluse le sezioni config, bindingRedirects, packageRestore, solution e packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911088"
---
# <a name="nugetconfig-reference"></a>riferimento di NuGet. config

Il comportamento di NuGet è controllato da impostazioni in diversi file `NuGet.Config`, come descritto in [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` è un file XML contenente un nodo `<configuration>` di livello superiore, che contiene a sua volta gli elementi per le sezioni descritte in questo argomento. Ogni sezione contiene zero o più elementi. Vedere il [file di configurazione di esempio](#example-config-file). Per i nomi delle impostazioni non viene fatta distinzione tra maiuscole e minuscole e per i valori si possono usare [variabili di ambiente](#using-environment-variables).

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
- [sezione trustedSigners](#trustedsigners-section)
- [Uso delle variabili di ambiente](#using-environment-variables)
- [File di configurazione di esempio](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Sezione config

Contiene varie impostazioni di configurazione, che possono essere impostate con il [comando `nuget config`](../tools/cli-ref-config.md).

`dependencyVersion` e `repositoryPath` si applicano solo ai progetti che usano `packages.config`. `globalPackagesFolder` si applica solo ai progetti che usano il formato PackageReference.

| Chiave | Value |
| --- | --- |
| dependencyVersion (solo `packages.config`) | Valore `DependencyVersion` predefinito per l'installazione, il ripristino e l'aggiornamento del pacchetto, quando non viene specificata direttamente l'opzione `-DependencyVersion`. Questo valore viene usato anche dall'interfaccia utente di Gestione pacchetti NuGet. I valori sono `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (progetti usando solo PackageReference) | Percorso della cartella dei pacchetti globale predefinita. L'impostazione predefinita è `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac/Linux). È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto. Questa impostazione viene sostituita dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza. |
| repositoryPath (solo `packages.config`) | Percorso in cui installare i pacchetti NuGet invece della cartella `$(Solutiondir)/packages` predefinita. È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto. Questa impostazione viene sostituita dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza. |
| defaultPushSource | Identifica l'URL o il percorso dell'origine del pacchetto che deve essere usato come impostazione predefinita se non vengono trovate altre origini di pacchetti per un'operazione. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Impostazioni del proxy da usare per la connessione a origini di pacchetti. `http_proxy` deve essere nel formato `http://<username>:<password>@<domain>`. Le password vengono crittografate e non possono essere aggiunte manualmente. Per `no_proxy`, il valore è un elenco delimitato da virgole di domini per il bypass del server proxy. In alternativa, è possibile usare le variabili di ambiente http_proxy e no_proxy per questi valori. Per altri dettagli, vedere [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (Impostazioni del proxy NuGet) (skolima.blogspot.com). |
| signatureValidationMode | Specifica la modalità di convalida utilizzata per verificare le firme dei pacchetti di installazione del pacchetto e il ripristino. I valori sono `accept`, `require`. Il valore predefinito è `accept`.

**Esempio**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>Sezione bindingRedirects

Specifica se NuGet esegue o meno i reindirizzamenti di binding automatici quando viene installato un pacchetto.

| Chiave | Value |
| --- | --- |
| skip | Valore booleano che indica se ignorare i reindirizzamenti di binding automatici. Il valore predefinito è false. |

**Esempio**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Sezione packageRestore

Controlla il ripristino dei pacchetti durante le compilazioni.

| Chiave | Value |
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

Controlla se la cartella `packages` di una soluzione è inclusa nel controllo del codice sorgente. Questa sezione funziona solo nei file `nuget.config` in una cartella della soluzione.

| Chiave | Value |
| --- | --- |
| disableSourceControlIntegration | Valore booleano che indica se ignorare la cartella dei pacchetti quando si utilizza il controllo del codice sorgente. Il valore predefinito è false. |

**Esempio**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Sezioni per le origini dei pacchetti

Il `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` e `trustedSigners` tutto il lavoro in modo da configurare come NuGet funziona con i repository dei pacchetti durante l'installazione, ripristino e le operazioni di aggiornamento.

Il [ `nuget sources` comandi](../tools/cli-ref-sources.md) viene generalmente usato per gestire queste impostazioni, ad eccezione dei `apikeys` che viene gestita con il [ `nuget setapikey` comando](../tools/cli-ref-setapikey.md), e `trustedSigners` che è gestito usando il [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).

Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Elenca tutte le origini di pacchetti note. L'ordine viene ignorato durante le operazioni di ripristino e con qualsiasi progetto usando il formato PackageReference. NuGet rispetta l'ordine delle origini per l'installazione e operazioni di aggiornamento con i progetti che usano `packages.config`.

| Chiave | Value |
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

| Chiave | Value |
| --- | --- |
| nomeutente | Nome utente per l'origine in testo normale. |
| password | Password crittografata per l'origine. |
| cleartextpassword | Password non crittografata per l'origine. |

**Esempio:**

Nel file di configurazione, l'elemento `<packageSourceCredentials>` contiene i nodi figlio per ogni nome di origine applicabile (gli spazi nel nome vengono sostituiti con `_x0020_`). Per le origini denominate "Contoso" e "Test Source", il file di configurazione contiene quanto segue quando si usano password crittografate:

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

| Chiave | Value |
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

| Chiave | Value |
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

| Chiave | Value |
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
## <a name="trustedsigners-section"></a>sezione trustedSigners

Gli archivi attendibili i firmatari utilizzati per consentire di pacchetto durante l'installazione o il ripristino. Questo elenco non può essere vuoto quando l'utente imposta `signatureValidationMode` a `require`. 

In questa sezione può essere aggiornata con le [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).

**Schema**:

Un'entità attendibile è una raccolta di `certificate` gli elementi che integra tutti i certificati che identificano un firmatario specificato. Un'entità attendibile può essere un' `Author` o un `Repository`.

Attendibile *repository* specifica inoltre il `serviceIndex` per il repository (che deve essere un valore valido `https` uri) e può facoltativamente specificare un elenco delimitato da punti e virgola di `owners` per limitare ulteriormente chi è attendibile da quel repository specifico.

Gli algoritmi hash supportati utilizzati per un'impronta digitale certificato vengono `SHA256`, `SHA384` e `SHA512`.

Se un `certificate` specifica `allowUntrustedRoot` come `true` il certificato specificato è consentito concatenarsi a una radice non attendibile durante la compilazione della catena di certificati come parte della verifica della firma.

**Esempio**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a>Uso delle variabili di ambiente

È possibile usare variabili di ambiente nei valori `nuget.config` (NuGet 3.4 +) per applicare le impostazioni in fase di esecuzione.

Ad esempio, se la variabile di ambiente `HOME` in Windows è impostata su `c:\users\username`, il valore di `%HOME%\NuGetRepository` nel file di configurazione viene risolto in `c:\users\username\NuGetRepository`.

In modo analogo, se la variabile `HOME` in Mac/Linux è impostata su `/home/myStuff`, `%HOME%/NuGetRepository` nel file di configurazione viene risolto in `/home/myStuff/NuGetRepository`.

Se non viene trovata una variabile di ambiente, NuGet usa il valore letterale dal file di configurazione.

## <a name="example-config-file"></a>File di configurazione di esempio

Di seguito è riportato un file `nuget.config` di esempio che illustra una serie di impostazioni:

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

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
