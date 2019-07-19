---
title: Comando origini CLI NuGet
description: Informazioni di riferimento sul comando NuGet. exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327598"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="c0690-103">Comando sources (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="c0690-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="c0690-104">**Si applica a:** utilizzo del pacchetto &bullet; , pubblicazione delle **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="c0690-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c0690-105">Gestisce l'elenco delle origini presenti nel file di configurazione dell'ambito utente o in un file di configurazione specificato.</span><span class="sxs-lookup"><span data-stu-id="c0690-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="c0690-106">Il file di configurazione dell'ambito utente si `%appdata%\NuGet\NuGet.Config` trova in (Windows `~/.nuget/NuGet/NuGet.Config` ) e (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c0690-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="c0690-107">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="c0690-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="c0690-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="c0690-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="c0690-109">dove `<operation>` è un *elenco, Aggiungi, Rimuovi, Abilita, Disabilita* o *Aggiorna* `<name>` è il nome dell'origine e `<source>` è l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="c0690-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="c0690-110">È possibile operare su una sola origine alla volta.</span><span class="sxs-lookup"><span data-stu-id="c0690-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="c0690-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="c0690-111">Options</span></span>

| <span data-ttu-id="c0690-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="c0690-112">Option</span></span> | <span data-ttu-id="c0690-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c0690-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0690-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c0690-114">ConfigFile</span></span> | <span data-ttu-id="c0690-115">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="c0690-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c0690-116">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c0690-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c0690-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c0690-117">ForceEnglishOutput</span></span> | <span data-ttu-id="c0690-118">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="c0690-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c0690-119">Formato</span><span class="sxs-lookup"><span data-stu-id="c0690-119">Format</span></span> | <span data-ttu-id="c0690-120">Si applica all' `list` azione e può essere `Detailed` (impostazione predefinita) o `Short`.</span><span class="sxs-lookup"><span data-stu-id="c0690-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="c0690-121">?</span><span class="sxs-lookup"><span data-stu-id="c0690-121">Help</span></span> | <span data-ttu-id="c0690-122">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="c0690-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="c0690-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c0690-123">NonInteractive</span></span> | <span data-ttu-id="c0690-124">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c0690-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c0690-125">Password</span><span class="sxs-lookup"><span data-stu-id="c0690-125">Password</span></span> | <span data-ttu-id="c0690-126">Specifica la password per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="c0690-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="c0690-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="c0690-127">StorePasswordInClearText</span></span> | <span data-ttu-id="c0690-128">Indica per archiviare la password in testo non crittografato anziché il comportamento predefinito di archiviazione di un modulo crittografato.</span><span class="sxs-lookup"><span data-stu-id="c0690-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="c0690-129">UserName</span><span class="sxs-lookup"><span data-stu-id="c0690-129">UserName</span></span> | <span data-ttu-id="c0690-130">Specifica il nome utente per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="c0690-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="c0690-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="c0690-131">Verbosity</span></span> | <span data-ttu-id="c0690-132">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="c0690-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="c0690-133">Assicurarsi di aggiungere la password delle origini nello stesso contesto utente in cui NuGet. exe verrà usato in un secondo momento per accedere all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c0690-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="c0690-134">La password verrà archiviata crittografata nel file di configurazione e potrà essere decrittografata solo nello stesso contesto utente in cui è stata crittografata.</span><span class="sxs-lookup"><span data-stu-id="c0690-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="c0690-135">Quindi, ad esempio, quando si usa un server di compilazione per ripristinare i pacchetti NuGet, la password deve essere crittografata con lo stesso utente di Windows in cui verrà eseguita l'attività del server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="c0690-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="c0690-136">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c0690-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c0690-137">Esempi</span><span class="sxs-lookup"><span data-stu-id="c0690-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
