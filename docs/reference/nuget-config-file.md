---
title: Riferimento al file di nuget.config
description: Informazioni di riferimento sul file NuGet.Config, incluse le sezioni config, bindingRedirects, packageRestore, solution e packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 60626a5a2a261241e0dce34421f73a86d815e454
ms.sourcegitcommit: aeb9072f2fcaca73dc9de05b7fd643f1aa7c5821
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/18/2021
ms.locfileid: "101101345"
---
# <a name="nugetconfig-reference"></a>Riferimento nuget.config

Il comportamento di NuGet è controllato dalle impostazioni in diversi `NuGet.Config` `nuget.config` file o, come descritto in [configurazioni comuni di NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` è un file XML contenente un nodo `<configuration>` di livello superiore, che contiene a sua volta gli elementi per le sezioni descritte in questo argomento. Ogni sezione contiene zero o più elementi. Vedere il [file di configurazione di esempio](#example-config-file). Per i nomi delle impostazioni non viene fatta distinzione tra maiuscole e minuscole e per i valori si possono usare [variabili di ambiente](#using-environment-variables).

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Sezione config

Contiene impostazioni di configurazione varie, che possono essere impostate tramite il [ `nuget config` comando](../reference/cli-reference/cli-ref-config.md).

`dependencyVersion` e `repositoryPath` si applicano solo ai progetti che usano `packages.config` . `globalPackagesFolder` si applica solo ai progetti che usano il formato PackageReference.

| Chiave | Valore |
| --- | --- |
| dependencyVersion (solo `packages.config`) | Valore `DependencyVersion` predefinito per l'installazione, il ripristino e l'aggiornamento del pacchetto, quando non viene specificata direttamente l'opzione `-DependencyVersion`. Questo valore viene usato anche dall'interfaccia utente di Gestione pacchetti NuGet. I valori sono `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (progetti che usano solo PackageReference) | Percorso della cartella dei pacchetti globale predefinita. L'impostazione predefinita è `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac/Linux). È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto. Questa impostazione viene sottoposta a override dalla `NUGET_PACKAGES` variabile di ambiente, che ha la precedenza. |
| repositoryPath (solo `packages.config`) | Percorso in cui installare i pacchetti NuGet invece della cartella `$(Solutiondir)/packages` predefinita. È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto. Questa impostazione viene sottoposta a override dalla `NUGET_PACKAGES` variabile di ambiente, che ha la precedenza. |
| defaultPushSource | Identifica l'URL o il percorso dell'origine del pacchetto che deve essere usato come impostazione predefinita se non vengono trovate altre origini di pacchetti per un'operazione. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Impostazioni del proxy da usare per la connessione a origini di pacchetti. `http_proxy` deve essere nel formato `http://<username>:<password>@<domain>`. Le password vengono crittografate e non possono essere aggiunte manualmente. Per `no_proxy`, il valore è un elenco delimitato da virgole di domini per il bypass del server proxy. In alternativa, è possibile usare le variabili di ambiente http_proxy e no_proxy per questi valori. Per altri dettagli, vedere [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (Impostazioni del proxy NuGet) (skolima.blogspot.com). |
| signatureValidationMode | Specifica la modalità di convalida utilizzata per verificare le firme dei pacchetti per l'installazione e il ripristino del pacchetto. I valori sono `accept` , `require` . Il valore predefinito è `accept`.

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

Controlla il ripristino dei pacchetti durante le compilazioni.

| Chiave | Valore |
| --- | --- |
| Enabled | Valore booleano che indica se NuGet può eseguire il ripristino automatico. È anche possibile impostare la variabile di ambiente `EnableNuGetPackageRestore` con il valore `True` invece di impostare questa chiave nel file di configurazione. |
| automatic | Valore booleano che indica se NuGet deve controllare se mancano pacchetti durante la compilazione. |

**Esempio**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Sezione solution

Controlla se la cartella `packages` di una soluzione è inclusa nel controllo del codice sorgente. Questa sezione funziona solo nei file `nuget.config` in una cartella della soluzione.

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

`packageSources`,, `packageSourceCredentials` `apikeys` , `activePackageSource` `disabledPackageSources` E `trustedSigners` interagiscono tra loro per configurare il funzionamento di NuGet con i repository dei pacchetti durante le operazioni di installazione, ripristino e aggiornamento.

Il [ `nuget sources` comando](../reference/cli-reference/cli-ref-sources.md) viene in genere usato per gestire queste impostazioni, ad eccezione di `apikeys` che viene gestito usando il [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md)e `trustedSigners` che viene gestito tramite il [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).

Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Elenca tutte le origini di pacchetti note. L'ordine viene ignorato durante le operazioni di ripristino e con qualsiasi progetto che usa il formato PackageReference. NuGet rispetta l'ordine delle origini per le operazioni di installazione e aggiornamento con i progetti che usano `packages.config` .

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

> [!Tip]
> Quando `<clear />` è presente per un determinato nodo, NuGet ignora i valori di configurazione definiti in precedenza per tale nodo. [Altre informazioni sulla modalità di applicazione delle impostazioni](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Archivia i nomi utente e le password per le origini, in genere specificati con le opzioni `-username` e `-password` con `nuget sources`. Le password vengono crittografate per impostazione predefinita, a meno che non venga usata anche l'opzione `-storepasswordincleartext`.
Facoltativamente, è possibile specificare tipi di autenticazione validi con l' `-validauthenticationtypes` opzione.

| Chiave | valore |
| --- | --- |
| username | Nome utente per l'origine in testo normale. |
| password | Password crittografata per l'origine. Le password crittografate sono supportate solo in Windows e possono essere decrittografate solo quando vengono usate nello stesso computer e tramite lo stesso utente della crittografia originale. |
| cleartextpassword | Password non crittografata per l'origine. Nota: le variabili di ambiente possono essere usate per una maggiore sicurezza. |
| validauthenticationtypes | Elenco delimitato da virgole di tipi di autenticazione validi per questa origine. Impostare questa impostazione su `basic` se il server annuncia NTLM o Negotiate e le credenziali devono essere inviate usando il meccanismo di base, ad esempio quando si usa un Pat con Azure DevOps server locale. Altri valori validi includono `negotiate` , `kerberos` , `ntlm` e `digest` , ma è improbabile che questi valori risultino utili. |

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

Quando si usano password non crittografate archiviate in una variabile di ambiente:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
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

È inoltre possibile specificare metodi di autenticazione validi:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

Archivia le chiavi per le origini che usano l'autenticazione con chiave API, come impostato con il [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md).

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

## <a name="trustedsigners-section"></a>sezione trustedSigners

Archivia i firmatari attendibili utilizzati per consentire il pacchetto durante l'installazione o il ripristino. Questo elenco non può essere vuoto quando l'utente imposta `signatureValidationMode` su `require` . 

Questa sezione può essere aggiornata con il [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).

**Schema**:

Un firmatario attendibile dispone di una raccolta di `certificate` elementi che integrano tutti i certificati che identificano un determinato firmatario. Un firmatario attendibile può essere un `Author` o un `Repository` .

Un *repository* attendibile specifica anche `serviceIndex` per il repository (che deve essere un URI valido `https` ) ed è possibile specificare facoltativamente un elenco delimitato da punti e virgola di `owners` per limitare ulteriormente l'attendibilità di tale repository specifico.

Gli algoritmi hash supportati usati per un'impronta digitale del certificato sono `SHA256` , `SHA384` e `SHA512` .

Se un oggetto `certificate` specifica `allowUntrustedRoot` come `true` il certificato specificato può essere concatenato a una radice non attendibile durante la compilazione della catena di certificati come parte della verifica della firma.

**Esempio**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a>sezione fallbackPackageFolders

*(3.5 +)* Consente di preinstallare i pacchetti in modo che non sia necessario eseguire alcuna operazione se il pacchetto viene trovato nelle cartelle di fallback. Le cartelle dei pacchetti di fallback hanno esattamente la stessa struttura di cartelle e file della cartella del pacchetto globale: *. nupkg* è presente e tutti i file vengono estratti.

La logica di ricerca per questa configurazione è la seguente:

- Cercare nella cartella del pacchetto globale per verificare se il pacchetto o la versione è già stata scaricata.

- Esaminare le cartelle di fallback per una corrispondenza del pacchetto o della versione.

Se una delle due ricerche ha esito positivo, non è necessario eseguire il download.

Se non viene trovata alcuna corrispondenza, NuGet controlla le origini file e quindi le origini http, quindi Scarica i pacchetti.

| Chiave | Valore |
| --- | --- |
| (nome della cartella di fallback) | Percorso della cartella di fallback. |

**Esempio**:

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>sezione packageManagement

Imposta il formato di gestione dei pacchetti predefinito, ovvero *packages.config* o PackageReference. I progetti in stile SDK utilizzano sempre PackageReference.

| Chiave | Valore |
| --- | --- |
| format | Valore booleano che indica il formato di gestione dei pacchetti predefinito. Se `1` , il formato è PackageReference. Se `0` , format è *packages.config*. |
| disabled | Valore booleano che indica se visualizzare la richiesta di selezione di un formato di pacchetto predefinito durante la prima installazione del pacchetto. `False` nasconde la richiesta. |

**Esempio**:

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>Uso delle variabili di ambiente

È possibile usare variabili di ambiente nei valori `nuget.config` (NuGet 3.4 +) per applicare le impostazioni in fase di esecuzione.

Ad esempio, se la variabile di ambiente `HOME` in Windows è impostata su `c:\users\username`, il valore di `%HOME%\NuGetRepository` nel file di configurazione viene risolto in `c:\users\username\NuGetRepository`.

Si noti che è necessario usare le variabili di ambiente di tipo Windows (inizia e termina con%) anche in Mac/Linux. `$HOME/NuGetRepository`La presenza di in un file di configurazione non viene risolta. In Mac/Linux il valore di `%HOME%/NuGetRepository` viene risolto in `/home/myStuff/NuGetRepository` .

Se non viene trovata una variabile di ambiente, NuGet usa il valore letterale dal file di configurazione. Ad esempio `%MY_UNDEFINED_VAR%/NuGetRepository` , verrà risolto come `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

La tabella seguente mostra la sintassi delle variabili ambiente e il supporto del separatore di percorso per i file di NuGet.Config.

### <a name="nugetconfig-environment-variable-support"></a>Supporto della variabile di ambiente NuGet.Config

| Sintassi | Separatore dir | nuget.exe di Windows | dotnet.exe di Windows | Mac nuget.exe (in mono) | dotnet.exe Mac |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | Sì | Sì | Sì | Sì |
| `%MY_VAR%` | `\`  | Sì | Sì | No | No |
| `$MY_VAR` | `/`  | No | No | No | No |
| `$MY_VAR` | `\`  | No | No | No | No |


## <a name="example-config-file"></a>File di configurazione di esempio

Di seguito è riportato un esempio `nuget.config` di file che illustra una serie di impostazioni, tra cui quelle facoltative:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
