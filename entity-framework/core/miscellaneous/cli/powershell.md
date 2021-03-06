---
title: "Paket-Manager-Konsole (Visual Studio) – EF Core"
author: bricelam
ms.author: bricelam
ms.date: 11/6/2017
ms.technology: entity-framework-core
ms.openlocfilehash: b4ecb27edf94e7b9ad6c7fe65a891dcbf1593309
ms.sourcegitcommit: 5e2d97e731f975cf3405ff3deab2a3c75ad1b969
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
<a name="ef-core-package-manager-console-tools"></a>EF-Core-Paket-Manager-Konsole Tools
=====================================
Die Tools EF Core Paket-Manager-Konsole (PMC) ausführen, in Visual Studio mithilfe von NuGet [Package Manager Console][2].
Diese Tools funktionieren mit .NET Framework und .NET Core-Projekten.

> [!TIP]
> Verwenden Sie nicht Visual Studio? Die [EF Core-Befehlszeilentools] [ 1] über Plattformen hinweg und in einer Eingabeaufforderung ausgeführt werden.

<a name="installing-the-tools"></a>Installieren der Tools
--------------------
Installieren von EF-Core-Paket-Manager-Konsole Tools durch das Microsoft.EntityFrameworkCore.Tools NuGet-Paket installieren.
Sie können es installieren, indem Sie in den folgenden Befehl ausführen [Package Manager Console][2].

``` powershell
Install-Package Microsoft.EntityFrameworkCore.Tools
```

Wenn alles ordnungsgemäß funktioniert, sollten Sie diesen Befehl ausführen können:

``` powershell
Get-Help about_EntityFrameworkCore
```
> [!TIP]
> Wenn das Startprojekt .NET Standard verwendet [Cross-Zielframework eine unterstützte] [ 3] vor der Verwendung der Tools.

> [!IMPORTANT]
> Bei Verwendung von **universelle Windows** oder **Xamarin**, Verschieben von EF Code auf eine .NET Standard-Klassenbibliothek und [Cross-Zielframework eine unterstützte] [ 3] vor der Verwendung der Tools. Geben Sie die Klassenbibliothek als Startprojekt fest.

<a name="using-the-tools"></a>Mithilfe der tools
---------------
Bei jedem eines Befehls aufrufen umfasst zwei Projekte:

Das Zielprojekt ist keine Dateien hinzugefügt werden (oder in einigen Fällen entfernt). Das Zielprojekt wird standardmäßig auf die **Standardprojekt** in Paket-Manager-Konsole ausgewählt, aber kann auch mit angegeben werden-Projektparameter.

Das Startprojekt wird von den Tools emuliert wird, wenn der Code des Projekts ausführen. Wird standardmäßig eine **als Startprojekt festlegen** im Projektmappen-Explorer. Sie können auch mit dem StartupProject - Parameter angegeben werden.

Allgemeine Parameter:

|                           |                             |
| ------------------------- | --------------------------- |
| -Kontext \<Zeichenfolge >        | Die DbContext verwenden.       |
| -Projekt \<Zeichenfolge >        | Das Projekt verwendet werden soll.         |
| -StartupProject \<Zeichenfolge > | Das Startup-Projekt verwenden. |
| -Verbose                  | Zeigen Sie eine ausführlichen Ausgabe.        |

Um Hilfeinformationen zu einem Befehl anzuzeigen, verwenden Sie PowerShell `Get-Help` Befehl.

> [!TIP]
> Der Kontext, Projekt- und StartupProject-Parameter unterstützen Tab-Taste.

> [!TIP]
> Legen Sie **Env:ASPNETCORE_ENVIRONMENT** vor dem Ausführen, um anzugeben, die ASP.NET Core-Umgebung.

<a name="commands"></a>Befehle
--------

### <a name="add-migration"></a>Hinzufügen-Migration

Fügt eine neue Migration.

Parameter:

