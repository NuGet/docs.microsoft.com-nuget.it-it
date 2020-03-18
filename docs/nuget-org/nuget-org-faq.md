---
title: Domande frequenti su NuGet.org
description: Domande frequenti e relative risposte per l'uso della raccolta NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 915f6e4cfc0b21d2b10006c62e8230720d07ce74
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428905"
---
# <a name="nugetorg-frequently-asked-questions"></a>Domande frequenti su NuGet.org

## <a name="license-terms"></a>Condizioni di licenza

**Quali sono le condizioni di licenza predefinite se un pacchetto non include informazioni di licenza specifiche?**

Ogni pacchetto è disciplinato dalle condizioni incluse nel pacchetto. È necessario leggere le condizioni applicabili prima di accedere, scaricare o acquisire qualsiasi pacchetto. In NuGet.org, usare il collegamento **License Info** (Informazioni di licenza) nella pagina del pacchetto.

Se per un pacchetto non sono specificate le condizioni di licenza, contattare il proprietario del pacchetto direttamente usando il collegamento **Contact owners** (Contatta proprietari) nella pagina del pacchetto su NuGet.org. Microsoft non concede in licenza all'utente alcuna proprietà intellettuale dei provider di pacchetti di terze parti e non è responsabile per le informazioni fornite da terze parti.

## <a name="managing-packages-on-nugetorg"></a>Gestione dei pacchetti in NuGet.org

**È possibile modificare i metadati del pacchetto dopo che è stato caricato?**

NuGet consiglia che tutti i pacchetti siano firmati. Uno dei principi di progettazione della firma dei pacchetti è che il contenuto del pacchetto firmato non deve essere modificabile e ciò include il file nuspec. La modifica dei metadati del pacchetto comporta modifiche al file nuspec, invalidando le firme esistenti. Si consiglia di modificare i flussi di lavoro esistenti in modo da non richiedere la modifica dei metadati del pacchetto dopo aver creato il pacchetto.

Si noti che le dipendenze elencate per il pacchetto vengono generate automaticamente dal pacchetto stesso e non possono essere modificate.

Il caricamento dei pacchetti in [int.nugettest.org](https://int.nugettest.org) è anche un ottimo modo per testare e convalidare il pacchetto senza rendere disponibile un pacchetto nella raccolta pubblica. Endpoint API: https://apiint.nugettest.org/v3/index.json

**È possibile eliminare un pacchetto pubblicato in NuGet.org?**

In generale, non è supportata l'eliminazione di un pacchetto pubblicato in NuGet.org. Scopri di più sui [criteri per l'eliminazione di pacchetti](policies/deleting-packages.md).

**È possibile riservare nomi per i pacchetti che verranno pubblicati in futuro?**

