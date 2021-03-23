---
title: Procedure consigliate per una supply chain di software sicuro
description: Procedure consigliate per la sicurezza della supply chain software con NuGet & GitHub.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: e0f235d99e41e23a4551fbf7577f6c42e3381f5b
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859226"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Procedure consigliate per una supply chain di software sicuro

Open Source è ovunque. Si trova in molte codebase proprietarie e progetti della community. Per le organizzazioni e i singoli utenti, la domanda odierna non è se si usa o non si usa codice open source, ma il codice open source che si sta usando e quanto ancora.

Se non si è a conoscenza di ciò che si trova nella catena di approvvigionamento software, una vulnerabilità a Monte in una delle dipendenze può essere fatale, rendendo l'utente e i clienti vulnerabili a un potenziale compromesso. In questo documento si approfondirà il significato del termine "catena di approvvigionamento software", il motivo per cui è importante e il modo in cui è possibile proteggere la supply chain del progetto con le procedure consigliate.

![Stato del Octoverse 2020-Open Source](media/opensource-percent.png)

## <a name="dependencies"></a>Dependencies 

Il termine Supply Chain software viene usato per fare riferimento a tutti gli elementi che passano al software e da dove provengono. Sono le dipendenze e le proprietà delle dipendenze da cui dipende la supply chain di software. Una dipendenza è il software che deve essere eseguito. Può trattarsi di codice, file binari o altri componenti e da dove provengono, ad esempio un repository o un gestore di pacchetti.

Include la persona che ha scritto il codice, quando è stato aggiunto, il modo in cui è stato esaminato per i problemi di sicurezza, le vulnerabilità note, le versioni supportate, le informazioni sulle licenze e quasi tutte le operazioni che lo toccano in qualsiasi punto del processo.

La supply chain comprende anche altre parti dello stack oltre a una singola applicazione, ad esempio gli script di compilazione e creazione di pacchetti o il software che esegue l'infrastruttura su cui si basa l'applicazione.

## <a name="vulnerabilities"></a>Vulnerabilità

Attualmente, le dipendenze software sono pervasive. È piuttosto comune che i progetti usino centinaia di dipendenze open source per le funzionalità che non è necessario scrivere. Questo potrebbe significare che la maggior parte dell'applicazione è costituita da codice che non è stato creato. 

![Stato del Octoverse 2020-dipendenze](media/dependencies.png)

Le possibili vulnerabilità nelle dipendenze di terze parti o Open Source sono presumibilmente dipendenze che non è possibile controllare in modo rigoroso quanto il codice scritto, che può creare potenziali rischi per la sicurezza nella supply chain.

Se una di queste dipendenze presenta una vulnerabilità, è probabile che si disponga di una vulnerabilità. Questo può essere spaventoso perché una delle dipendenze può cambiare anche se non si conosce. Anche se una vulnerabilità esiste attualmente in una dipendenza, ma non è sfruttabile, può essere sfruttabile in futuro. 

La possibilità di sfruttare il lavoro di migliaia di sviluppatori open source e autori di librerie significa che migliaia di sconosciuti possono contribuire efficacemente direttamente al codice di produzione. Il prodotto, attraverso la supply chain di software, è interessato da vulnerabilità senza patch, errori innocenti o attacchi dannosi contro le dipendenze.

## <a name="supply-chain-compromises"></a>Compromessi Supply Chain

La definizione tradizionale di una supply chain deriva dalla produzione; si tratta della catena di processi necessari per creare e fornire qualcosa. Include la pianificazione, la fornitura di materiali, la produzione e la vendita al dettaglio. Una catena di approvvigionamento software è simile, ad eccezione dei materiali, bensì del codice. Anziché produrre, si tratta di uno sviluppo. Anziché scavare da zero, il codice viene originato da fornitori, commerciali o open source e, in generale, il codice open source deriva da repository. L'aggiunta di codice da un repository significa che il prodotto prende una dipendenza da tale codice.

Un esempio di attacco a catena di alimentazione software si verifica quando il codice dannoso viene aggiunto intenzionalmente a una dipendenza, usando la supply chain di tale dipendenza per distribuire il codice alle sue vittime. Gli attacchi supply chain sono reali. Sono disponibili molti metodi per attaccare una supply chain, inserendo direttamente il codice dannoso come nuovo collaboratore, per acquisire la proprietà di un account collaboratore senza che altri abbiano notato o addirittura compromettere una chiave di firma per distribuire software che non fa ufficialmente parte della dipendenza.

Un attacco a catena di alimentazione software si trova raramente nell'obiettivo finale, ma è l'inizio di un'opportunità per un utente malintenzionato di inserire malware o fornire una backdoor per l'accesso futuro.

