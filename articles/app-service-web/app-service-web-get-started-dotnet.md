---
title: Skapa en ASP.NET-webbapp i Azure | Microsoft Docs
description: "Distribuera standard-ASP.NET-webbappen och lär dig att köra webbappar i Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.translationtype: HT
ms.sourcegitcommit: 8021f8641ff3f009104082093143ec8eb087279e
ms.openlocfilehash: b5a7f3ebe5e95d3838e71b7b17b91e85da0d51a2
ms.contentlocale: sv-se
ms.lasthandoff: 07/21/2017

---
# <a name="create-an-aspnet-web-app-in-azure"></a>Skapa en ASP.NET-webbapp i Azure

Med [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) får du en mycket skalbar och automatiskt uppdaterad webbvärdtjänst.  Den här snabbstarten visar hur du distribuerar din första ASP.NET-webbapp till Azure Web Apps. När du är klar har du en resursgrupp som består av en App Service-plan och en Azure-webbapp med en distribuerad webbapp.

![ASP.NET-webbapp i Azure App Service](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="prerequisites"></a>Krav

För att slutföra den här självstudien behöver du:

* Installera [Visual Studio 2017](https://www.visualstudio.com/downloads/) med följande arbetsbelastningar:
    - **ASP.NET och webbutveckling**
    - **Azure Development**

    ![ASP.NET och webbutveckling och Azure Development (under webb och moln)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>Skapa en ASP.NET-webbapp

Skapa ett nytt projekt i Visual Studio genom att välja **Arkiv > Nytt > Projekt**. 

I dialogrutan **Nytt projekt** väljer du **Visual C# > Webb > ASP.NET-webbtillämpningsprogram (.NET Framework)**.

Ge programmet namnet _myFirstAzureWebApp_ och välj **OK**.
   
![Dialogrutan Nytt projekt](./media/app-service-web-get-started-dotnet/new-project.png)

Du kan distribuera alla typer av ASP.NET-webbappar till Azure. I den här snabbstarten väljer du **MVC**-mallen och ser till att autentiseringen är inställd på **Ingen autentisering**.
      
Välj **OK**.

![Dialogrutan Nytt ASP.NET-projekt](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

På menyn väljer du **Felsöka > Starta utan felsökning** för att köra webbappen lokalt.

![Kör appen lokalt](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-to-azure"></a>Publicera till Azure

Högerklicka på projektet **myFirstAzureWebApp** i **Solution Explorer** och välj **Publicera**.

![Publicera från Solution Explorer](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

Se till att **Microsoft Azure App Service** är markerat och välj **Publicera**.

![Publicera från projektöversiktssidan](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

Då öppnas dialogrutan **Skapa App Service** där du får hjälp med att skapa alla Azure-resurser du behöver för att köra ASP.NET-webbappen i Azure.

## <a name="sign-in-to-azure"></a>Logga in på Azure

I dialogrutan **Skapa App Service** väljer du **Lägg till ett konto** och loggar sedan in med din Azure-prenumeration. Välj det konto som innehåller den önskade prenumerationen i listrutan om du redan är inloggad.

> [!NOTE]
> Välj inte **Skapa** ännu om du redan är inloggad.
>
>
   
![Logga in på Azure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>Skapa en resursgrupp

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

Välj **Ny** bredvid **Resursgrupp**.

Ge resursgruppen namnet **myResourceGroup** och välj **OK**.

## <a name="create-an-app-service-plan"></a>Skapa en App Service-plan

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Välj **Ny** bredvid **App Service-plan**. 

I dialogrutan **Configure App Service Plan** (Konfigurera App Service-plan) använder du inställningarna i tabellen som följer skärmbilden.

![Skapa apptjänstplan](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| Inställning | Föreslaget värde | Beskrivning |
|-|-|-|
|App Service-plan| myAppServicePlan | Namnet på App Service-planen. |
| Plats | Västra Europa | Datacenter som är värd för webbappen. |
| Storlek | Kostnadsfri | [Prisnivån](https://azure.microsoft.com/pricing/details/app-service/) avgör tillgängliga värdfunktioner. |

Välj **OK**.

## <a name="create-and-publish-the-web-app"></a>Skapa och publicera webbappen

I **Webbprogramnamnet** skriver du ett unikt appnamn (giltiga tecken är `a-z`, `0-9` och `-`) eller acceptera det automatiskt genererade unika namnet. Webbadressen till webbappen är `http://<app_name>.azurewebsites.net`, där `<app_name>` är webbappens namn.

Välj **Skapa** för att börja skapa Azure-resurser.

![Ange webbappnamn](./media/app-service-web-get-started-dotnet/web-app-name.png)

När guiden slutförs publiceras ASP.NET-webbappen till Azure och sedan öppnas appen i standardwebbläsaren.

![Publicerad ASP.NET-webbapp i Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

Webbprogramnamnet som anges i steget [skapa och publicera](#create-and-publish-the-web-app) används som URL-prefixet i formatet `http://<app_name>.azurewebsites.net`.

Grattis, din ASP.NET-webbapp körs live i Azure App Service.

## <a name="update-the-app-and-redeploy"></a>Uppdatera och distribuera om appen

Öppna _Views\Home\Index.cshtml_ från **Solution Explorer**.

Leta reda på HTML-taggen `<div class="jumbotron">` längst upp på sidan och ersätt hela elementet med följande kod:

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

Högerklicka på projektet **myFirstAzureWebApp** i **Solution Explorer** och välj **Publicera** för att distribuera om appen till Azure.

Välj **Publicera** på publiceringssidan.

När publiceringen är klar startar Visual Studio en webbläsare till webbappens URL.

![Uppdaterad ASP.NET-webbapp i Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-the-azure-web-app"></a>Hantera Azure-webbappen

Gå till <a href="https://portal.azure.com" target="_blank">Azure Portal</a> för att hantera webbappen.

Klicka på **Apptjänster** på menyn till vänster och välj sedan namnet på din Azure-webbapp.

![Navigera till webbappen på Azure Portal](./media/app-service-web-get-started-dotnet/access-portal.png)

Nu visas sidan Översikt för din webbapp. Här kan du utföra grundläggande hanteringsåtgärder som att bläddra, stoppa, starta, starta om och ta bort. 

![App Service-blad på Azure Portal](./media/app-service-web-get-started-dotnet/web-app-blade.png)

Menyn till vänster innehåller olika sidor för att konfigurera appen. 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [ASP.NET med SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md)

