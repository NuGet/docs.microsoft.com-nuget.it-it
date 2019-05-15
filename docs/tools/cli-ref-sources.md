---
title: Comando le origini NuGet CLI
description: Informazioni di riferimento per il nuget.exe origini di comandi
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610627"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="1f8ed-103">Comando sources (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="1f8ed-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="1f8ed-104">**Si applica a:** utilizzo di un pacchetto, la pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="1f8ed-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1f8ed-105">Gestisce l'elenco delle origini che si trova nel file di configurazione di ambito utente o un file di configurazione specificato.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="1f8ed-106">Il file di configurazione di ambito utente si trova in `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1f8ed-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="1f8ed-107">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="1f8ed-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="1f8ed-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="1f8ed-109">in cui `<operation>` è uno dei *elencare, aggiungere, rimuovere, abilitare, disabilitare* oppure *Update*, `<name>` è il nome dell'origine, e `<source>` è l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="1f8ed-110">È possibile utilizzare una sola origine alla volta.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="1f8ed-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="1f8ed-111">Options</span></span>

| <span data-ttu-id="1f8ed-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="1f8ed-112">Option</span></span> | <span data-ttu-id="1f8ed-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1f8ed-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1f8ed-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1f8ed-114">ConfigFile</span></span> | <span data-ttu-id="1f8ed-115">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1f8ed-116">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1f8ed-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1f8ed-117">ForceEnglishOutput</span></span> | <span data-ttu-id="1f8ed-118">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1f8ed-119">Formato</span><span class="sxs-lookup"><span data-stu-id="1f8ed-119">Format</span></span> | <span data-ttu-id="1f8ed-120">Viene applicata il `list` azione e può essere `Detailed` (predefinito) o `Short`.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="1f8ed-121">?</span><span class="sxs-lookup"><span data-stu-id="1f8ed-121">Help</span></span> | <span data-ttu-id="1f8ed-122">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="1f8ed-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1f8ed-123">NonInteractive</span></span> | <span data-ttu-id="1f8ed-124">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1f8ed-125">Password</span><span class="sxs-lookup"><span data-stu-id="1f8ed-125">Password</span></span> | <span data-ttu-id="1f8ed-126">Specifica la password per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="1f8ed-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="1f8ed-127">StorePasswordInClearText</span></span> | <span data-ttu-id="1f8ed-128">Indica di archiviare la password in testo non crittografato anziché il comportamento predefinito di un modulo crittografato di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="1f8ed-129">UserName</span><span class="sxs-lookup"><span data-stu-id="1f8ed-129">UserName</span></span> | <span data-ttu-id="1f8ed-130">Specifica il nome utente per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="1f8ed-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1f8ed-131">Verbosity</span></span> | <span data-ttu-id="1f8ed-132">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="1f8ed-133">Assicurarsi di aggiungere password delle origini nello stesso contesto utente come il nuget.exe viene successivamente utilizzato per accedere all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="1f8ed-134">La password verrà archiviata crittografati nel file di configurazione e può essere decrittografata solo nello stesso contesto utente perché è stato crittografato.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="1f8ed-135">Quindi, ad esempio quando si usa un server di compilazione per ripristinare i pacchetti NuGet che la password deve essere crittografata con lo stesso utente di Windows con cui verrà eseguita l'attività del server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="1f8ed-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="1f8ed-136">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1f8ed-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1f8ed-137">Esempi</span><span class="sxs-lookup"><span data-stu-id="1f8ed-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
