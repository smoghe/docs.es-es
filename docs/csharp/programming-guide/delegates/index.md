---
title: "Delegados (Gu&#237;a de programaci&#243;n de C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "lenguaje C#, delegados"
  - "delegados [C#]"
ms.assetid: 97de039b-c76b-4b9c-a27d-8c1e1c8d93da
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# Delegados (Gu&#237;a de programaci&#243;n de C#)
Un [delegado](../../../csharp/language-reference/keywords/delegate.md) es un tipo que representa referencias a métodos con una lista de parámetros determinada y un tipo de valor devuelto.  Cuando se crea una instancia de un delegado, puede asociar su instancia a cualquier método mediante una signatura compatible y un tipo de valor devuelto.  Puede invocar \(o llamar\) al método a través de la instancia del delegado.  
  
 Los delegados se utilizan para pasar métodos como argumentos a otros métodos.  Los controladores de eventos no son más que métodos que se invocan a través de delegados.  Cree un método personalizado y una clase, como un control de Windows, podrá llamar al método cuando se produzca un determinado evento.  En el siguiente ejemplo se muestra una declaración de delegado:  
  
 [!code-cs[csProgGuideDelegates#20](../../../csharp/programming-guide/delegates/codesnippet/CSharp/index_1.cs)]  
  
 Cualquier método de cualquier clase o struct accesible que coincida con el tipo de delegado se puede asignar al delegado.  El método puede ser estático o de instancia.  Esto permite cambiar las llamadas a métodos mediante programación y agregar nuevo código a las clases existentes.  
  
> [!NOTE]
>  En el contexto de la sobrecarga de métodos, la signatura de un método no incluye el valor devuelto.  Sin embargo, en el contexto de los delegados, la signatura sí lo incluye.  En otras palabras, un método debe tener el mismo tipo de valor devuelto que el delegado.  
  
 Esta capacidad de hacer referencia a un método como parámetro hace que los delegados sean idóneos para definir métodos de devolución de llamada.  Por ejemplo, una referencia a un método que compara dos objetos podría pasarse como argumento a un algoritmo de ordenación.  Dado que el código de comparación está en un procedimiento independiente, el algoritmo de ordenación se puede escribir de manera más general.  
  
## Información general sobre los delegados  
 Los delegados tienen las propiedades siguientes:  
  
-   Los delegados son como los punteros de función de C\+\+, pero tienen seguridad de tipos.  
  
-   Los delegados permiten pasar los métodos como parámetros.  
  
-   Los delegados pueden usarse para definir métodos de devolución de llamada.  
  
-   Los delegados pueden encadenarse entre sí; por ejemplo, se puede llamar a varios métodos en un solo evento.  
  
-   No es necesario que los métodos coincidan exactamente con el tipo de delegado.  Para obtener más información, vea [Usar varianza en delegados](../Topic/Using%20Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md).  
  
-   La versión 2.0 de C\# presentó el concepto de [Métodos anónimos](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md), los cuales permiten pasar bloques de código como parámetros en lugar de un método definido por separado.  En C\# 3.0 se presentaron las expresiones lambda como una manera más concisa de escribir bloques de código alineado.  Tanto los métodos anónimos como las expresiones lambda \(en ciertos contextos\) se compilan en tipos de delegado.  Juntas, estas características se conocen ahora como funciones anónimas.  Para obtener más información sobre las expresiones lambda, vea [Funciones anónimas](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md).  
  
## En esta sección  
  
-   [Utilizar delegados](../../../csharp/programming-guide/delegates/using-delegates.md)  
  
-   [When to Use Delegates Instead of Interfaces \(C\# Programming Guide\)](http://msdn.microsoft.com/es-es/2e759bdf-7ca4-4005-8597-af92edf6d8f0)  
  
-   [Delegados con métodos con nombre y delegados con métodos anónimos](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)  
  
-   [Métodos anónimos](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)  
  
-   [Usar varianza en delegados](../Topic/Using%20Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)  
  
-   [Cómo: Combinar delegados \(delegados de multidifusión\)](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)  
  
-   [Cómo: Declarar un delegado, crear instancias del mismo y utilizarlo](../../../csharp/programming-guide/delegates/how-to-declare-instantiate-and-use-a-delegate.md)  
  
## Especificación del lenguaje C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Capítulos destacados del libro  
 [Delegates, Events, and Lambda Expressions](http://go.microsoft.com/fwlink/?LinkId=195395) en [C\# 3.0 Cookbook, Third Edition: More than 250 solutions for C\# 3.0 programmers](http://go.microsoft.com/fwlink/?LinkId=195369)  
  
 [Delegates and Events](http://go.microsoft.com/fwlink/?LinkId=195418) en [Learning C\# 3.0: Master the fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)  
  
## Vea también  
 <xref:System.Delegate>   
 [Guía de programación de C\#](../../../csharp/programming-guide/index.md)   
 [Eventos](../../../csharp/programming-guide/events/index.md)