![Stato del ciclo di vita della vulnerabilità Octoverse 2020](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Software senza patch

Attualmente l'uso di Open Source è significativo e non è previsto un rallentamento imminente. Dato che non verrà interrotto l'uso di software open source, la minaccia per la sicurezza della supply chain è il software senza patch. In che modo è possibile risolvere il rischio che una dipendenza del progetto abbia una vulnerabilità?

- **Conoscere le funzionalità dell'ambiente.** Questa operazione richiede l'individuazione delle dipendenze e di eventuali dipendenze transitive per comprendere i rischi di tali dipendenze, ad esempio vulnerabilità o restrizioni di licenza.
- **Gestire le dipendenze.** Quando viene individuata una nuova vulnerabilità di sicurezza, è necessario determinare se si è interessati e, in tal caso, eseguire l'aggiornamento alla versione più recente e alla patch di sicurezza disponibile. Questo è particolarmente importante per esaminare le modifiche che introducono nuove dipendenze o controllano regolarmente le dipendenze precedenti.
- **Monitorare la supply chain.** Questa operazione viene controllata controllando i controlli disponibili per la gestione delle dipendenze. Ciò consentirà di applicare condizioni più restrittive da soddisfare per le dipendenze.

![Stato dei Octoverse 2020-Advisor](media/advisories.png)

Vengono illustrati diversi strumenti e tecniche offerti da NuGet e GitHub, che è possibile utilizzare oggi per risolvere i potenziali rischi all'interno del progetto. 

## <a name="knowing-what-is-in-your-environment"></a>Conoscenza di ciò che si trova nell'ambiente

### <a name="nuget-dependency-graph"></a>Grafico delle dipendenze NuGet

**📦 Utente del pacchetto**

È possibile visualizzare le dipendenze NuGet nel progetto esaminando direttamente il rispettivo file di progetto.

Si trova in genere in una delle due posizioni seguenti:

-   [`packages.config`](../reference/packages-config.md) : Si trova nella radice del progetto.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) : Si trova nel file di progetto. 

A seconda del metodo usato per gestire le dipendenze di NuGet, è anche possibile usare Visual Studio per visualizzare le dipendenze direttamente in [Esplora soluzioni](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) o in [Gestione pacchetti NuGet](../consume-packages/install-use-packages-visual-studio.md).

Per gli ambienti dell'interfaccia della riga di comando, è possibile usare il [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) comando per elencare le dipendenze del progetto o della soluzione. 

Per ulteriori informazioni sulla gestione delle dipendenze NuGet, [vedere la documentazione seguente](../consume-packages/overview-and-workflow.md).

### <a name="github-dependency-graph"></a>Grafico delle dipendenze di GitHub 

**📦 Consumer del pacchetto | 📦🖊 Autore del pacchetto**

È possibile usare il grafico delle dipendenze di GitHub per visualizzare i pacchetti da cui dipende il progetto e i repository che dipendono da esso. Questo può essere utile per visualizzare eventuali vulnerabilità rilevate nelle relative dipendenze.

