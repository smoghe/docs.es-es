---
title: "Creación de una solución completa de .NET Core en Windows con Visual Studio 2017 | Microsoft Docs"
description: "Creación de una solución completa de .NET Core en Windows con Visual Studio 2017"
keywords: .NET, .NET Core
author: bleroy
ms.author: mairaw
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: ba7e082c-a7c8-431e-a342-f67734b660f6
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: b8505f88b324fcdf3a51d75c455ec5869e058774
ms.lasthandoff: 03/07/2017

---

# <a name="building-a-complete-net-core-solution-on-windows-using-visual-studio-2017"></a>Creación de una solución completa de .NET Core en Windows con Visual Studio 2017

Visual Studio 2017 proporciona un entorno de desarrollo completo para las aplicaciones .NET Core. Los procedimientos de este documento describen los pasos necesarios para compilar una solución típica de .NET Core que incluye bibliotecas reutilizables, pruebas y el uso de bibliotecas de terceros. 

## <a name="prerequisites"></a>Requisitos previos

Siga las instrucciones de [nuestra página de requisitos previos](../windows-prerequisites.md) para actualizar su entorno.

## <a name="a-solution-using-only-net-core-projects"></a>Una solución solo con proyectos de .NET Core

### <a name="writing-the-library"></a>Escritura de la biblioteca

1. En Visual Studio, elija **Archivo**, **Nuevo**, **Proyecto**. En el cuadro de diálogo **Nuevo proyecto**, expanda el nodo **Visual C#**, elija el nodo **.NET Core** y luego elija **Biblioteca de clases (.NET Standard)**. 

2. Llame "Library" al proyecto y "Golden" a la solución. Deje desactivada la casilla **Crear directorio para la solución**. Haga clic en **Aceptar**.

3. En el Explorador de soluciones, abra el menú contextual del nodo **Dependencias** y luego elija **Administrar paquetes NuGet**.

4. Elija "nuget.org" como **origen del paquete** y elija la pestaña **Examinar**. Busque **Newtonsoft.Json**. Haga clic en **Instalar** y acepte el acuerdo de licencia. El paquete debe aparecer ahora en **Dependencias/NuGet** y restaurarse automáticamente.

5. Cambie el nombre del archivo `Class1.cs` a `Thing.cs`. Acepte el cambio de nombre de la clase. Agregue un método: `public int Get(int number) => Newtonsoft.Json.JsonConvert.DeserializeObject<int>($"{number}");`

7. En el menú **Compilar** , elija **Compilar solución**.

   La solución se debe compilar sin errores.

### <a name="writing-the-test-project"></a>Escritura del proyecto de prueba

1. En el Explorador de soluciones, abra el menú contextual del nodo **Solución** y elija **Agregar**, **Nuevo proyecto**. En el cuadro de diálogo **Nuevo proyecto**, en **Visual C# / .NET Core**, elija **Proyecto de prueba unitaria (.NET Core)**. Asígnele el nombre "TestLibrary" y haga clic en Aceptar. 

2. En el proyecto **TestLibrary**, abra el menú contextual del nodo **Dependencias** y elija **Agregar referencia**. Haga clic en **Proyectos**, marque el proyecto de biblioteca y haga clic en Aceptar. Se agrega una referencia a la biblioteca desde el proyecto de prueba.

3. Cambie el nombre del archivo `UnitTest1.cs` por `LibraryTests.cs` y acepte el cambio de nombre de la clase. Agregue `using Library;` al principio del archivo y sustituya el método `TestMethod1` por el siguiente código:
    ```csharp
    [TestMethod]
    public void ThingGetsObjectValFromNumber()
    {
        Assert.AreEqual(42, new Thing().Get(42));
    }
    ```

   Ahora debería poder compilar la solución. 
   
4. En el menú **Prueba**, elija **Windows**, **Explorador de pruebas** para introducir la ventana del explorador de pruebas en su área de trabajo. Al cabo de unos segundos, la prueba `ThingGetsObjectValFromNumber` debe aparecer en el Explorador de pruebas. Elija **Ejecutar todas**.
   
   La prueba debe realizarse correctamente.

### <a name="writing-the-console-app"></a>Escritura de la aplicación de consola

1. En el Explorador de soluciones, abra el menú contextual de la solución y agregue un nuevo proyecto **Aplicación de consola (.NET Core)**. Asígnele el nombre "App".

2. En el proyecto **App**, abra el menú contextual del nodo **Dependencias** y elija **Agregar**, **Referencia**. 

3. En el cuadro de diálogo **Administrador de referencias**, active **Biblioteca** bajo el nodo **Proyectos**, **Solución** y, después, haga clic en **Aceptar**.

6. Abra el menú contextual por el nodo **App** y elija **Establecer como proyecto de inicio**. Esto garantiza que al presionar F5 o CTRL+F5 se iniciará la aplicación de consola.

7. Abra el archivo `Program.cs`, agregue una directiva `using Library;` en la parte superior del archivo y, después, agregue `Console.WriteLine($"The answer is {new Thing().Get(42)}.");` al método `Main`.

8. Establezca un punto de interrupción después de la línea que acaba de agregar.

9. Presione F5 para ejecutar la aplicación.

   La aplicación se debe compilar sin errores y debe alcanzar el punto de interrupción. También debe ser capaz de comprobar que aplicación produce la salida "La respuesta es 42".