|                                    |                                                                                 |
| ---------------------------------- | ------------------------------------------------------------------------------- |
| ***-Namen*** \<Zeichenfolge >              | Der Name der Migration.                                                      |
| <nobr>-OutputDir \<Zeichenfolge ></nobr>  | Das Verzeichnis (und Sub-Namespace) zu verwenden. Pfade sind relativ zum Projektverzeichnis an. Der Standardwert ist "Migration". |

> [!NOTE]
> Parameter in **fett** sind erforderlich, und diejenigen *Kursiv* sind mit Feldern fester Breite.

### <a name="drop-database"></a>Drop-Datenbank

Löscht die Datenbank.

Parameter:

|          |                                                          |
| -------- | -------------------------------------------------------- |
| "-WhatIf"  | Anzeigen, welche Datenbank verworfen werden, jedoch nicht, legen Sie sie. |

### <a name="get-dbcontext"></a>Get-DbContext

Ruft Informationen zu einem DbContext-Typ ab.

### <a name="remove-migration"></a>Remove-Migration

Entfernt die letzte Migration.

Parameter:

|        |                                                                       |
| ------ | --------------------------------------------------------------------- |
| -Force | Überprüfen Sie nicht, um festzustellen, ob die Migration der Datenbank angewendet wurde. |

### <a name="scaffold-dbcontext"></a>Gerüst DbContext

Gerüste ein ' DbContext ' und Entität Typen für eine Datenbank.

Parameter:

|                                          |                                                                           |
| ---------------------------------------- | ------------------------------------------------------------------------- |
| <nobr>***-Verbindung*** \<Zeichenfolge ></nobr> | Die Verbindungszeichenfolge zur Datenbank.                                    |
| ***-Anbieter*** \<Zeichenfolge >                | Die zu verwendenden Anbieter an. (D. h. Microsoft.EntityFrameworkCore.SqlServer)       |
| -OutputDir \<Zeichenfolge >                     | Das Verzeichnis in den Dateien versetzt. Pfade sind relativ zum Projektverzeichnis an. |
| -Kontext \<Zeichenfolge >                       | Der Name von ' DbContext ' zu generieren.                                    |
| -Schemas \<String [] >                     | Die Schemas der Tabellen zur Generierung von Entitätstypen für.                       |
| -Tabellen \<String [] >                      | Die Tabellen für Entitätstypen generieren.                                  |
| DataAnnotations-                         | Verwenden Sie Attribute, um das Modell (sofern möglich) konfigurieren. Wenn nicht angegeben, wird nur die fluent-API verwendet. |
| -UseDatabaseNames                        | Verwenden Sie die Tabellen- und Spaltennamen direkt aus der Datenbank.                    |
| -Force                                   | Überschreiben Sie vorhandene Dateien.                                                 |

### <a name="script-migration"></a>Skript-Migration

Generiert ein SQL-Skript von Migrationen.

Parameter:

|                   |                                                                    |
| ----------------- | ------------------------------------------------------------------ |
| *-From* \<Zeichenfolge > | Der Start Migration. Der Standardwert ist 0 (die ursprüngliche Datenbank).      |
| *-Zu* \<Zeichenfolge >   | Der Endwert Migration. Standardmäßig bis zum letzten Migration.              |
| -Idempotent       | Generiert ein Skript, das für eine Datenbank bei jeder Migration verwendet werden kann. |
| -Output \<Zeichenfolge > | Die Datei, schreibt das Ergebnis.                                   |

> [!TIP]
> To, From, und Output-Parameter unterstützen Tab-Taste.

### <a name="update-database"></a>Datenbank aktualisieren

|                                     |                                                                                |
| ----------------------------------- | ------------------------------------------------------------------------------ |
| <nobr>*-Migration* \<Zeichenfolge ></nobr> | Der zielmigration. Bei "0" werden bei allen Migrationen rückgängig gemacht werden. Standardmäßig bis zum letzten Migration. |

> [!TIP]
> Der Parameter für die Migration unterstützt Tab-Taste.


  [1]: dotnet.md
  [2]: https://docs.microsoft.com/nuget/tools/package-manager-console
  [3]: index.md#frameworks