Per ulteriori informazioni sulle dipendenze del repository GitHub, [vedere la documentazione seguente](https://github.co/dependency-graph).

### <a name="dependency-versions"></a>Versioni delle dipendenze

**📦 Consumer del pacchetto | 📦🖊 Autore del pacchetto**

Per garantire una supply chain di dipendenze sicura, è necessario assicurarsi che tutte le dipendenze & gli strumenti vengano aggiornati regolarmente alla versione stabile più recente, in quanto spesso includono le funzionalità più recenti e le patch di sicurezza per le vulnerabilità note. Le dipendenze possono includere il codice da cui dipende, i file binari utilizzati, gli strumenti usati e altri componenti. Questo può includere:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [.NET SDK & Runtime](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [Pacchetti NuGet](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Gestione delle dipendenze

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>Dipendenze deprecate e vulnerabili di NuGet

**📦 Consumer del pacchetto | 📦🖊 Autore del pacchetto**

È possibile usare l' [interfaccia](/dotnet/core/tools/dotnet-list-package) della riga di comando di DotNet per elencare eventuali dipendenze deprecate o vulnerabili note che potrebbero essere presenti all'interno del progetto o della soluzione. È possibile usare il comando `dotnet list package --deprecated` o `dotnet list package --vulnerable` per fornire un elenco di eventuali deprecazioni o vulnerabilità note.

### <a name="github-vulnerable-dependencies"></a>Dipendenze vulnerabili di GitHub

**📦 Consumer del pacchetto | 📦🖊 Autore del pacchetto**

Se il progetto è ospitato in GitHub, è possibile sfruttare la [sicurezza di GitHub](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) per individuare le vulnerabilità e gli errori di sicurezza nel progetto e Dependabot li correggerà aprendo una richiesta pull per la codebase. 

Il rilevamento delle dipendenze vulnerabili prima che vengano introdotte è uno degli obiettivi del movimento ["Shift Left"](https://en.wikipedia.org/wiki/Shift-left_testing) . La possibilità di ottenere informazioni sulle dipendenze, ad esempio la licenza, le dipendenze transitive e l'età delle dipendenze, consente di eseguire questa operazione.

Per ulteriori informazioni sugli avvisi di Dependabot & gli aggiornamenti [della sicurezza, vedere la documentazione seguente](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).

### <a name="nuget-feeds"></a>Feed NuGet

**📦 Utente del pacchetto**

Quando si usano più feed di origine NuGet privati & pubblici, un pacchetto può essere scaricato da uno qualsiasi dei feed. Per garantire che la compilazione sia prevedibile e sicura da attacchi noti, ad esempio dalla [confusione delle dipendenze](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610), la procedura consigliata consiste nel sapere quali feed specifici provengono dai pacchetti. È possibile usare un feed singolo o un feed privato con funzionalità di upstream per la protezione.

Per ulteriori informazioni su come proteggere i feed di pacchetti, vedere [3 modi per attenuare i rischi quando si utilizzano i feed di pacchetti privati](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).

### <a name="client-trust-policies"></a>Criteri di attendibilità client

**📦 Utente del pacchetto**

Esistono criteri a cui è possibile acconsentire esplicitamente, in cui è necessario che i pacchetti usati siano firmati. In questo modo è possibile considerare attendibile l'autore di un pacchetto, purché sia firmato dall'autore, oppure considerare attendibile un pacchetto se appartiene a un utente o a un account specifico che è il repository firmato da NuGet.org.

Per configurare i criteri di attendibilità del client, [vedere la documentazione seguente](../consume-packages/installing-signed-packages.md).

### <a name="lock-files"></a>Blocca file

**📦 Utente del pacchetto**

I file di blocco archiviano l'hash del contenuto del pacchetto. Se l'hash del contenuto di un pacchetto che si desidera installare corrisponde al file di blocco, verrà garantita la ripetibilità del pacchetto.

Per abilitare i file di blocco, [vedere la documentazione seguente](../consume-packages/package-references-in-project-files.md#locking-dependencies).

## <a name="monitor-your-supply-chain"></a>Monitorare la supply chain

### <a name="github-secret-scanning"></a>Analisi dei segreti di GitHub

**📦🖊 Autore del pacchetto**

GitHub analizza i repository per le chiavi API NuGet per impedire l'uso fraudolento di segreti di cui è stato eseguito il commit accidentale. 

Per altre informazioni sull'analisi dei segreti, vedere [informazioni sull'analisi dei](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)segreti.

### <a name="author-package-signing"></a>Creazione firma pacchetto

**📦🖊 Autore del pacchetto**

La [firma dell'autore](../reference/signed-packages-reference.md) consente a un autore di pacchetti di contrassegnare l'identità in un pacchetto e a un consumer di verificarne il risultato. In questo modo si evita la manomissione del contenuto e funge da singola fonte di verità sull'origine del pacchetto e sull'autenticità del pacchetto. In combinazione con i criteri di attendibilità del client, è possibile verificare che un pacchetto provenga da un autore specifico.

Per creare la firma di un pacchetto, vedere [firmare un pacchetto](../create-packages/sign-a-package.md).

### <a name="two-factor-authentication-2fa"></a>Autenticazione Two-Factor (2FA)

**📦🖊 Autore del pacchetto**

L'abilitazione dell'autenticazione a due fattori (2FA) può aggiungere un ulteriore livello di sicurezza quando si [accede all'account github](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) o al [repository del pacchetto pubblico NuGet.org](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa). È consigliabile abilitare l'autenticazione a due fattori per proteggere l'account.

### <a name="package-id-prefix-reservation"></a>Prenotazione del prefisso ID del pacchetto 

**📦🖊 Autore del pacchetto**

Per proteggere l'identità dei pacchetti, è possibile riservare un prefisso di ID pacchetto al rispettivo spazio dei nomi per associare un proprietario corrispondente se il prefisso dell'ID pacchetto rientra correttamente nei [criteri specificati](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria). 

Per informazioni su come riservare i prefissi ID, vedere [prenotazione prefisso ID pacchetto](../nuget-org/id-prefix-reservation.md).

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Deprecazione e annullamento dell'elenco di un pacchetto vulnerabile

**📦🖊 Autore del pacchetto**

Per proteggere l'ecosistema di pacchetti .NET quando si è a conoscenza di una vulnerabilità in un pacchetto che è stato creato, è consigliabile deprecare e rimuovere l'elenco del pacchetto in modo che sia nascosto agli utenti che cercano i pacchetti. Se si utilizza un pacchetto deprecato e non incluso nell'elenco, è consigliabile evitare di utilizzare il pacchetto.

Per informazioni su come deprecare e non elencare un pacchetto, vedere la documentazione seguente su come [deprecare](../nuget-org/deprecate-packages.md) e non [elencare i pacchetti](../nuget-org/policies/deleting-packages.md#unlisting-a-package).

## <a name="summary"></a>Riepilogo

La supply chain del software è qualsiasi elemento che entra in o influisca sul codice. Anche se i compromessi della catena di fornitura sono reali e crescono in popolarità, sono ancora rari; quindi, la cosa più importante da fare è proteggere la supply chain tenendo **conto delle dipendenze, gestendo le dipendenze** e **monitorando la supply chain.**

Sono stati appresi i vari metodi forniti da NuGet e [GitHub](/learn/modules/maintain-secure-repository-github/) che sono attualmente disponibili per essere più efficaci nella visualizzazione, nella gestione e nel monitoraggio della supply chain.

Per ulteriori informazioni sulla protezione del software del mondo, vedere [lo stato del report sulla sicurezza di Octoverse 2020](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).
