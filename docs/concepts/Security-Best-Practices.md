---
title: Procedure consigliate per una supply chain di software sicuro
description: Procedure consigliate per proteggere la supply chain del software tramite NuGet & GitHub.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726977"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Procedure consigliate per una supply chain di software sicuro

Open Source è ovunque. Si trova in molte codebase proprietarie e progetti della community. Per organizzazioni e singoli utenti, la domanda attuale non è se si sta usando codice open source, ma quale codice open source si sta usando e quanto.

Se non si è a conoscenza di ciò che è presente nella supply chain del software, una vulnerabilità upstream in una delle dipendenze può essere irreversibile, rendendo l'utente e i clienti vulnerabili a una potenziale compromissione. In questo documento si approfondirà il significato del termine "supply chain software", il motivo per cui è importante e come è possibile proteggere la supply chain del progetto con le procedure consigliate.

![Stato di Octoverse 2020 - Open Source](media/opensource-percent.png)

## <a name="dependencies"></a>Dependencies 

Il termine supply chain software viene usato per fare riferimento a tutto ciò che entra nel software e da dove proviene. Sono le dipendenze e le proprietà delle dipendenze da cui dipende la supply chain del software. Una dipendenza è ciò che il software deve eseguire. Può trattarsi di codice, file binari o altri componenti e da dove provengono, ad esempio un repository o un gestore di pacchetti.

Include chi ha scritto il codice, quando è stato contribuito, come è stato esaminato per problemi di sicurezza, vulnerabilità note, versioni supportate, informazioni sulle licenze e qualsiasi elemento che lo riguarda in qualsiasi momento del processo.

La supply chain comprende anche altre parti dello stack oltre a una singola applicazione, ad esempio gli script di compilazione e creazione dei pacchetti o il software che esegue l'infrastruttura su cui si basa l'applicazione.

## <a name="vulnerabilities"></a>Vulnerabilità

Attualmente, le dipendenze software sono pervasive. È piuttosto comune per i progetti usare centinaia di dipendenze open source per funzionalità che non è stato necessario scrivere manualmente. Ciò può significare che la maggior parte dell'applicazione è costituita da codice non creato dall'utente. 

![Stato di Octoverse 2020 - Dipendenze](media/dependencies.png)

Le possibili vulnerabilità nelle dipendenze di terze parti o open source sono presumibilmente dipendenze che non è possibile controllare con latemporaneamente al codice scritto, il che può creare potenziali rischi per la sicurezza nella supply chain.

Se una di queste dipendenze presenta una vulnerabilità, è probabile che si abbia anche una vulnerabilità. Questo può essere un problema, in quanto una delle dipendenze può cambiare senza che l'utente ne sia a conoscenza. Anche se una vulnerabilità esiste attualmente in una dipendenza, ma non è sfruttabile, può essere sfruttata in futuro. 

La possibilità di sfruttare il lavoro di migliaia di sviluppatori open source e autori di librerie significa che migliaia di sviluppatori possono contribuire in modo efficace direttamente al codice di produzione. Il prodotto, attraverso la supply chain del software, è interessato da vulnerabilità senza applicazione, errori inefficievoli o persino da attacchi dannosi contro le dipendenze.

## <a name="supply-chain-compromises"></a>Compromissione della supply chain

La definizione tradizionale di una supply chain deriva dalla produzione. è la catena di processi necessari per creare e fornire qualcosa. Include pianificazione, fornitura di materiali, produzione e vendita al dettaglio. Una supply chain software è simile, tranne che per i materiali, è codice. Invece di produrre, si tratta di sviluppo. Invece di disaggregare il ore da zero, il codice viene generato da fornitori, commerciali o open source e, in generale, il codice open source proviene da repository. L'aggiunta di codice da un repository significa che il prodotto assume una dipendenza da tale codice.

Un esempio di attacco alla supply chain del software si verifica quando il codice dannoso viene intenzionalmente aggiunto a una dipendenza, usando la catena di alimentazione di tale dipendenza per distribuire il codice alle sue dipendenze. Gli attacchi alla supply chain sono reali. Esistono molti metodi per attaccare una supply chain, dall'inserimento diretto di codice dannoso come nuovo collaboratore, all'assunzione dell'account di un collaboratore senza che altri ne siano abilitino la verifica o persino la compromissione di una chiave di firma per distribuire software che non fa ufficialmente parte della dipendenza.

Un attacco alla supply chain del software è di per sé raramente l'obiettivo finale, ma è l'inizio di un'opportunità per un utente malintenzionato di inserire malware o fornire una backdoor per l'accesso futuro.

