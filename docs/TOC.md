# [Che cos'è NuGet?](what-is-nuget.md)
# Introduzione
## [Installare gli strumenti client di NuGet](install-nuget-client-tools.md)
## [Installare e usare un pacchetto (interfaccia della riga di comando di dotnet)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md)
## [Installare e usare un pacchetto (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md)
## [Installare e usare un pacchetto (Visual Studio per Mac)](quickstart/install-and-use-a-package-in-visual-studio-mac.md)
## [Creare e pubblicare un pacchetto .NET Standard (interfaccia della riga di comando dotnet)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
## [Creare e pubblicare un pacchetto .NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md)
## [Creare e pubblicare un pacchetto .NET Framework (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
# Utilizzare i pacchetti
## [Panoramica e flusso di lavoro](consume-packages/overview-and-workflow.md)
## [Trovare e scegliere pacchetti](consume-packages/finding-and-choosing-packages.md)
## Installare e gestire pacchetti
### [Visual Studio](consume-packages/install-use-packages-visual-studio.md)
### [Visual Studio per Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)
### [Interfaccia della riga di comando di dotnet](consume-packages/install-use-packages-dotnet-cli.md)
### [Interfaccia della riga di comando di nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
### [Console di Gestione pacchetti (PowerShell)](consume-packages/install-use-packages-powershell.md)
## Configurare NuGet
### Opzioni di ripristino pacchetti
#### [Ripristinare pacchetti](consume-packages/package-restore.md)
#### [Risoluzione dei problemi](consume-packages/package-restore-troubleshooting.md)
### [Reinstallare e aggiornare pacchetti](consume-packages/reinstalling-and-updating-packages.md)
### [Gestire pacchetti globali e cartelle cache](consume-packages/managing-the-global-packages-and-cache-folders.md)
### [Gestire i limiti di attendibilità dei pacchetti](consume-packages/installing-signed-packages.md)
### [Usare i feed autenticati](consume-packages/consuming-packages-authenticated-feeds.md)
### [Usare i sistemi di controllo del codice sorgente](consume-packages/packages-and-source-control.md)
### [Configurazioni comuni di NuGet](consume-packages/configuring-nuget-behavior.md)
## Fare riferimento ai pacchetti nel progetto
### [Riferimenti ai pacchetti nei file di progetto](consume-packages/package-references-in-project-files.md)
### [Eseguire la migrazione di packages.config a PackageReference](consume-packages/migrate-packages-config-to-package-reference.md)
### [packages.config](reference/packages-config.md)
# Creazione di pacchetti
## [Panoramica e flusso di lavoro](create-packages/overview-and-workflow.md)
## [Creare un pacchetto (interfaccia della riga di comando dotnet)](create-packages/creating-a-package-dotnet-cli.md)
## [Creare un pacchetto (interfaccia della riga di comando nuget.exe)](create-packages/creating-a-package.md)
## [Creare un pacchetto (MSBuild)](create-packages/creating-a-package-msbuild.md)
## [Procedure consigliate per la creazione di pacchetti](create-packages/Package-authoring-best-practices.md)
## [Compilare un pacchetto per versione non definitiva](create-packages/prerelease-packages.md)
## [Creare un pacchetto di simboli](create-packages/symbol-packages-snupkg.md)
## [Supportare framework a più destinazioni nel file di progetto](create-packages/multiple-target-frameworks-project-file.md)
## Attività avanzate
### [Supportare più framework di destinazione](create-packages/supporting-multiple-target-frameworks.md)
### [Modificare il codice sorgente e i file di configurazione](create-packages/source-and-config-file-transformations.md)
### [Selezionare gli assembly cui i progetti fanno riferimento](create-packages/select-assemblies-referenced-by-projects.md)
### [Impostare il tipo di pacchetto](create-packages/set-package-type.md)
### [Creare un pacchetto localizzato](create-packages/creating-localized-packages.md)
## Guide per contenuto specifico
### [Creare un pacchetto UWP (C++)](guides/create-uwp-packages.md)
### [Creare un pacchetto UWP (C#)](guides/create-uwp-packages-CS.md)
### [Creare un pacchetto nativo](guides/native-packages.md)
### [Creare controlli dell'interfaccia utente come pacchetti NuGet](guides/create-UI-controls.md)
### [Creare un analizzatore diagnostico come pacchetto NuGet](guides/analyzers-conventions.md)
### [Creare un pacchetto per Xamarin con Visual Studio 2017 o 2019](guides/create-packages-for-xamarin.md)
### [Creare un pacchetto con assembly di interoperabilità COM](create-packages/author-packages-with-COM-interop-assemblies.md)
## Firmare pacchetti
### [Firmare un pacchetto](create-packages/sign-a-package.md)
### [Requisiti e firme di pacchetti firmati](reference/signed-packages-reference.md)
# Pubblicazione di pacchetti
## Pubblicare in NuGet.org
### [Pubblicare un pacchetto](nuget-org/publish-a-package.md)
### [Chiavi API](nuget-org/scoped-api-keys.md)
## Pubblicare in un feed privato
### [Panoramica](hosting-packages/overview.md)
### [Artefatti di Azure](/azure/devops/artifacts/nuget/publish?view=azure-devops)
### [NuGet.Server](hosting-packages/nuget-server.md)
### [Feed locali](hosting-packages/local-feeds.md)
# Concetti
## [Processo di installazione pacchetti](concepts/package-installation-process.md)
## [Controllo delle versioni dei pacchetti](concepts/package-versioning.md)
## [Risoluzione delle dipendenze](concepts/dependency-resolution.md)
## [Procedure consigliate per una supply chain di software sicuro](concepts/Security-Best-Practices.md)
## [Risoluzione dei problemi relativi ai pacchetti installati](concepts/troubleshooting-installed-packages.md)
# Riferimento
## [.nuspec](reference/nuspec.md)
## [File nuget.config](reference/nuget-config-file.md)
## [Framework di destinazione](reference/target-frameworks.md)
## [Pack e restore come destinazioni MSBuild](reference/msbuild-targets.md)
## [Interfaccia della riga di comando di dotnet](reference/dotnet-Commands.md)
## [Informazioni di riferimento sull'interfaccia della riga di comando di nuget.exe](reference/nuget-exe-cli-reference.md)
### [add](reference/cli-reference/cli-ref-add.md)
### [config](reference/cli-reference/cli-ref-config.md)
### [delete](reference/cli-reference/cli-ref-delete.md)
### [help or ?](reference/cli-reference/cli-ref-help.md)
### [init](reference/cli-reference/cli-ref-init.md)
### [install](reference/cli-reference/cli-ref-install.md)
### [list](reference/cli-reference/cli-ref-list.md)
### [locals](reference/cli-reference/cli-ref-locals.md)
### [mirror](reference/cli-reference/cli-ref-mirror.md)
### [pack](reference/cli-reference/cli-ref-pack.md)
### [push](reference/cli-reference/cli-ref-push.md)
### [restore](reference/cli-reference/cli-ref-restore.md)
### [search](reference/cli-reference/cli-ref-search.md)
### [setapikey](reference/cli-reference/cli-ref-setapikey.md)
### [sign](reference/cli-reference/cli-ref-sign.md)
### [sources](reference/cli-reference/cli-ref-sources.md)
### [spec](reference/cli-reference/cli-ref-spec.md)
### [update](reference/cli-reference/cli-ref-update.md)
### [verify](reference/cli-reference/cli-ref-verify.md)
### [trusted-signers](reference/cli-reference/cli-ref-trusted-signers.md)
### [Variabili di ambiente](reference/cli-reference/cli-ref-environment-variables.md)
### [Supporto del percorso lungo](reference/cli-reference/cli-ref-long-path.md)
## [Informazioni di riferimento su PowerShell](reference/powershell-reference.md)
### [Add-BindingRedirect](reference/ps-reference/ps-ref-add-bindingredirect.md)
### [Find-Package](reference/ps-reference/ps-ref-find-package.md)
### [Get-Package](reference/ps-reference/ps-ref-get-package.md)
### [Get-Project](reference/ps-reference/ps-ref-get-project.md)
### [Install-Package](reference/ps-reference/ps-ref-install-package.md)
### [Open-PackagePage](reference/ps-reference/ps-ref-open-packagepage.md)
### [Sync-Package](reference/ps-reference/ps-ref-sync-package.md)
### [Uninstall-Package](reference/ps-reference/ps-ref-uninstall-package.md)
### [Update-Package](reference/ps-reference/ps-ref-update-package.md)
## API Server NuGet
### [Panoramica](api/overview.md)
### Risorse
#### [Completamento automatico](api/search-autocomplete-service-resource.md)
#### [Catalogo](api/catalog-resource.md)
#### [Contenuto dei pacchetti](api/package-base-address-resource.md)
#### [URL dei dettagli dei pacchetti](api/package-details-template-resource.md)
#### [Metadati dei pacchetti](api/registration-base-url-resource.md)
#### [Push ed eliminazione](api/package-publish-resource.md)
#### [Eseguire il push dei pacchetti di simboli](api/symbol-package-publish-resource.md)
#### [URL per segnalare abusi](api/report-abuse-resource.md)
#### [Firme di repository](api/repository-signatures-resource.md)
#### [Ricerca](api/search-query-service-resource.md)
#### [Indice dei servizi](api/service-index.md)
### [Procedura: Query per recuperare tutti i pacchetti tramite l'API](guides/api/query-for-all-published-packages.md)
### [Limiti di velocità](api/rate-limits.md)
### [Protocolli di nuget.org](api/nuget-protocols.md)
### [tools.json](api/tools-json.md)
## [NuGet Client SDK](reference/nuget-client-sdk.md)
## [Errori e avvisi](reference/Errors-and-Warnings.md)
### [NU1000](reference/errors-and-warnings/NU1000.md)
### [NU1001](reference/errors-and-warnings/NU1001.md)
### [NU1002](reference/errors-and-warnings/NU1002.md)
### [NU1003](reference/errors-and-warnings/NU1003.md)
### [NU1100](reference/errors-and-warnings/NU1100.md)
### [NU1101](reference/errors-and-warnings/NU1101.md)
### [NU1102](reference/errors-and-warnings/NU1102.md)
### [NU1103](reference/errors-and-warnings/NU1103.md)
### [NU1104](reference/errors-and-warnings/NU1104.md)
### [NU1105](reference/errors-and-warnings/NU1105.md)
### [NU1106](reference/errors-and-warnings/NU1106.md)
### [NU1107](reference/errors-and-warnings/NU1107.md)
### [NU1108](reference/errors-and-warnings/NU1108.md)
### [NU1201](reference/errors-and-warnings/NU1201.md)
### [NU1202](reference/errors-and-warnings/NU1202.md)
### [NU1203](reference/errors-and-warnings/NU1203.md)
### [NU1401](reference/errors-and-warnings/NU1401.md)
### [NU1500](reference/errors-and-warnings/NU1500.md)
### [NU1501](reference/errors-and-warnings/NU1501.md)
### [NU1502](reference/errors-and-warnings/NU1502.md)
### [NU1503](reference/errors-and-warnings/NU1503.md)
### [NU1601](reference/errors-and-warnings/NU1601.md)
### [NU1602](reference/errors-and-warnings/NU1602.md)
### [NU1603](reference/errors-and-warnings/NU1603.md)
### [NU1604](reference/errors-and-warnings/NU1604.md)
### [NU1605](reference/errors-and-warnings/NU1605.md)
### [NU1608](reference/errors-and-warnings/NU1608.md)
### [NU1701](reference/errors-and-warnings/NU1701.md)
### [NU1703](reference/errors-and-warnings/NU1703.md)
### [NU1801](reference/errors-and-warnings/NU1801.md)
### [NU3000](reference/errors-and-warnings/NU3000.md)
### [NU3001](reference/errors-and-warnings/NU3001.md)
### [NU3002](reference/errors-and-warnings/NU3002.md)
### [NU3003](reference/errors-and-warnings/NU3003.md)
### [NU3004](reference/errors-and-warnings/NU3004.md)
### [NU3005](reference/errors-and-warnings/NU3005.md)
### [NU3006](reference/errors-and-warnings/NU3006.md)
### [NU3007](reference/errors-and-warnings/NU3007.md)
### [NU3008](reference/errors-and-warnings/NU3008.md)
### [NU3009](reference/errors-and-warnings/NU3009.md)
### [NU3010](reference/errors-and-warnings/NU3010.md)
### [NU3011](reference/errors-and-warnings/NU3011.md)
### [NU3012](reference/errors-and-warnings/NU3012.md)
### [NU3013](reference/errors-and-warnings/NU3013.md)
### [NU3014](reference/errors-and-warnings/NU3014.md)
### [NU3015](reference/errors-and-warnings/NU3015.md)
### [NU3016](reference/errors-and-warnings/NU3016.md)
### [NU3017](reference/errors-and-warnings/NU3017.md)
### [NU3018](reference/errors-and-warnings/NU3018.md)
### [NU3019](reference/errors-and-warnings/NU3019.md)
### [NU3020](reference/errors-and-warnings/NU3020.md)
### [NU3021](reference/errors-and-warnings/NU3021.md)
### [NU3022](reference/errors-and-warnings/NU3022.md)
### [NU3023](reference/errors-and-warnings/NU3023.md)
### [NU3024](reference/errors-and-warnings/NU3024.md)
### [NU3025](reference/errors-and-warnings/NU3025.md)
### [NU3026](reference/errors-and-warnings/NU3026.md)
### [NU3027](reference/errors-and-warnings/NU3027.md)
### [NU3028](reference/errors-and-warnings/NU3028.md)
### [NU3029](reference/errors-and-warnings/NU3029.md)
### [NU3030](reference/errors-and-warnings/NU3030.md)
### [NU3031](reference/errors-and-warnings/NU3031.md)
### [NU3032](reference/errors-and-warnings/NU3032.md)
### [NU3033](reference/errors-and-warnings/NU3033.md)
### [NU3034](reference/errors-and-warnings/NU3034.md)
### [NU3035](reference/errors-and-warnings/NU3035.md)
### [NU3036](reference/errors-and-warnings/NU3036.md)
### [NU3037](reference/errors-and-warnings/NU3037.md)
### [NU3038](reference/errors-and-warnings/NU3038.md)
### [NU3040](reference/errors-and-warnings/NU3040.md)
### [NU5000](reference/errors-and-warnings/NU5000.md)
### [NU5001](reference/errors-and-warnings/NU5001.md)
### [NU5002](reference/errors-and-warnings/NU5002.md)
### [NU5003](reference/errors-and-warnings/NU5003.md)
### [NU5004](reference/errors-and-warnings/NU5004.md)
### [NU5005](reference/errors-and-warnings/NU5005.md)
### [NU5007](reference/errors-and-warnings/NU5007.md)
### [NU5008](reference/errors-and-warnings/NU5008.md)
### [NU5009](reference/errors-and-warnings/NU5009.md)
### [NU5010](reference/errors-and-warnings/NU5010.md)
### [NU5011](reference/errors-and-warnings/NU5011.md)
### [NU5012](reference/errors-and-warnings/NU5012.md)
### [NU5013](reference/errors-and-warnings/NU5013.md)
### [NU5014](reference/errors-and-warnings/NU5014.md)
### [NU5015](reference/errors-and-warnings/NU5015.md)
### [NU5016](reference/errors-and-warnings/NU5016.md)
### [NU5017](reference/errors-and-warnings/NU5017.md)
### [NU5018](reference/errors-and-warnings/NU5018.md)
### [NU5019](reference/errors-and-warnings/NU5019.md)
### [NU5020](reference/errors-and-warnings/NU5020.md)
### [NU5021](reference/errors-and-warnings/NU5021.md)
### [NU5022](reference/errors-and-warnings/NU5022.md)
### [NU5023](reference/errors-and-warnings/NU5023.md)
### [NU5024](reference/errors-and-warnings/NU5024.md)
### [NU5025](reference/errors-and-warnings/NU5025.md)
### [NU5026](reference/errors-and-warnings/NU5026.md)
### [NU5027](reference/errors-and-warnings/NU5027.md)
### [NU5028](reference/errors-and-warnings/NU5028.md)
### [NU5029](reference/errors-and-warnings/NU5029.md)
### [NU5030](reference/errors-and-warnings/NU5030.md)
### [NU5031](reference/errors-and-warnings/NU5031.md)
### [NU5032](reference/errors-and-warnings/NU5032.md)
### [NU5033](reference/errors-and-warnings/NU5033.md)
### [NU5034](reference/errors-and-warnings/NU5034.md)
### [NU5035](reference/errors-and-warnings/NU5035.md)
### [NU5036](reference/errors-and-warnings/NU5036.md)
### [NU5037](reference/errors-and-warnings/NU5037.md)
### [NU5046](reference/errors-and-warnings/NU5046.md)
### [NU5047](reference/errors-and-warnings/NU5047.md)
### [NU5048](reference/errors-and-warnings/NU5048.md)
### [NU5100](reference/errors-and-warnings/NU5100.md)
### [NU5101](reference/errors-and-warnings/NU5101.md)
### [NU5102](reference/errors-and-warnings/NU5102.md)
### [NU5103](reference/errors-and-warnings/NU5103.md)
### [NU5104](reference/errors-and-warnings/NU5104.md)
### [NU5105](reference/errors-and-warnings/NU5105.md)
### [NU5106](reference/errors-and-warnings/NU5106.md)
### [NU5107](reference/errors-and-warnings/NU5107.md)
### [NU5108](reference/errors-and-warnings/NU5108.md)
### [NU5109](reference/errors-and-warnings/NU5109.md)
### [NU5110](reference/errors-and-warnings/NU5110.md)
### [NU5111](reference/errors-and-warnings/NU5111.md)
### [NU5112](reference/errors-and-warnings/NU5112.md)
### [NU5114](reference/errors-and-warnings/NU5114.md)
### [NU5115](reference/errors-and-warnings/NU5115.md)
### [NU5116](reference/errors-and-warnings/NU5116.md)
### [NU5117](reference/errors-and-warnings/NU5117.md)
### [NU5118](reference/errors-and-warnings/NU5118.md)
### [NU5119](reference/errors-and-warnings/NU5119.md)
### [NU5120](reference/errors-and-warnings/NU5120.md)
### [NU5121](reference/errors-and-warnings/NU5121.md)
### [NU5122](reference/errors-and-warnings/NU5122.md)
### [NU5123](reference/errors-and-warnings/NU5123.md)
### [NU5124](reference/errors-and-warnings/NU5124.md)
### [NU5125](reference/errors-and-warnings/NU5125.md)
### [NU5127](reference/errors-and-warnings/NU5127.md)
### [NU5128](reference/errors-and-warnings/NU5128.md)
### [NU5129](reference/errors-and-warnings/NU5129.md)
### [NU5130](reference/errors-and-warnings/NU5130.md)
### [NU5131](reference/errors-and-warnings/NU5131.md)
### [NU5500](reference/errors-and-warnings/NU5500.md)
## Contenuti in archivio
### [Formato di gestione project.json](archive/project-json.md)
### [project.json e UWP](archive/project-json-and-uwp.md)
### [project.json impact](archive/project-json-impact.md)
# Estendibilità
## Estendibilità: plug-in NuGet
### [Plug-in multipiattaforma NuGet](reference/extensibility/NuGet-Cross-Platform-Plugins.md)
### [Plug-in di autenticazione multipiattaforma NuGet](reference/extensibility/nuget-cross-platform-authentication-plugin.md)
### [Provider di credenziali NuGet per Visual Studio](reference/extensibility/nuget-credential-providers-for-visual-studio.md)
### [Provider di credenziali nuget.exe](reference/extensibility/nuget-exe-credential-providers.md)
## Estendibilità in Visual Studio
### [API NuGet in Visual Studio](visual-studio-extensibility/nuget-api-in-visual-studio.md)
### [Supporto del sistema di progetto](visual-studio-extensibility/project-system-support.md)
### [Modelli di Visual Studio](visual-studio-extensibility/visual-studio-templates.md)
# Risorse
## Criteri
### [Governance](policies/governance.md)
### [Ecosistema](policies/ecosystem.md)
### [Criteri di NuGet.org](nuget-org/policies/data-requests.md)
## Note sulla versione
### [Problemi noti](release-notes/known-issues.md)
### NuGet 5.x
#### [NuGet 5.11](release-notes/NuGet-5.11.md)
#### [NuGet 5.10](release-notes/NuGet-5.10.md)
#### [NuGet 5.9](release-notes/NuGet-5.9.md)
#### [NuGet 5.8](release-notes/NuGet-5.8.md)
#### [NuGet 5.7](release-notes/NuGet-5.7.md)
#### [NuGet 5.6](release-notes/NuGet-5.6.md)
#### [NuGet 5.5](release-notes/NuGet-5.5.md)
#### [NuGet 5.4](release-notes/NuGet-5.4.md)
#### [NuGet 5.3](release-notes/NuGet-5.3.md)
#### [NuGet 5.2](release-notes/NuGet-5.2-RTM.md)
#### [NuGet 5.1](release-notes/NuGet-5.1-RTM.md)
#### [NuGet 5.0](release-notes/NuGet-5.0-RTM.md)
### NuGet 4.x
#### [NuGet 4.9 RTM](release-notes/NuGet-4.9-RTM.md)
#### [NuGet 4.8 RTM](release-notes/NuGet-4.8-RTM.md)
#### [NuGet 4.7 RTM](release-notes/NuGet-4.7-RTM.md)
#### [NuGet 4.6 RTM](release-notes/NuGet-4.6-RTM.md)
#### [NuGet 4.5 RTM](release-notes/NuGet-4.5-RTM.md)
#### [NuGet 4.4 RTM](release-notes/NuGet-4.4-RTM.md)
#### [NuGet 4.3 RTM](release-notes/NuGet-4.3-RTM.md)
#### [NuGet 4.0 RTM](release-notes/NuGet-4.0-RTM.md)
#### [NuGet 4.0 RC](release-notes/NuGet-4.0-RC.md)
### NuGet 3.x
#### [NuGet 3.5 RTM](release-notes/NuGet-3.5-RTM.md)
#### [NuGet 3.5 RC](release-notes/NuGet-3.5-RC.md)
#### [NuGet 3.5 Beta2](release-notes/NuGet-3.5-Beta2.md)
#### [NuGet 3.5 Beta](release-notes/NuGet-3.5-Beta.md)
#### [NuGet 3.4.4](release-notes/NuGet-3.4.4.md)
#### [NuGet 3.4.3](release-notes/NuGet-3.4.3.md)
#### [NuGet 3.4.2](release-notes/NuGet-3.4.2.md)
#### [NuGet 3.4.1](release-notes/NuGet-3.4.1.md)
#### [NuGet 3.4](release-notes/NuGet-3.4.md)
#### [NuGet 3.4 RC](release-notes/NuGet-3.4-RC.md)
#### [NuGet 3.3](release-notes/NuGet-3.3.md)
#### [NuGet 3.2.1](release-notes/NuGet-3.2.1.md)
#### [NuGet 3.2](release-notes/NuGet-3.2.md)
#### [NuGet 3.2 RC](release-notes/NuGet-3.2-RC.md)
#### [NuGet 3.1.1](release-notes/NuGet-3.1.1.md)
#### [NuGet 3.1](release-notes/NuGet-3.1.md)
#### [NuGet 3.0.0](release-notes/NuGet-3.0.0.md)
#### [NuGet 3.0 RC2](release-notes/NuGet-3.0-RC2.md)
#### [NuGet 3.0 RC](release-notes/NuGet-3.0-RC.md)
#### [NuGet 3.0 Beta](release-notes/NuGet-3.0-Beta.md)
#### [NuGet 3.0 Preview](release-notes/NuGet-3.0-Preview.md)
### NuGet 2.x
#### [NuGet 2.12](release-notes/NuGet-2.12.md)
#### [NuGet 2.12 RC](release-notes/NuGet-2.12-RC.md)
#### [NuGet 2.9 RC](release-notes/NuGet-2.9-RC.md)
#### [NuGet 2.8.7](release-notes/NuGet-2.8.7.md)
#### [NuGet 2.8.6](release-notes/NuGet-2.8.6.md)
#### [NuGet 2.8.5](release-notes/NuGet-2.8.5.md)
#### [NuGet 2.8.3](release-notes/NuGet-2.8.3.md)
#### [NuGet 2.8.2](release-notes/NuGet-2.8.2.md)
#### [NuGet 2.8.1](release-notes/NuGet-2.8.1.md)
#### [NuGet 2.8](release-notes/NuGet-2.8.md)
#### [NuGet 2.7.2](release-notes/NuGet-2.7.2.md)
#### [NuGet 2.7.1](release-notes/NuGet-2.7.1.md)
#### [NuGet 2.7](release-notes/NuGet-2.7.md)
#### [NuGet 2.6.1 per WebMatrix](release-notes/NuGet-2.6.1-for-WebMatrix.md)
#### [NuGet 2.6](release-notes/NuGet-2.6.md)
#### [NuGet 2.5](release-notes/NuGet-2.5.md)
#### [NuGet 2.2.1](release-notes/NuGet-2.2.1.md)
#### [NuGet 2.2](release-notes/NuGet-2.2.md)
#### [NuGet 2.1](release-notes/NuGet-2.1.md)
#### [NuGet 2.0](release-notes/NuGet-2.0.md)
### NuGet 1.x
#### [NuGet 1.8](release-notes/NuGet-1.8.md)
#### [NuGet 1.7](release-notes/NuGet-1.7.md)
#### [NuGet 1.6](release-notes/NuGet-1.6.md)
#### [NuGet 1.5](release-notes/NuGet-1.5.md)
#### [NuGet 1.4](release-notes/NuGet-1.4.md)
#### [NuGet 1.3](release-notes/NuGet-1.3.md)
#### [NuGet 1.2](release-notes/NuGet-1.2.md)
#### [NuGet 1.1](release-notes/NuGet-1.1.md)
## [Domande frequenti](resources/nuget-faq.yml)
## [Formato di progetto](resources/check-project-format.md)
# [NuGet.org](nuget-org/overview-nuget-org.md)
