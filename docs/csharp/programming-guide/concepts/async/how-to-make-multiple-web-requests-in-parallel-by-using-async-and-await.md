---
title: "Cómo: Hacer varias solicitudes web en paralelo usando async y await (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 19745899-f97a-4499-a7c7-e813d1447580
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: eb358daf212b171acd998a1aa74fe2ecd82a239a
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await-c"></a>Cómo: Hacer varias solicitudes web en paralelo usando async y await (C#)
En un método asincrónico, las tareas se inician en el momento de crearse. El operador [await](../../../../csharp/language-reference/keywords/await.md) se aplica a la tarea en el momento del método en que no se puede continuar el procesamiento hasta que finalice la tarea. A menudo se espera una tarea en cuanto se crea, como se muestra en el ejemplo siguiente.  
  
```csharp  
var result = await someWebAccessMethodAsync(url);  
```  
  
 Pero puede separar la creación de la tarea de la espera si el programa tiene otro trabajo por efectuar que no dependa de la finalización de la tarea.  
  
```csharp  
// The following line creates and starts the task.  
var myTask = someWebAccessMethodAsync(url);  
  
// While the task is running, you can do other work that doesn't depend  
// on the results of the task.  
// . . . . .  
  
// The application of await suspends the rest of this method until the task is complete.  
var result = await myTask;  
  
```  
  
 Entre el inicio de una tarea y la espera puede iniciar otras tareas. Las tareas adicionales se ejecutan implícitamente en paralelo, pero no se crean subprocesos adicionales.  
  
 El programa siguiente inicia tres descargas web asincrónicas y las espera en el orden en el que se han llamado. Observe que, al ejecutar el programa, las tareas no siempre finalizan en el orden en que se han creado y esperado. Empiezan a ejecutarse en el momento de crearse y una o más tareas podrían finalizar antes de que el método llegue a las expresiones await.  
  