![Stato del ciclo di vita della vulnerabilità octoverse 2020](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Software senzatch

L'uso open source è attualmente significativo e non è previsto un rallentamento in qualsiasi momento. Dato che non si interromperà l'uso di software open source, la minaccia per la sicurezza della supply chain è il software senza patch. Sapendo che, come è possibile affrontare il rischio che una dipendenza del progetto abbia una vulnerabilità?

- **Sapere cosa si trova nell'ambiente.** Ciò richiede l'individuazione delle dipendenze e delle dipendenze transitive per comprendere i rischi di tali dipendenze, ad esempio vulnerabilità o restrizioni di licenza.
- **Gestire le dipendenze.** Quando viene individuata una nuova vulnerabilità di sicurezza, è necessario determinare se si è influenzati e, in tal caso, eseguire l'aggiornamento alla versione più recente e alla patch di sicurezza disponibili. Ciò è particolarmente importante per esaminare le modifiche che introducono nuove dipendenze o controllano regolarmente le dipendenze meno recenti.
- **Monitorare la supply chain.** Ciò avviene controllando i controlli disponibili per gestire le dipendenze. Ciò consente di applicare condizioni più restrittive da rispettare per le dipendenze.

![Stato dell'octoverse 2020 - Avvisi](media/advisories.png)

Verranno illustrate varie tecniche e strumenti forniti NuGet e GitHub, che è possibile usare oggi per affrontare potenziali rischi all'interno del progetto. 

## <a name="knowing-what-is-in-your-environment"></a>Conoscere gli elementi presenti nell'ambiente

### <a name="nuget-dependency-graph"></a>NuGet grafico delle dipendenze

**📦 Consumer di pacchetti**

È possibile visualizzare le NuGet dipendenze nel progetto esaminando direttamente il file di progetto corrispondente.

In genere si trova in una delle due posizioni seguenti:

-   [`packages.config`](../reference/packages-config.md) : si trova nella radice del progetto.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) : si trova nel file di progetto. 

A seconda del metodo utilizzato per gestire le dipendenze NuGet, è anche possibile usare Visual Studio per visualizzare le dipendenze direttamente [in](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) Esplora soluzioni o [NuGet Gestione pacchetti](../consume-packages/install-use-packages-visual-studio.md).

Per gli ambienti dell'interfaccia della riga di comando, è possibile usare il comando per elencare le dipendenze del progetto [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) o della soluzione. 

Per altre informazioni sulla gestione NuGet dipendenze, [vedere la documentazione seguente.](../consume-packages/overview-and-workflow.md)

### <a name="github-dependency-graph"></a>Grafico delle dipendenze di GitHub 

**📦 Consumer di pacchetti | 📦🖊 Autore del pacchetto**

È possibile usare GitHub grafico delle dipendenze del progetto per visualizzare i pacchetti da cui dipende il progetto e i repository che dipendono da esso. Ciò consente di visualizzare eventuali vulnerabilità rilevate nelle relative dipendenze.

Per altre informazioni sulle dipendenze GitHub repository, [vedere la documentazione seguente.](https://github.co/dependency-graph)

### <a name="dependency-versions"></a>Versioni delle dipendenze

**📦 Consumer di pacchetti | 📦🖊 Autore del pacchetto**

Per garantire una supply chain sicura delle dipendenze, è necessario assicurarsi che tutte le dipendenze degli strumenti di & siano aggiornate regolarmente alla versione stabile più recente perché spesso includono le funzionalità e le patch di sicurezza più recenti per le vulnerabilità note. Le dipendenze possono includere il codice da cui si dipende, i file binari utilizzati, gli strumenti in uso e altri componenti. Ciò può includere:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [Runtime & .NET SDK](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [Pacchetti NuGet](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Gestire le dipendenze

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>NuGet dipendenze deprecate e vulnerabili

**📦 Consumer di pacchetti | 📦🖊 Autore del pacchetto**

È possibile usare l'interfaccia della riga di comando [dotnet](/dotnet/core/tools/dotnet-list-package) per elencare eventuali dipendenze deprecate o vulnerabili note presenti all'interno del progetto o della soluzione. È possibile usare il comando o per fornire un elenco di eventuali `dotnet list package --deprecated` `dotnet list package --vulnerable` deprecazioni o vulnerabilità note.

### <a name="github-vulnerable-dependencies"></a>GitHub dipendenze vulnerabili

**📦 Consumer di pacchetti | 📦🖊 Autore del pacchetto**

Se il progetto è ospitato in GitHub, è possibile sfruttare la sicurezza di [GitHub](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) per individuare vulnerabilità ed errori di sicurezza nel progetto e Dependabot li correggerà aprendo una richiesta pull sulla codebase. 

Il rilevamento delle dipendenze vulnerabili prima dell'introduzione è uno degli obiettivi del [movimento "Maiusc a](https://en.wikipedia.org/wiki/Shift-left_testing) sinistra". La possibilità di avere informazioni sulle dipendenze, ad esempio la licenza, le dipendenze transitive e l'età delle dipendenze, consente di eseguire questa operazione.

Per altre informazioni sugli avvisi di Dependabot & aggiornamenti della sicurezza, [vedere la documentazione seguente.](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)

### <a name="nuget-feeds"></a>NuGet feed

**📦 Consumer di pacchetti**

Quando si usano più feed & di origine NuGet privati, è possibile scaricare un pacchetto da qualsiasi feed. Per garantire che la compilazione sia prevedibile [](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)e sicura da attacchi noti, ad esempio la confusione delle dipendenze, conoscere i feed specifici da cui proviene il pacchetto è una procedura consigliata. È possibile usare un singolo feed o un feed privato con funzionalità upstream per la protezione.

Per altre informazioni su come proteggere i feed dei pacchetti, vedere [3 Ways to Mitigate Risk When Using Private Package Feeds](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).

### <a name="client-trust-policies"></a>Criteri di attendibilità client

**📦 Consumer di pacchetti**

Esistono criteri a cui è possibile acconsentire esplicitamente in cui è necessario che i pacchetti in uso siano firmati. In questo modo è possibile considerare attendibile l'autore di un pacchetto, purché sia firmato dall'autore, o considerare attendibile un pacchetto se è di proprietà di un utente o un account specifico firmato da NuGet.org.

Per configurare i criteri di attendibilità client, [vedere la documentazione seguente.](../consume-packages/installing-signed-packages.md)

### <a name="lock-files"></a>Bloccare i file

**📦 Consumer di pacchetti**

I file di blocco archiviano l'hash del contenuto del pacchetto. Se l'hash del contenuto di un pacchetto da installare corrisponde al file di blocco, garantisce la ripetibilità del pacchetto.

Per abilitare i file di blocco, [vedere la documentazione seguente.](../consume-packages/package-references-in-project-files.md#locking-dependencies)

## <a name="monitor-your-supply-chain"></a>Monitorare la supply chain

### <a name="github-secret-scanning"></a>Analisi dei segreti di GitHub

**📦🖊 Autore del pacchetto**

GitHub analizza i repository per NuGet chiavi API per impedire usi fraudolenti di segreti di cui è stato accidentalmente eseguito il commit. 

Per altre informazioni sull'analisi dei segreti, vedere [Informazioni sull'analisi dei segreti.](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)

### <a name="author-package-signing"></a>Creare la firma dei pacchetti

**📦🖊 Autore del pacchetto**

[La firma dell'autore](../reference/signed-packages-reference.md) consente all'autore di un pacchetto di firmare la propria identità in un pacchetto e a un consumer di verificare che proveni dall'utente. Ciò consente di proteggersi dalla manomissione del contenuto e funge da unica fonte di verità sull'origine del pacchetto e sull'autenticità del pacchetto. In combinazione con i criteri di attendibilità client, è possibile verificare che un pacchetto proveniva da un autore specifico.

Per creare la firma di un pacchetto, vedere [Firmare un pacchetto.](../create-packages/sign-a-package.md)

### <a name="two-factor-authentication-2fa"></a>Two-Factor autenticazione a più fattori (2FA)

**📦🖊 Autore del pacchetto**

L'abilitazione dell'autenticazione a due fattori (2FA) può aggiungere un ulteriore livello di sicurezza quando si accede [all'account GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) o al repository di pacchetti pubblici [NuGet.org.](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa) È consigliabile abilitare l'autenticazione a due fattori per proteggere l'account.

### <a name="package-id-prefix-reservation"></a>Prenotazione del prefisso ID del pacchetto 

**📦🖊 Autore del pacchetto**

Per proteggere l'identità dei pacchetti, è possibile riservare un prefisso ID pacchetto al rispettivo spazio dei nomi per associare un proprietario corrispondente se il prefisso ID pacchetto rientra correttamente nei [criteri specificati.](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) 

Per informazioni sulla prenotazione dei prefissi ID, vedere [Prenotazione del prefisso ID pacchetto.](../nuget-org/id-prefix-reservation.md)

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Deprecazione e rimozione dall'elenco di un pacchetto vulnerabile

**📦🖊 Autore del pacchetto**

Per proteggere l'ecosistema di pacchetti .NET quando si è a conoscenza di una vulnerabilità in un pacchetto creato, fare del proprio meglio per deprecare e rimuovere il pacchetto dall'elenco in modo che sia nascosto agli utenti che cercano i pacchetti. Se si utilizza un pacchetto deprecato e non in elenco, è consigliabile evitare di utilizzarlo.

Per informazioni su come deprecare e rimuovere un pacchetto dall'elenco, vedere la documentazione seguente sulla deprecazione [e](../nuget-org/deprecate-packages.md) l'annullamento [dell'elenco dei pacchetti.](../nuget-org/policies/deleting-packages.md#unlisting-a-package)

## <a name="summary"></a>Riepilogo

La supply chain del software è qualsiasi elemento che entra o influisce sul codice. Anche se i compromessi della supply chain sono reali e in continua diffusione, sono comunque rari. Pertanto, la cosa più importante che è possibile fare è proteggere la supply chain conoscendo le **dipendenze,** gestendo le dipendenze e **monitorando la supply chain.**

Sono stati descritti diversi metodi NuGet e [GitHub](/learn/modules/maintain-secure-repository-github/) che sono attualmente disponibili per essere più efficaci nella visualizzazione, nella gestione e nel monitoraggio della supply chain.

Per altre informazioni sulla protezione del software del mondo, vedere The State of the Octoverse 2020 Security Report ( Report sulla sicurezza di [Octoverse 2020).](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)