Sì. È possibile riservare ID per i pacchetti in [NuGet.org](https://www.nuget.org/) richiedendo un prefisso per l'ID dei pacchetti per l'account. Per richiedere un prefisso per l'ID dei pacchetti, seguire le istruzioni nella [documentazione](id-prefix-reservation.md).

**Come è possibile ottenere l'attestazione di proprietà per i pacchetti?**

Vedere [Gestione dei proprietari dei pacchetti in NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Qual è la procedura per gestire il caso di un proprietario di pacchetto che viola una licenza di software?**

Microsoft incoraggia la collaborazione tra i membri della community di NuGet per risolvere eventuali controversie tra i proprietari di pacchetti e i proprietari di altro software. È stato elaborato un [processo di risoluzione delle controversie](policies/dispute-resolution.md) da seguire prima di chiedere l'intercessione degli amministratori di NuGet.org.

**È consigliabile caricare i pacchetti di test in NuGet.org?**

A scopo di test, è possibile usare [int.nugettest.org](https://int.nugettest.org) o server NuGet pubblici alternativi, come [myget.org](https://myget.org) o [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Si noti che i pacchetti caricati in int.nugettest.org potrebbero non essere mantenuti.

**Quali sono le dimensioni massime per i pacchetti che è possibile caricare in NuGet.org?**

NuGet.org consente pacchetti fino a 250 MB, ma è consigliabile mantenere dimensioni inferiori a 1 MB per i pacchetti se possibile e usare le dipendenze per collegare i pacchetti. Come regola generale, i pacchetti contengono un solo assembly per evitare conflitti.

NuGet usa HTTP per scaricare i pacchetti, pertanto per i pacchetti di dimensioni maggiori sono più probabili errori di installazione rispetto a quelli più piccoli.

È possibile condividere le dipendenze tra più pacchetti, riducendo le dimensioni totali del download per i consumer dei pacchetti NuGet.

Le dipendenze sono prevalentemente statiche e non cambiano mai. Quando si corregge un bug nel codice, è possibile che non occorra aggiornare le dipendenze. Se si aggregano le dipendenze, alla fine diventa necessario ripubblicare ogni volta pacchetti più grandi. Suddividendo i pacchetti NuGet in dipendenze correlate, gli aggiornamenti sono molto più selezionati per i consumer del pacchetto.

## <a name="nugetorg-not-accessible"></a>NuGet.org non accessibile

**Perché non è possibile scaricare o caricare pacchetti in NuGet.org?**

Verificare innanzitutto di usare le versioni più recenti di NuGet. Se il problema persiste anche con la versione più recente, [contattare il supporto tecnico](https://www.nuget.org/policies/Contact) e fornire informazioni aggiuntive per la risoluzione del problema di connessione, tra cui:

- Versione di NuGet in uso
- Origini dei pacchetti in uso
- Log di ripristino con livello di dettaglio massimo
- Tracce MTR o Fiddler (vedere più avanti)
- Area geografica
- Se il computer è protetto da proxy o firewall
- Se il computer si trova nel data center di un provider di servizi cloud (Azure, AWS e così via) In caso affermativo, specificare il nome del provider e l'area.

*Per acquisire una traccia MTR:*

- Scaricare [WinMTR](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download).
- Immettere `api.nuget.org` come nome host e fare clic su **Start** (Avvia).
- Attendere fino a quando il valore indicato nella colonna **Sent** (Inviati) è > = 100.

    ![Acquisizione di una traccia MTR](media/mtr.png)

- Copiare il testo negli Appunti.

*Per acquisire una traccia Fiddler:*

- Installare la versione più recente di [Fiddler](https://www.telerik.com/download/fiddler).
- Avviare Fiddler e disabilitare l'acquisizione del traffico tramite il menu **File > Capture Traffic** (File > Acquisisci traffico).
- Rimuovere tutte le sessioni (selezionare tutti gli elementi nell'elenco e premere **CANC**).
- Configurare Fiddler per acquisire il traffico HTTPS selezionando **Decrypt HTTPS traffic** (Decrittografa traffico HTTPS) nella scheda **HTTPS** nel menu **Tools > Fiddler Options** (Strumenti > Opzioni Fiddler).
- Chiudere Visual Studio.
- Abilitare il menu **File > Capture Traffic** (File > Acquisisci traffico).
- Avviare Visual Studio o nuget.exe ed eseguire le azioni che non funzionano. Il traffico generato da queste azioni dovrebbe essere visualizzato in Fiddler.
- Dopo aver eseguito le azioni, usare **File > Save > All Sessions** (File > Salva > Tutte le sessioni) per archiviare le sessioni acquisite.

Nota: può essere richiesto di impostare la variabile di ambiente `HTTP_PROXY` su `http://127.0.0.1:8888` per il routing del traffico NuGet attraverso Fiddler.

Se il problema persiste, provare i [suggerimenti indicati in questo post di StackOverflow](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>Gestione degli account di NuGet.org

### <a name="how-to-recover-nugetorg-password-login"></a>Come si recupera l'accesso tramite password di NuGet.org?

Si noti che l'[accesso tramite password di NuGet.org è stato sospeso](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) ed è possibile accedere a NuGet.org unicamente con un account Microsoft personale (MSA) o con un account di Azure Active Directory (AAD). Se tuttavia non si è in grado di accedere agli account AAD o MSA associati, può essere necessario usare l'accesso tramite password per recuperare l'account di NuGet.org. In questa situazione, seguire questa procedura.
- **Requisito:** Sarà necessario avere accesso al messaggio di posta elettronica associato all'account per il quale è necessario ripristinare la password.
- Andare alla [pagina Forgot password](https://www.nuget.org/account/ForgotPassword) (Password dimenticata)
- Immettere l'indirizzo di **posta elettronica** associato all'account di NuGet.org che si vuole recuperare.
- Fare clic sul pulsante **Invia**.
- All'account dell'indirizzo di posta elettronica specificato si riceverà un messaggio con il collegamento per la reimpostazione della password. Fare clic su questo collegamento e impostare la nuova password. Se non si riesce a trovare il messaggio, controllare la cartella "Posta indesiderata".
- Al termine, sarà possibile accedere con nome utente e password a NuGet.
- Per accedere con nome utente e password, usare il collegamento **Sign in using Nuget.org account** (Accedi con l'account di Nuget.org) nella [pagina di accesso di NuGet.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Quale account Microsoft è collegato all'account di NuGet.org?

Se non si ricorda a quale account Microsoft è associato l'account di NuGet.org, seguire questa procedura per ottenere assistenza.
1. Passare alla [pagina di accesso di NuGet.org](https://www.nuget.org/users/account/LogOn) e fare clic sul collegamento **Need assistance signing in?** (Serve assistenza per l'accesso?).
1. Verrà visualizzata la finestra di dialogo popup di assistenza. Seguire i passaggi descritti in questa finestra di dialogo per risalire all'account o gli account Microsoft associati all'account di NuGet.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Come si cambia l'account Microsoft usato per l'accesso a NuGet.org?
Se si vuole cambiare l'account Microsoft per l'utente di NuGet.org, seguire questa procedura. Si supponga che l'account Microsoft con indirizzo di posta elettronica `account1@outlook.com` sia associato all'account di NuGet.org con nome utente `MyNuGetAccount`. Si vuole cambiare l'account di accesso con un altro account Microsoft con indirizzo di posta elettronica `account2@outlook.com`
1. Accedere usando **l'account Microsoft attualmente associato**, vale a dire `account1@outlook.com`, nella [pagina di accesso](https://www.nuget.org/users/account/LogOn) dopo aver fatto clic su **Sign in with Microsoft** (Accedi con Microsoft).
1. Dopo l'accesso, passare alla pagina [Account settings](https://www.nuget.org/account) (Impostazioni account).
1. Espandere la sezione **Login Account** (Account di accesso). Fare clic sul pulsante **Change Account** (Cambia account).
1. Verrà effettuato il reindirizzamento alla pagina di accesso Microsoft. Accedere con l'account a cui si vuole modificare l'associazione, ad esempio `account2@outlook.com`. **Nota**: potrebbe essere necessario fare clic su **disconnettersi e accedere con un account diverso** durante il flusso di accesso per poter accedere con un account Microsoft diverso.
1. Se viene visualizzato un errore simile a quello riportato di seguito, vedere [L'account Microsoft è collegato a un altro account di NuGet.org](#microsoft-account-is-linked-with-another-nugetorg-account) per altri dettagli.
    >_Non è stato possibile aggiornare il account Microsoft con ' Account2 <account2@outlook.com>'. Questo problema può verificarsi se è già collegato a un altro account NuGet. Per ulteriori informazioni, contattare il supporto tecnico._

1. Dopo l'accesso con il secondo account, verrà effettuato il reindirizzamento alla pagina Account settings (Impostazioni account) di NuGet.org. Come account di accesso è ora associato il nuovo account Microsoft. D'ora in avanti sarà necessario usare questo account per l'accesso a NuGet.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>L'account Microsoft è collegato a un altro account di NuGet.org.

Se si è tentato di cambiare l'account di accesso Microsoft ed è stato visualizzato l'errore seguente:
> _Non è stato possibile aggiornare il account Microsoft con ' Account2 <account2@outlook.com>'. Questo problema può verificarsi se è già collegato a un altro account NuGet. Per ulteriori informazioni, contattare il supporto tecnico._

Per l'utente di NuGet.org con nome utente `account1@outlook.com`, si supponga di aver tentato di cambiare l'account di accesso Microsoft da `MyNuGetAccount1` a un altro account Microsoft con indirizzo di posta elettronica `account2@outlook.com` e che sia visualizzato l'errore sopra riportato.

**Che cosa significa l'errore sopra riportato?**

Significa che esiste un altro account NuGet.org account associato all'account Microsoft a cui si sta tentando di passare. Nell'esempio precedente, l'account Microsoft con indirizzo di posta elettronica `<account2@outlook.com>` è associato a un altro account di NuGet.org, ad esempio a un account con nome utente `MyNuGetAccount2`.

Non è possibile cambiare l'account di accesso associato con un account Microsoft collegato a un altro account di NuGet.org.

**Se si è dimenticato di avere un altro account di NuGet.org, come è possibile sapere di quale account si tratta?**

Accedere con la seconda account Microsoft nella [pagina di accesso](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "pagina di accesso"). In questo modo si accederà all'account di NuGet.org attualmente associato al secondo account Microsoft. Sarà quindi possibile visualizzare i pacchetti caricati ed eseguire operazioni di gestione di questo account.

**Non sono interessati a questo secondo account NuGet.org, desidero modificare l'accesso per il primo account NuGet.org con la seconda account Microsoft. Cosa devo fare?**

Il secondo account di NuGet.org non serve e si vuole comunque riutilizzare l'account Microsoft associato con indirizzo di posta elettronica `account2@outlook.com`. 

È possibile rilasciare l'associazione tra l'account Microsoft e l'account di NuGet.org eliminando quest'ultimo.
1. Seguire i passaggi necessari per [eliminare un utente](#how-to-delete-my-nugetorg-account) per il secondo account di NuGet.org `MyNuGetAccount2`. 
1. Dopo l'eliminazione dell'account, è possibile riprovare la procedura per [cambiare l'account di accesso Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Si è interessati anche a questo secondo account. Non si desidera perdere questo account, ma modificare gli account di accesso associati per il primo account.**

È necessario creare o usare un terzo account Microsoft, ad esempio con indirizzo di posta elettronica `account3@outlook.com`. 
1. Per prima cosa è necessario effettuare l'accesso con la seconda account Microsoft `account2@outlook.com` in NuGet.org. Attenersi alla procedura descritta in precedenza per modificare gli account di accesso associati e associare la terza account Microsoft a questo account NuGet.org.
1. Al termine, il secondo account Microsoft con indirizzo di posta elettronica `account2@outlook.com` è libero e può essere associato al primo account di NuGet.org, `MyNuGetAccount1`. Seguire gli stessi passaggi per cambiare l'account di accesso Microsoft per il secondo account Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Se si accede con l'account Microsoft, si può vedere che l'indirizzo di posta elettronica è collegato a un altro account Microsoft

Se si è tentato di accedere con l'account Microsoft, ad esempio con quello con indirizzo di posta elettronica `account1@outlook.com` e viene visualizzato un errore simile al seguente:
> _The account with email 'account1@outlook.com' is linked with another microsoft account._
>
> _If you would like to update the linked Microsoft account you can do so from the account settings page._ (L'account con email 'account1@outlook.com' è collegato a un altro account Microsoft. Se si vuole aggiornare l'account Microsoft collegato, è possibile farlo dalla pagina Impostazioni account)

**Che cosa significa l'errore sopra riportato?**

Quando viene creato un account in NuGet.org, a tale account è associato un indirizzo di posta elettronica di comunicazione. Si tratta in genere dello stesso indirizzo di posta elettronica usato per l'account Microsoft associato. È tuttavia possibile scegliere per la comunicazione un altro indirizzo di posta elettronica. Tecnicamente, quindi, è possibile avere un account Microsoft diverso, ad esempio con `account2@outlook.com`, collegato all'account di NuGet.org con indirizzo di posta elettronica di comunicazione `account1@outlook.com`.

Quindi, l'errore precedente indica che esiste già un account NuGet.org con indirizzo di posta elettronica di comunicazione `account1@outlook.com` ma è associato a un altro account Microsoft con posta elettronica **che non è** `account1@outlook.com`.

**Come è possibile scoprire quale account Microsoft è collegato a un account di NuGet.org?**

È consigliabile usare il flusso di [assistenza all'accesso](#which-microsoft-account-is-linked-to-my-nugetorg-account) per determinare quale account Microsoft è collegato all'account di NuGet.org con l'indirizzo di posta elettronica `account1@outlook.com`.

**Si vuole sostituire tale account con un account Microsoft**

Seguire i passaggi descritti nella sezione [Non è possibile usare l'account di accesso Microsoft. Come si recupera l'account di NuGet.org?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) per associare il proprio account Microsoft all'account di NuGet.org esistente.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Non è possibile usare l'account di accesso Microsoft. Come si recupera l'account di NuGet.org?

Se si è provato a usare l'[assistenza all'accesso](#which-microsoft-account-is-linked-to-my-nugetorg-account) e non si ha accesso all'account Microsoft associato all'account di NuGet.org, attenersi alla procedura seguente per collegare un nuovo account Microsoft all'account di NuGet.org.
1. **Requisito**: è necessario accedere a un account Microsoft che non è associato ad alcun account NuGet.org esistente. Se non se ne ha alcuno, è possibile [crearne uno](https://signup.live.com).
2. Se si dimenticano il nome utente e la password per l'account di NuGet.org, seguire la [procedura per ripristinare l'account di accesso con password](#how-to-recover-nugetorg-password-login).
3. [Accedere a NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) usando l'account di accesso tramite nome utente e password.
4. Dopo l'accesso, verrà visualizzata la finestra di dialogo popup illustrata più avanti. Si tratta di finestra di dialogo che informa della sospensione delle password.
5. **Nota**: ignorare l'istruzione per eseguire l'accesso con il account Microsoft specificato. È ora possibile collegare l'account di NuGet.org a qualsiasi altro account di accesso Microsoft.
6. Fare clic sul pulsante **Sign in with Microsoft** (Accedi con Microsoft) e accedere con l'account Microsoft a cui si ha accesso, come indicato nel passaggio 1.
7. L'account è ora collegato al nuovo account Microsoft, che d'ora in avanti potrà essere usato per accedere a NuGet.org.

    ![Finestra di dialogo di collegamento MSA](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Come è possibile trasformare l'account di NuGet.org in un'organizzazione?

Se si vuole trasformare l'account in un'organizzazione e l'account è già associato a un account di accesso Microsoft, seguire i passaggi indicati nella documentazione relativa a [organizzazioni in nuget org](organizations-on-nuget-org.md).

Se tuttavia l'account NuGet.org non è associato o collegato a un account Microsoft, la procedura seguente consente di trasformare l'account in un'organizzazione.
1. **Requisito**: è necessario avere un singolo account creato per la prima volta in NuGet.org da usare come amministratore nell'account dell'organizzazione. Se non se ne ha alcuno, [creare un nuovo account di NuGet.org](individual-accounts.md).
2. Seguire i [passaggi per recuperare l'account di accesso tramite password](#how-to-recover-nugetorg-password-login) per l'account di NuGet.org, se tale account non è disponibile. In caso contrario, ignorare questo passaggio.
3. [Accedere a NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) usando l'account di accesso tramite nome utente e password.
4. Dopo l'accesso, verrà visualizzata la finestra di dialogo popup illustrata più avanti. Si tratta di finestra di dialogo che informa della sospensione delle password. 
    > [!Important]
    > Ignorare questa finestra di dialogo, **non** fare clic sul pulsante **Sign in with Microsoft** (Accedi con Microsoft).

5. Passare a [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform). In questo modo sarà possibile convertire l'account di NuGet.org in un'organizzazione senza collegamento a un account Microsoft.
6. Specificare il nome utente amministratore per l'account di NuGet.org personale o l'account creato nel passaggio 1.
7. Seguire le istruzioni per completare la trasformazione di questo account in un'organizzazione.

    ![Finestra di dialogo di collegamento MSA](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>Problemi di accesso a NuGet.org per gli account AAD con tenant non gestito

Se durante il flusso di accesso con il dominio dell'account di posta elettronica (@yourdomain.com) viene visualizzato un errore simile a quello che segue, vedere la procedura riportata più avanti per recuperare l'account di NuGet.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Che cos'è questa operazione di stato non gestito durante l'accesso? E perché si sta verificando adesso?** 

L'account è stato registrato in precedenza come account Microsoft personale e ha funzionato senza problemi. Ora, tuttavia, sembra che sia stato registrato come tenant "non gestito" in Azure Active Directory (il servizio di gestione delle identità usato per autenticare gli account Microsoft). 

Questo può essere accaduto se l'utente corrente o un altro utente dell'organizzazione (con indirizzo di posta elettronica @yourdomain.com) si è registrato con uno dei servizi integrati di AAD o ha effettuato un'[iscrizione self-service per Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-self-service-signup), che crea un tenant "non gestito"per il dominio dell'account Microsoft usato (@yourdomain.com in questo caso). 

**Cosa si può fare per recuperare l'account?**

In questo momento NuGet.org non è in grado di autenticare gli account con tali account tenant "non gestiti" in Azure Active Directory. È in corso la ricerca di un modo più efficiente di autenticare tali account.

Se vuole accedere a NuGet.org con l'account Microsoft (@yourdomain.com), l'utente (o un amministratore della società) dovrà attestare la proprietà dell'account tenant AAD tramite una convalida DNS per l'autenticazione degli utenti con indirizzo di posta elettronica "@yourdomain.com". Seguire la procedura per l'[acquisizione come amministratore di domini](https://docs.microsoft.com/azure/active-directory/users-groups-roles/domains-admin-takeover) documentata da Azure Active Directory. Dopo l'esecuzione della procedura, l'accesso normale inizierà a funzionare.

**Se non si vogliono eseguire tutte queste operazioni, qual è l'altro modo per recuperare l'account?**

È possibile [creare](https://www.microsoft.com/account) un nuovo account Microsoft (con un indirizzo e-mail **non** associato a @yourdomain.com). Seguire i passaggi descritti nella sezione [Recuperare l'account di NuGet.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account).

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Come si cambia il nome utente dell'account di NuGet.org?

Non è possibile. Per quanto riguarda i criteri, non è possibile modificare i nomi utente. Questa operazione è inoltre una modifica sostanziale per gli utenti che possono avere definito [criteri di attendibilità del pacchetto in base al proprietario del pacchetto](../consume-packages/installing-signed-packages.md#trust-package-owners). L'unico modo per cambiare il nome utente consiste nel creare un nuovo account con il nome utente desiderato. È consigliabile eliminare l'account esistente prima di crearne uno nuovo. In caso contrario non sarà possibile riutilizzare l'account Microsoft registrato.
> [!Important]
> L'eliminazione dell'utente **mantiene riservato**`username`. Non sarà possibile riutilizzare lo stesso nome utente, **neanche cambiando alcune lettere in maiuscole o minuscole**. Se, ad esempio, è stato creato un utente con nome utente `mycoolname` e si vuole cambiare quest'ultimo in `MyCoolName` (modifica di maiuscole e minuscole), questa operazione non sarà possibile dopo l'eliminazione dell'utente.

Seguire i passaggi descritti nelle sezioni [Eliminare l'account di NuGet.org](#how-to-delete-my-nugetorg-account) e quindi [registrare un nuovo account](individual-accounts.md) con il nome utente corretto.

### <a name="how-to-delete-my-nugetorg-account"></a>Come si elimina l'account di NuGet.org?

Per eliminare l'account, si noti che è consigliabile trasferire la proprietà di tutti i pacchetti di cui l'account da eliminare è l'unico proprietario. Altre informazioni sulla [gestione dei proprietari dei pacchetti](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg) e su come eseguire questa operazione. Ciò risulta utile anche per accelerare la richiesta.

Se si desidera trasformare l'account in un'organizzazione, seguire la procedura descritta in [Trasformare l'account personale di NuGet.org in un'organizzazione](#how-to-transform-my-nugetorg-account-to-an-organization).

> [!Important]
> L'eliminazione dell'utente avrà i risultati seguenti:
>  1. Il nome utente sarà riservato e nessuno potrà riutilizzarlo per creare un account personale o un account dell'organizzazione.
>  1. Revoca delle chiavi API associate. 
>  1. Rimozione dell'account come proprietario per tutti i pacchetti figlio.
>  1. Annullamento dell'associazione di tutte le prenotazioni di prefisso ID esistenti in precedenza per l'account.
>  1. Rimozione dell'account come membro di tutte le organizzazioni.

Seguire questi passaggi per procedere con l'eliminazione dell'account.
1. [Accedere a NuGet.org](https://www.nuget.org/users/account/LogOn) con l'account da eliminare.
2. Fare clic sull'URL [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) e seguire i passaggi per inviare la richiesta di eliminazione dell'account.

L'assistenza clienti elaborerà la richiesta ed eseguirà l'eliminazione dell'account.
