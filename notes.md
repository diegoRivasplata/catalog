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

<Para configurar la base de datos de mongo primero>
<en appsettings.json>
      "MongoDbSettings": 
      {
            "Host": "localhost",
            "Port": "27017"
      }
<en startup>
      services.AddSingleton<IMongoClient>(ServiceProvider => 
      {
        var settings = Configuration.GetSection(nameof(MongoDbSettings)).Get<MongoDbSettings>();
        return new MongoClient(settings.ConnectionString);
      });
      services.AddSingleton<IItemsRepository, MongoDbItemsRepository>();

<crear la clase mongodbsettgins.cs>
      namespace Catalog.Settings
      {
            public class MongoDbSettings
            {
                  public string Host { get; set; }
                  public int Port { get; set; }

                  public string ConnectionString
                  {
                        get
                        {
                        return $"mongodb://{Host}:{Port}";
                        }
                  }
            }
      }