> [!NOTE]
>  Para llevar a cabo este proyecto, debe tener instalados en el equipo Visual Studio 2012 o posterior y .NET Framework 4.5 o posterior.  
  
 Para ver otro ejemplo que inicia varias tareas al mismo tiempo, vea [How to: Extend the async Walkthrough by Using Task.WhenAll (C#)](../../../../csharp/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md) (Cómo: Ampliar el tutorial de async usando Task.WhenAll (C#)).  
  
 Puede descargar el código de este ejemplo en [Muestras de código para desarrollador](http://go.microsoft.com/fwlink/?LinkId=254906).  
  
### <a name="to-set-up-the-project"></a>Para configurar el proyecto  
  
1.  Para configurar una aplicación WPF, lleve a cabo los siguientes pasos. Encontrará instrucciones detalladas de estos pasos en [Walkthrough: Accessing the Web by Using async and await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md) (Tutorial: Acceso a la web usando async y await [C#]).  
  
    -   Cree una aplicación WPF que contenga un cuadro de texto y un botón. Asigne al botón el nombre `startButton` y, al cuadro de texto, `resultsTextBox`.  
  
    -   Agregue una referencia para <xref:System.Net.Http>.  
  
    -   En el archivo MainWindow.xaml.cs, agregue una directiva `using` para `System.Net.Http`.  
  
### <a name="to-add-the-code"></a>Para agregar el código  
  
1.  En la ventana de diseño, MainWindow.xaml, haga doble clic en el botón para crear el controlador de eventos `startButton_Click` en MainWindow.xaml.cs.  
  
2.  Copie el código siguiente y péguelo en el cuerpo de `startButton_Click` en MainWindow.xaml.cs.  
  
    ```csharp  
    resultsTextBox.Clear();  
    await CreateMultipleTasksAsync();  
    resultsTextBox.Text += "\r\n\r\nControl returned to startButton_Click.\r\n";  
    ```  
  
     El código llama a un método asincrónico, `CreateMultipleTasksAsync`, que dirige la aplicación.  
  
3.  Agregue los siguientes métodos de soporte técnico al proyecto:  
  
    -   `ProcessURLAsync` usa un método <xref:System.Net.Http.HttpClient> para descargar el contenido de un sitio web como una matriz de bytes. Luego, el método de soporte, `ProcessURLAsync`, muestra y devuelve la longitud de la matriz.  
  
    -   `DisplayResults` muestra el número de bytes de la matriz de bytes de cada dirección URL. En esta pantalla se muestra cuándo se ha terminado la descarga de cada tarea.  
  
     Copie los métodos siguientes y péguelos después del controlador de eventos `startButton_Click` en MainWindow.xaml.cs.  
  
    ```csharp  
    async Task<int> ProcessURLAsync(string url, HttpClient client)  
    {  
        var byteArray = await client.GetByteArrayAsync(url);  
        DisplayResults(url, byteArray);  
        return byteArray.Length;  
    }  
  
    private void DisplayResults(string url, byte[] content)  
    {  
        // Display the length of each website. The string format   
        // is designed to be used with a monospaced font, such as  
        // Lucida Console or Global Monospace.  
        var bytes = content.Length;  
        // Strip off the "http://".  
        var displayURL = url.Replace("http://", "");  
        resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
    }  
    ```  
  
4.  Por último, defina el método `CreateMultipleTasksAsync`, que lleva a cabo los siguientes pasos.  
  
    -   El método declara un objeto `HttpClient`, que necesita para obtener acceso al método <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> en `ProcessURLAsync`.  
  
    -   El método crea e inicia tres tareas de tipo <xref:System.Threading.Tasks.Task%601>, donde `TResult` es un entero. A medida que finaliza cada tarea, `DisplayResults` muestra la dirección URL de la tarea y la longitud del contenido descargado. Dado que las tareas se ejecutan de manera asincrónica, el orden en que aparecen los resultados puede ser diferente del orden en que se han declarado.  
  
    -   El método espera la finalización de cada tarea. Cada operador `await` suspende la ejecución de `CreateMultipleTasksAsync` hasta que finalice la tarea esperada. El operador también recupera el valor devuelto de la llamada a `ProcessURLAsync` desde cada tarea finalizada.  
  
    -   Una vez concluidas las tareas y recuperados los valores enteros, el método suma las longitudes de los sitios web y muestra el resultado.  
  
     Copie el método siguiente y péguelo en la solución.  
  
    ```csharp  
    private async Task CreateMultipleTasksAsync()  
    {  
        // Declare an HttpClient object, and increase the buffer size. The  
        // default buffer size is 65,536.  
        HttpClient client =  
            new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
  
        // Create and start the tasks. As each task finishes, DisplayResults   
        // displays its length.  
        Task<int> download1 =   
            ProcessURLAsync("http://msdn.microsoft.com", client);  
        Task<int> download2 =   
            ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client);  
        Task<int> download3 =   
            ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client);  
  
        // Await each task.  
        int length1 = await download1;  
        int length2 = await download2;  
        int length3 = await download3;  
  
        int total = length1 + length2 + length3;  
  
        // Display the total count for the downloaded websites.  
        resultsTextBox.Text +=  
            string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
    }  
    ```  
  
5.  Presione la tecla F5 para ejecutar el programa y elija el botón **Inicio** .  
  
     Ejecute el programa varias veces para comprobar que las tres tareas no finalizan siempre en el mismo orden y que el orden en el que finalizan no es necesariamente el orden en que se han creado y esperado.  
  
## <a name="example"></a>Ejemplo  
 El código siguiente contiene el ejemplo completo.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Documents;  
using System.Windows.Input;  
using System.Windows.Media;  
using System.Windows.Media.Imaging;  
using System.Windows.Navigation;  
using System.Windows.Shapes;  
  
// Add the following using directive, and add a reference for System.Net.Http.  
using System.Net.Http;  
  
namespace AsyncExample_MultipleTasks  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            resultsTextBox.Clear();  
            await CreateMultipleTasksAsync();  
            resultsTextBox.Text += "\r\n\r\nControl returned to startButton_Click.\r\n";  
        }  
  
        private async Task CreateMultipleTasksAsync()  
        {  
            // Declare an HttpClient object, and increase the buffer size. The  
            // default buffer size is 65,536.  
            HttpClient client =  
                new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
  
            // Create and start the tasks. As each task finishes, DisplayResults   
            // displays its length.  
            Task<int> download1 =   
                ProcessURLAsync("http://msdn.microsoft.com", client);  
            Task<int> download2 =   
                ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client);  
            Task<int> download3 =   
                ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client);  
  
            // Await each task.  
            int length1 = await download1;  
            int length2 = await download2;  
            int length3 = await download3;  
  
            int total = length1 + length2 + length3;  
  
            // Display the total count for the downloaded websites.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        async Task<int> ProcessURLAsync(string url, HttpClient client)  
        {  
            var byteArray = await client.GetByteArrayAsync(url);  
            DisplayResults(url, byteArray);  
            return byteArray.Length;  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each website. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "http://".  
            var displayURL = url.Replace("http://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Walkthrough: Accessing the Web by Using async and await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)  (Tutorial: Acceso a la web usando async y await [C#])  
 [Programación asincrónica con async y await (C#)](../../../../csharp/programming-guide/concepts/async/index.md)   
 [How to: Extend the async Walkthrough by Using Task.WhenAll (C#)](../../../../csharp/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md) (Cómo: Ampliar el tutorial de async usando Task.WhenAll (C#))
