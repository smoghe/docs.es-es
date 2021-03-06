---
title: "Propiedades implementadas autom&#225;ticamente (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AutoProperty"
  - "vb.AutoImplementedProperty"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "propiedades implementadas automáticamente [Visual Basic]"
  - "propiedades [Visual Basic], autoimplementadas"
  - "propiedades, implementadas automáticamente [Visual Basic]"
ms.assetid: 5c669f0b-cf95-4b4e-ae84-9cc55212ca87
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Propiedades implementadas autom&#225;ticamente (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Las *propiedades implementadas automáticamente* permiten especificar rápidamente una propiedad de una clase sin tener que escribir código para obtener \(`Get`\) y establecer \(`Set`\) la propiedad.  Al escribir código para una propiedad implementada automáticamente, el compilador de Visual Basic crea de manera automática un campo privado para almacenar la variable de propiedad, además de crear los procedimientos `Get` y `Set` asociados.  
  
 Con las propiedades implementadas automáticamente, una propiedad \(incluido un valor predeterminado\) puede declararse en una sola línea.  En el ejemplo siguiente se muestran tres declaraciones de propiedad.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#1](./codesnippet/VisualBasic/auto-implemented-properties_1.vb)]  
  
 Una propiedad implementada automáticamente equivale a una propiedad cuyo valor se almacena en un campo privado.  En el siguiente ejemplo de código se muestra una propiedad implementada automáticamente.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#5](./codesnippet/VisualBasic/auto-implemented-properties_2.vb)]  
  
 En el ejemplo de código siguiente se muestra el código equivalente al del ejemplo anterior de propiedad implementada automáticamente.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#2](./codesnippet/VisualBasic/auto-implemented-properties_3.vb)]  
  
 En el código siguiente se muestran las propiedades de solo lectura implementadoras:  
  
```vb  
Class Customer  
   Public ReadOnly Property Tags As New List(Of String)  
   Public ReadOnly Property Name As String = ""  
   Public ReadOnly Property File As String  
  
   Sub New(file As String)  
      Me.File = file  
   End Sub  
End Class  
  
```  
  
 Se pueden realizar asignaciones a la propiedad con expresiones de inicialización, como se muestra en el ejemplo, o se pueden realizar asignaciones a las propiedades en el constructor del tipo contenedor.  Siempre que lo desee, puede realizar asignaciones a los campos de respaldo de propiedades de solo lectura.  
  
## Campo de respaldo  
 Cuando se declara una propiedad implementada automáticamente, Visual Basic crea automáticamente un campo privado oculto denominado *campo de respaldo* que contiene el valor de propiedad.  El nombre del campo de respaldo es el nombre de la propiedad implementada automáticamente precedido por un carácter de subrayado \(\_\).  Por ejemplo, si declara una propiedad implementada automáticamente denominada `ID`, el campo de respaldo se denominará `_ID`.  Si se incluye un miembro de la clase que también se denomina `_ID`, se produce un conflicto de nomenclatura y Visual Basic informa de un error del compilador.  
  
 El campo de respaldo también tiene las siguientes características:  
  
-   El modificador de acceso del campo de respaldo siempre es `Private`, incluso cuando la misma propiedad tiene un nivel de acceso diferente, como `Public`.  
  
-   Si la propiedad está marcada como `Shared`, también se comparte el campo de respaldo.  
  
-   Los atributos especificados para la propiedad no se aplican al campo de respaldo.  
  
-   El acceso al campo de respaldo se puede realizar desde el código contenido en la clase y desde herramientas de depuración como la ventana Inspección.   Sin embargo, dicho campo no se muestra en una lista de finalización de palabras de IntelliSense.  
  
## Inicializar una propiedad implementada automáticamente  
 Cualquier expresión que se pueda usar para inicializar un campo es válida para inicializar una propiedad implementada automáticamente.  Al inicializar una propiedad implementada automáticamente, la expresión se evalúa y se pasa al procedimiento `Set` para la propiedad.  En los ejemplos de código siguientes se muestran algunas propiedades implementadas automáticamente que incluyen valores iniciales.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#3](./codesnippet/VisualBasic/auto-implemented-properties_4.vb)]  
  
 No se puede inicializar una propiedad implementada automáticamente que sea miembro de una `Interface` o que esté marcada como `MustOverride`.  
  
 Al declarar una propiedad implementada automáticamente como miembro de una `Structure`, solo se puede inicializar la propiedad implementada automáticamente si se marca como `Shared`.  
  
 Al declarar una propiedad implementada automáticamente como matriz, no se pueden especificar límites de matriz explícitos.  Sin embargo, se puede proporcionar un valor con un inicializador de matriz, como se muestra en los ejemplos siguientes.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#4](./codesnippet/VisualBasic/auto-implemented-properties_5.vb)]  
  
## Definiciones de propiedades que requieren sintaxis estándar  
 Las propiedades implementadas automáticamente son fáciles de usar y admiten muchos escenarios de programación.  Sin embargo, hay situaciones en las que no se puede usar una propiedad de este tipo y, en su lugar, debe usarse la sintaxis de propiedades estándar o *expandidas*.  
  
 Si desea realizar una de las acciones siguientes, tiene que usar la sintaxis de definición de propiedades expandidas:  
  
-   Agregar código al procedimiento `Get` o `Set` de una propiedad, como código para validar los valores de entrada del procedimiento `Set`.  Por ejemplo, puede que desee comprobar si una cadena que representa un número de teléfono contiene la cantidad de números necesaria antes de establecer el valor de propiedad.  
  
-   Especificar distintos tipos de accesibilidad para los procedimientos `Get` y `Set`.  Por ejemplo, puede que desee establecer el procedimiento `Set` como `Private` y el procedimiento `Get` como `Public`.  
  
-   Crear propiedades de tipo `WriteOnly`.  
  
-   Usar propiedades parametrizadas \(incluidas las propiedades `Default`\).  Debe declarar una propiedad expandida para especificar un parámetro para la propiedad o para especificar parámetros adicionales para el procedimiento `Set`.  
  
-   Colocar un atributo en el campo de respaldo o cambiar el nivel de acceso del campo de respaldo.  
  
-   Proporcionar comentarios XML para el campo de respaldo.  
  
## Expandir una propiedad implementada automáticamente  
 Si tiene que convertir una propiedad implementada automáticamente en una propiedad expandida que contiene un procedimiento `Get` o `Set`, el Editor de código de Visual Basic puede generar automáticamente los procedimientos `Get` y `Set` y la instrucción `End Property` para la propiedad.  Para generar el código, se coloca el cursor en una línea en blanco a continuación de la instrucción `Property`, se escribe una `G` \(para `Get`\) o una `S` \(para `Set`\) y se presiona ENTRAR.  El Editor de código de Visual Basic genera automáticamente el procedimiento `Get` o `Set` para las propiedades de solo lectura y de solo escritura al presionar ENTRAR al final de una instrucción `Property`.  
  
## Vea también  
 [Cómo: Declarar y llamar a una propiedad predeterminada en Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [Cómo: Declarar una propiedad con niveles de acceso mixtos](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [Property \(Instrucción\)](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [ReadOnly](../../../../visual-basic/language-reference/modifiers/readonly.md)   
 [WriteOnly](../../../../visual-basic/language-reference/modifiers/writeonly.md)   
 [Objetos y clases](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)