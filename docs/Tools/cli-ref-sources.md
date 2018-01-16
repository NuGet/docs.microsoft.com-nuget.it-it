---
title: NuGet CLI origini comando | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: Riferimento per il nuget.exe origini comando
keywords: NuGet origini di riferimento, le origini di comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="434c5-104">comando origini (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="434c5-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="434c5-105">**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="434c5-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="434c5-106">Gestisce l'elenco delle origini nel `%AppData%\NuGet\NuGet.Config` o file di configurazione specificato.</span><span class="sxs-lookup"><span data-stu-id="434c5-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="434c5-107">Si noti che è l'URL di origine per nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="434c5-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="434c5-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="434c5-108">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="434c5-109">dove `<operation>` è uno dei *elenco, aggiungere, rimuovere, attivare, disattivare* o *aggiornamento*, `<name>` è il nome dell'origine, e `<source>` è l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="434c5-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="434c5-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="434c5-110">Options</span></span>

| <span data-ttu-id="434c5-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="434c5-111">Option</span></span> | <span data-ttu-id="434c5-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="434c5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="434c5-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="434c5-113">ConfigFile</span></span> | <span data-ttu-id="434c5-114">*(2.5 +)*  Questo file di configurazione da applicare.</span><span class="sxs-lookup"><span data-stu-id="434c5-114">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="434c5-115">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="434c5-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="434c5-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="434c5-116">ForceEnglishOutput</span></span> | <span data-ttu-id="434c5-117">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="434c5-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="434c5-118">Formato</span><span class="sxs-lookup"><span data-stu-id="434c5-118">Format</span></span> | <span data-ttu-id="434c5-119">Si applica al `list` azione e può essere `Detailed` (impostazione predefinita) o `Short`.</span><span class="sxs-lookup"><span data-stu-id="434c5-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="434c5-120">?</span><span class="sxs-lookup"><span data-stu-id="434c5-120">Help</span></span> | <span data-ttu-id="434c5-121">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="434c5-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="434c5-122">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="434c5-122">NonInteractive</span></span> | <span data-ttu-id="434c5-123">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="434c5-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="434c5-124">Password</span><span class="sxs-lookup"><span data-stu-id="434c5-124">Password</span></span> | <span data-ttu-id="434c5-125">Specifica la password per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="434c5-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="434c5-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="434c5-126">StorePasswordInClearText</span></span> | <span data-ttu-id="434c5-127">Indica di archiviare la password in testo non crittografato anziché il comportamento predefinito di archiviazione di un formato crittografato.</span><span class="sxs-lookup"><span data-stu-id="434c5-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="434c5-128">UserName</span><span class="sxs-lookup"><span data-stu-id="434c5-128">UserName</span></span> | <span data-ttu-id="434c5-129">Specifica il nome utente per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="434c5-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="434c5-130">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="434c5-130">Verbosity</span></span> | <span data-ttu-id="434c5-131">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="434c5-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="434c5-132">Assicurarsi di aggiungere password delle origini nel contesto dell'utente stesso come il nuget.exe viene successivamente utilizzato per accedere all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="434c5-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="434c5-133">La password verrà archiviata crittografati nel file di configurazione e può essere decrittografata solo nello stesso contesto utente come è stato crittografato.</span><span class="sxs-lookup"><span data-stu-id="434c5-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="434c5-134">Ad esempio quando si utilizza un server di compilazione per il ripristino dei pacchetti NuGet che la password deve essere crittografata con lo stesso utente di Windows in cui verrà eseguita l'attività del server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="434c5-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="434c5-135">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="434c5-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="434c5-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="434c5-136">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
