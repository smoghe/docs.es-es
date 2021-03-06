---
title: "Realizar operaciones de combinación externa izquierda"
description: "Cómo realizar operaciones de combinación externa izquierda."
keywords: .NET, .NET Core, C#
author: stevehoag
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: f542cee6-3169-4dcf-a631-3a6a79ccd473
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6ba90a6fe16d4ba33e8b9e55c93f7365b6bc905b
ms.lasthandoff: 03/13/2017

---
# <a name="perform-left-outer-joins"></a>Realizar operaciones de combinación externa izquierda
Una combinación externa izquierda es una combinación en la que se devuelve cada elemento de la primera colección, independientemente de si tiene elementos correlacionados en la segunda colección. Puede usar LINQ para realizar una combinación externa izquierda llamando al método <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> en los resultados de una combinación agrupada.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo usar el método <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> en los resultados de una combinación agrupada para realizar una combinación externa izquierda.  
  
 El primer paso para generar una combinación externa izquierda de dos colecciones consiste en realizar una combinación interna usando una combinación agrupada. (Vea [Realizar combinaciones internas](perform-inner-joins.md) para obtener una explicación de este proceso). En este ejemplo, la lista de objetos de `Person` está unida a la lista de objetos `Pet` basándose en un objeto `Person` que coincide con `Pet.Owner`.  
  
 El segundo paso consiste en incluir cada elemento de la primera colección (izquierda) en el conjunto de resultados, incluso cuando no haya coincidencias en la colección derecha. Esto se realiza llamando a <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> en cada secuencia de elementos coincidentes de la combinación agrupada. En este ejemplo, se llama a <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> en cada secuencia de objetos `Pet` coincidentes. El método devuelve una colección que contiene un único, valor predeterminado si la secuencia de objetos `Pet` coincidentes está vacía para cualquier objeto `Person`, con lo que cada objeto `Person` se representa en la colección de resultados.  
  
> [!NOTE]
>  El valor predeterminado para un tipo de referencia es `null`; por consiguiente, el ejemplo busca una referencia NULL antes de tener acceso a cada elemento de cada colección de `Pet`.  
  
 [!code-cs[CsLINQProgJoining#7](../../../samples/snippets/csharp/concepts/linq/how-to-perform-left-outer-joins_1.cs)]  
 
## <a name="see-also"></a>Vea también  
 <xref:System.Linq.Enumerable.Join%2A>   
 <xref:System.Linq.Enumerable.GroupJoin%2A>   
 [Realizar combinaciones internas](perform-inner-joins.md)   
 [Realizar combinaciones agrupadas](perform-grouped-joins.md)   
 [Tipos anónimos](../programming-guide/classes-and-structs/anonymous-types.md)   
 
