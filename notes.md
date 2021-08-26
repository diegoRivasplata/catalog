.net con mongoDB

https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mongo-app?view=aspnetcore-5.0&tabs=visual-studio

<para que el programa sea confiable	al browser>
      ->	en la consola dotnet dev-certs https --trust

<para que no se abra un browser cada vez que se ejecuta el programa>			
 		  -> 	en el archivo launch.json eliminar la parte de startup

<para acelerar el build del proyecto>
      -> 	en task.json debajo de problemMatcher
						"group": 
            {
        			"kind": "build",
       	 			"isDefault": true
     				}
<registrar repositorio en startup.cs>
      ->	services.AddSingleton<interface, implementation>();

<descargar nuget de mongo>
      -> 	dotnet add package MongoDB.Driver

<al momento de ejecutar el programa .net remueve el sufijo Async por eso
al decir nameof(GetItemAsync), GetItemAsync se convierte en GetItem
y no encuentra el metodo>
      -> en startUp.cs
          services.AddControllers(options =>
          {
            options.SuppressAsyncSuffixInActionNames = false;
          });
