---
title: Comando dotnet-restore | Microsoft Docs
description: "Aprenda a restaurar dependencias y herramientas específicas del proyecto con el comando dotnet restore."
keywords: dotnet-restore, CLI, comando de la CLI, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fd7a5769-afbe-4838-bbaf-3ae0cfcbb914
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: a55cd932045a59f08146dff367a87eb6fe61f6e5
ms.lasthandoff: 03/07/2017

---

#<a name="dotnet-restore"></a>dotnet-restore

## <a name="name"></a>Name

`dotnet-restore`: restaura las dependencias y las herramientas de un proyecto.

## <a name="synopsis"></a>Sinopsis

```
dotnet restore [root] [-s|--source] [-r|--runtime] [--packages] [--disable-parallel] [--configfile] [--no-cache] [--ignore-failed-sources] [--no-dependencies] [-v|--verbosity]
dotnet restore [-h|--help]
```

## <a name="description"></a>Descripción

El comando `dotnet restore` usa NuGet para restaurar las dependencias, así como las herramientas específicas del proyecto que se especifican en el archivo project.json. De forma predeterminada, la restauración de dependencias y herramientas se realizan en paralelo.

Para restaurar las dependencias, NuGet necesita las fuentes donde se encuentran los paquetes. Normalmente se proporcionan fuentes mediante el archivo de configuración NuGet.config; hay uno predeterminado cuando se instalan las herramientas de la CLI. Puede especificar más fuentes creando su propio archivo NuGet.config en el directorio del proyecto. También se pueden especificar fuentes por invocación en el símbolo del sistema. 

Para las dependencias, puede especificar dónde se colocan los paquetes restaurados durante la operación de restauración mediante el argumento `--packages`. Si no se especifica, se usa la caché del paquete de NuGet predeterminada. Se encuentra en el directorio `.nuget/packages` en el directorio del directorio principal del usuario en todos los sistemas operativos (por ejemplo, */home/user1* en Linux o *C:\Users\user1* en Windows).

Para herramientas específicas del proyecto, `dotnet restore` restaura primero el paquete en el que se empaqueta la herramienta y, a continuación, continúa con la restauración de las dependencias de la herramienta especificadas en su project.json.

## <a name="options"></a>Opciones

`root` 
    
Ruta de acceso opcional del archivo de proyecto para restaurar. 

`-h|--help`

Imprime una corta ayuda para el comando.

`-s|--source <SOURCE>`

Especifica un origen de paquetes de NuGet que se usará durante la operación de restauración. Esto invalida todos los orígenes especificados en los archivos NuGet.config. Al especificar esta opción varias veces, se pueden proporcionar varios orígenes.

`--packages <PACKAGES_DIRECTORY]`

Especifica el directorio donde colocar los paquetes restaurados. 

`--disable-parallel`

Deshabilita la restauración de varios proyectos en paralelo. 

`--configfile <FILE>`

El archivo de configuración (NuGet.config) que se usará para la operación de restauración.

`--no-cache`

Especifica que no se almacenen en caché los paquetes y las solicitudes HTTP.

` --ignore-failed-sources`

Solo se advierte sobre los orígenes con error si hay paquetes que satisfacen el requisito de versión.

`--no-dependencies`

Al restaurar un proyecto con referencias de P2P, no restaure las referencias, solo el proyecto raíz.

`--verbosity <LEVEL>`

Muestra esta cantidad de detalles en la salida. El nivel puede ser `normal`, `quiet` o `detailed`.

## <a name="examples"></a>Ejemplos

Restauración de dependencias y herramientas para el proyecto en el directorio actual:

`dotnet restore` 

Restauración de dependencias y herramientas para el proyecto `app1` encontrado en la ruta de acceso dada:

`dotnet restore ~/projects/app1/app1.csproj`
    
Restauración de dependencias y herramientas para el proyecto en el directorio actual con la ruta de acceso de archivo proporcionada como origen de reserva:

`dotnet restore -f c:\packages\mypackages` 

Restauración de dependencias y herramientas para el proyecto en el directorio actual, con las dos rutas de acceso de archivo proporcionadas como orígenes de reserva:

`dotnet restore -f c:\packages\mypackages -f c:\packages\myotherpackages` 

Restauración de dependencias y herramientas para el proyecto en el directorio actual y visualización únicamente de los errores en la salida:

`dotnet restore --verbosity Error`

