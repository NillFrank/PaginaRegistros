# PaginaRegistros
Solución para implementación de paginado de registros en un datagridview,
estructura en capas, cuatro proyectos de libreria de clases de .NET standar
desarrollado en lenguaje C# el objeto del desarrollo es hacer el uso de una mejor
practica al momento de mostrar los datos en una grilla, se hace uso de clases
para este ejemplo se usa el gestor de base de datos postgreSQL, tranquilamente
se puede usar cualquier otro gestos de bases de datos.

Para utilizar otro gestor de base datos simplemente modifique el archivo de configuracion app.config

```
<connectionStrings>
  <add connectionString="Server=127.0.0.1;Port=5453;Database=AdventureWorks;Username=postgresql;Password=P@ssw0rds" name="postgreSQL" />
</connectionStrings>
```
Por cada nuevo SGBD solo copie una nueva linea de conexion ejemplo:
```
<connectionStrings>
  <add connectionString="Server=127.0.0.1;Port=5453;Database=AdventureWorks;Username=postgresql;Password=P@ssw0rds" name="postgreSQL" /> 
  <add connectionString="Server=myServerAddress;Database=myDataBase;Trusted_Connection=True;" name="servidor_SGBD" />
</connectionStrings>
```
  para invocación de las lineas de conexion se ejecuta lo siguiente:
```  
using System.Configuration;
namespace Cp_Configura
{
    public class CnnHost
    {
        public static string CnnPgSQL()
        {
            const string svr = "PostgreSQL";
            return Conectarme(nameof(svr));
        }
        public static string CnnMsSQL()
        {
            const string svr = "servidor_SGBD";
            return Conectarme(nameof(svr));
        }
        public static string CnnMySQL()
        {
            const string svr= "MySQL";
            return Conectarme(nameof(svr));
        }
        private static string Conectarme(string cn="")
        {
            var ConfigSection = ConfigurationManager.ConnectionStrings[cn].ConnectionString;
            return ConfigSection;
        }
    }
}
using (NpgsqlConnection cn = new NpgsqlConnection(CnnHost.CnnPgSQL()))
            {
              resto de la implementación
            }
```
