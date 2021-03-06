---
title: "Fråga Azure SQL Database med Java | Microsoft Docs"
description: "Det här avsnittet visar hur du använder Java för att skapa ett program som ansluter till en Azure SQL Database och frågar den med hjälp av Transact-SQL-uttryck."
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.translationtype: HT
ms.sourcegitcommit: 54454e98a2c37736407bdac953fdfe74e9e24d37
ms.openlocfilehash: f07f49e64f107ec063bfb755dbb89644f3d00576
ms.contentlocale: sv-se
ms.lasthandoff: 07/13/2017

---
# <a name="use-java-to-query-an-azure-sql-database"></a>Fråga Azure SQL Database med Java

Den här snabbstarten visar hur du använder [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) för att ansluta till en Azure SQL-databas och sedan använda Transact-SQL-uttryck för att fråga data.

## <a name="prerequisites"></a>Krav

För att kunna slutföra den här snabbstartskursen behöver du följande:

- En Azure SQL-databas. Den här snabbstarten använder resurser som har skapats i någon av dessa snabbstarter: 

   - [Skapa DB – Portal](sql-database-get-started-portal.md)
   - [Skapa DB – CLI](sql-database-get-started-cli.md)
   - [Skapa DB – PowerShell](sql-database-get-started-powershell.md)

- En [brandväggsregel på servernivå](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) för den offentliga IP-adressen för den dator du använder för den här snabbstartskursen.

- Du har installerat Java och relaterad programvara för ditt operativsystem.

    - **MacOS**: Installera Homebrew och Java och installera sedan Maven. Se [Steg 1.2 och 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).
    - **Ubuntu**: Installera Java Development Kit och Maven. Se [Steg 1.2, 1.3 och 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).
    - **Windows**: Installera Java Development Kit och Maven. Se [Steg 1.2 och 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).    

## <a name="sql-server-connection-information"></a>Anslutningsinformation för en SQL-server

Skaffa den anslutningsinformation du behöver för att ansluta till Azure SQL Database. Du behöver det fullständiga servernamnet, databasnamnet och inloggningsinformationen i nästa procedurer.

1. Logga in på [Azure-portalen](https://portal.azure.com/).
2. Välj **SQL-databaser** på den vänstra menyn och klicka på databasen på sidan **SQL-databaser**. 
3. Granska serverns fullständiga namn på sidan **Översikt** för databasen enligt vad som visas på bilden nedan. Du kan hovra över servernamnet för att se alternativet **Klicka för att kopiera**.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Om du glömmer inloggningsinformationen för din server öppnar du serversidan i SQL Database. Där ser du administratörsnamnet för servern.  Du kan återställa lösenordet om det behövs.     

## <a name="create-maven-project-and-dependencies"></a>**Skapa Maven-projekt och beroenden**
1. Skapa ett nytt Maven-projekt som du namnger **sqltest** från terminalen. 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. Ange **Y** när du tillfrågas.
3. Gå till katalogen för **sqltest** och öppna ***pom.xml*** med valfri textredigerare.  Lägg till **Microsoft JDBC-drivrutinen för SQL Server** i projektets beroenden med följande kod:

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. Lägg även till följande egenskaper i projektet i filen ***pom.xml***.  Om du inte har ett avsnitt för egenskaper kan du lägga till efter beroendena.

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. Spara och stäng ***pom.xml***.

## <a name="insert-code-to-query-sql-database"></a>Infoga kod för att fråga SQL Database

1. Du bör redan ha en fil med namnet ***App.java*** i ditt Maven-projekt som finns i: ...\sqltest\src\main\java\com\sqlsamples\App.Java

2. Öppna filen och ersätt innehållet med följande kod och lägg till lämpliga värden för server, databas, användare och lösenord.

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect to database
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                   }
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-the-code"></a>Kör koden

1. Kör följande kommandon i kommandotolken:

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. Kontrollera att de 20 översta raderna returneras och stäng sedan programfönstret.


## <a name="next-steps"></a>Nästa steg
- [Utforma din första Azure SQL Database](sql-database-design-first-database.md)
- [Microsoft JDBC-drivrutin för SQL Server](https://github.com/microsoft/mssql-jdbc)
- [Rapportera problem/ställ frågor](https://github.com/microsoft/mssql-jdbc/issues)


