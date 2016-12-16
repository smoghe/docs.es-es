---
title: "C&#243;mo: Devolver una consulta desde un m&#233;todo (Gu&#237;a de programaci&#243;n de C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "consulta de devoluciones de métodos [C#]"
  - "consultas [LINQ en C#], consulta de devoluciones de métodos"
  - "expresiones de consulta [LINQ en C#], consulta de devoluciones de métodos"
ms.assetid: 9d6f20a7-f085-44cf-9df3-71948255ec68
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# C&#243;mo: Devolver una consulta desde un m&#233;todo (Gu&#237;a de programaci&#243;n de C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

En este ejemplo se muestra cómo se devuelve una consulta desde un método como valor devuelto y como parámetro `out`.  
  
 Cualquier consulta debe tener un tipo de <xref:System.Collections.IEnumerable> o <xref:System.Collections.Generic.IEnumerable%601>, o un tipo derivado como <xref:System.Linq.IQueryable%601>.  Por consiguiente, cualquier valor devuelto o parámetro `out` de un método que devuelve una consulta también debe tener ese tipo.  Si un método materializa una consulta en un tipo <xref:System.Collections.Generic.List%601> o <xref:System.Array> concreto, se considera que está devolviendo los resultados de la consulta en lugar de la propia consulta.  Una variable de consulta devuelta desde un método se puede componer o modificar.  
  
## Ejemplo  
 En el ejemplo siguiente, el primer método devuelve una consulta como valor devuelto, mientras que el segundo método devuelve una consulta como parámetro `out`.  Tenga en cuenta que, en ambos casos, se devuelve una consulta, no los resultados de la consulta.  
  
 [!code-cs[csProgGuideLINQ#80](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-return-a-query-from-a-method_1.cs)]  
  
## Compilar el código  
  
-   Cree un proyecto [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)] que tenga como destino la versión 3.5 u otra posterior de.NET Framework.  De manera predeterminada, el proyecto incluye una referencia a System.Core.dll y una directiva `using` para el espacio de nombres System.Linq.  
  
-   Reemplace la clase por el código del ejemplo.  
  
-   Presione F5 para compilar y ejecutar el programa.  
  
-   Presione cualquier tecla para salir de la ventana de consola.  
  
## Vea también  
 [Expresiones de consulta LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)