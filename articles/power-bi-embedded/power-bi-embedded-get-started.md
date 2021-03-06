---
title: "Komma igång med Microsoft Power BI Embedded"
description: "Power BI Embedded lägger till interaktiva Power BI-rapporter i dina Business Intelligence-appar"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
translationtype: Human Translation
ms.sourcegitcommit: c1cd1450d5921cf51f720017b746ff9498e85537
ms.openlocfilehash: 4afa8d2c7f8ec1942521ba5fa131967dfd581c91
ms.lasthandoff: 03/14/2017

---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Komma igång med Microsoft Power BI Embedded

**Power BI Embedded** är en Azure-tjänst som gör det möjligt för apputvecklare att lägga till interaktiva Power BI-rapporter till sina egna appar. **Power BI Embedded** fungerar med befintliga program utan att behöva designa om eller ändra hur användarna loggar in.

Resurser för **Microsoft Power BI Embedded** distribueras via [Azure ARM-API:er](https://msdn.microsoft.com/library/mt712306.aspx). I det här fallet är den resurs som du etablerar en **Power BI-arbetsytesamling**.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>Skapa en arbetsytesamling

En **arbetsytesamling** är en Azure-resurs på högsta nivå och en behållare för det innehåll som kommer att vara inbäddat i din app. En **arbetsytesamling** kan skapas på två sätt:

* Använda Azure Portal manuellt
* Genom programmering med Azure Resource Manager-API:er

Låt oss gå igenom stegen för att skapa en **arbetsytesamling** i Azure Portal.

1. Öppna och logga in på **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).
2. Klicka på **+ Ny** på den övre panelen.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. Under **Data + analys** klickar du på **Power BI Embedded**.
4. Ange den information som krävs på **bladet Arbetsytesamling**. Mer information om **priser** finns i [Priser för Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. Klicka på **Skapa**.

Det tar en liten stund att etablera **arbetsytesamlingen**. När den har slutförts förs du till **arbetsytesamlingsbladet**.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

Bladet **Skapa** innehåller den information du behöver för att anropa de API:er som skapar arbetsytor och distribuera innehåll till dem.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Visa API-åtkomstnycklar för Power BI

En av de viktigaste informationsdelarna som krävs för att anropa Power BI REST-API:er är **åtkomstnycklarna**. Dessa används för att generera de **apptoken** som används för att autentisera dina API-begäranden. För att visa dina **åtkomstnycklar**, klickar du på **Åtkomstnycklar** på bladet **Inställningar**. Mer information om **apptoken**, finns i [Autentisering och auktorisering med Power BI Embedded](power-bi-embedded-app-token-flow.md).

   ![](media/power-bi-embedded-get-started/access-keys.png)

Du ser att du har två nycklar.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

Kopiera nycklarna och lagra dem på ett säkert sätt i din app. Det är mycket viktigt att du hanterar de här nycklarna lika försiktigt som ett lösenord, eftersom de ger åtkomst till allt innehåll i din **arbetsytesamling**.

Det finns två nycklar listade men bara en i taget behövs. Den andra nyckeln tillhandahålls så att du regelbundet kan återskapa nycklar utan att avbryta åtkomsten till tjänsten.

Nu när du har en Power BI-instans för din app och **åtkomstnycklar** kan du importera en rapport till din egen app. Innan du lär dig hur du importerar en rapport får du i nästa avsnitt lära dig hur du skapar Power BI-datauppsättningar och -rapporter som ska bäddas in i en app.

## <a name="working-with-workspaces"></a>Arbeta med arbetsytor

När du har skapat arbetsytesamlingen behöver du skapa en arbetsyta för dina rapporter och datauppsättningar. Du behöver använda [REST-API-anropet Post Workspace](https://msdn.microsoft.com/library/azure/mt711503.aspx) för att skapa en arbetsyta.

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app-using-power-bi-desktop"></a>Skapa Power BI-datauppsättningar och -rapporter som ska bäddas in i en app med hjälp av Power BI Desktop

Nu när du har skapat en Power BI-instans för din app och har **åtkomstnycklar** måste du skapa de Power BI-datauppsättningar och -rapporter som du vill bädda in. Datauppsättningar och rapporter kan skapas med hjälp av **Power BI Desktop**. Du kan hämta [Power BI Desktop kostnadsfritt](https://go.microsoft.com/fwlink/?LinkId=521662). Om du vill komma igång snabbt kan du också hämta [exempel på detaljhandelsanalys PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).

> [!NOTE]
> Mer information om hur du använder **Power BI Desktop** finns i [Komma igång med Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).

Med **Power BI Desktop** ansluter du till din datakälla genom att importera en kopia av data till **Power BI Desktop** eller ansluta direkt till datakällan med **DirectQuery**.

Detta är skillnaderna mellan **Importera** och **DirectQuery**.

| Importera | DirectQuery |
| --- | --- |
| Tabeller, kolumner *och data* importeras eller kopieras till **Power BI Desktop**. När du arbetar med visualiseringar ställer **Power BI Desktop** frågor till en kopia av data. Om du vill se ändringar som gjorts i underliggande data måste du uppdatera eller importera en fullständig, aktuell datauppsättning igen. |Endast *tabeller och kolumner* importeras eller kopieras till **Power BI Desktop**. När du arbetar med visualiseringar ställer **Power BI Desktop** frågor till den underliggande datakällan, vilket innebär att du alltid visar aktuella data. |

Mer information om hur du ansluter till en datakälla finns i [Ansluta till en datakälla](power-bi-embedded-connect-datasource.md).

När du har sparat ditt arbete i **Power BI Desktop** skapas en PBIX-fil. Den här filen innehåller rapporten. Om du importerar data innehåller PBIX dessutom den fullständiga datauppsättningen. Om du använder **DirectQuery** innehåller PBIX bara ett datauppsättningsschema. Du distribuerar PBIX genom programmering till din arbetsyta med hjälp av [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).

> [!NOTE]
> **Power BI Embedded** har ytterligare API:er för att ändra den server och den databas som din datauppsättning pekar på och ange autentiseringsuppgifter för tjänstekontot som datauppsättningen kommer att använda för att ansluta till databasen. Se [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) och [Datakälla för korrigeringsgateway](https://msdn.microsoft.com/library/mt711498.aspx).

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>Skapa Power BI-datauppsättningar och -rapporter med hjälp av API:er

### <a name="datsets"></a>Datauppsättningar

Du kan skapa datauppsättningar i Power BI Embedded med hjälp av REST API. Du kan sedan skicka data till datauppsättningen. På så sätt kan du arbeta med data utan att du behöver Power BI Desktop. Mer information finns i [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Lägga upp datauppsättningar).

### <a name="reports"></a>Rapporter

Du kan skapa en rapport från en datamängd direkt i programmet med hjälp av JavaScript API. Mer information finns i [Skapa en ny rapport från en datauppsättning i Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).

## <a name="see-also"></a>Se även

[Komma igång med exemplet](power-bi-embedded-get-started-sample.md)  
[Autentisering och auktorisering i Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Bädda in en rapport](power-bi-embedded-embed-report.md)  
[Skapa en ny rapport från en datauppsättning i Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Spara rapporter](power-bi-embedded-save-reports.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Inbäddat exempel med JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Fler frågor? [Försök med Power BI Community](http://community.powerbi.com/)


