# Blazor

### Sisällyksen pöytä

# Yleistä
Blazor on Microsoftin kehittämä Front-end websovelluskehys, minkä avulla pystytään luomaan SPA-sovelluksia. Kyseinen kehys käyttää C#-ohjelmointikieltä ja pyörii .NET-ympäristössä. Tästä syystä websovelluskehityksen tukena on laaja kirjo Microsoftin kehittämiä kirjastoja, sekä valmis infrastruktuuri kehitystä varten.

## .NET
Kuten edellisessä kappaleessa kerrottiin, .NET-ohjelmistokehys tarjoaa laajan valikoiman kirjastoja sovelluskehitykseen. Näistä kaikille tutuin kirjasto Ohjelmoinnin Perusteet-kurssilta lienee System, mikä on C#-kielen olennaisin kirjasto.
```c#
System.Console.Writeline("Hello World!");
```
_Yllä oleva esimerkki kuvastaa System-nimiavaruudesta löytyvän Console-luokan Writeline-metodia. Hyvin tuttu varmasti jokaiselle meistä._

Kattavan luokkakirjaston lisäksi muita .NET:n ominaisuuksia voi lukea [**tästä linkistä!**](https://docs.microsoft.com/fi-fi/dotnet/standard/)

[**.NET Core vs .NET Framework**](https://docs.microsoft.com/fi-fi/dotnet/standard/choosing-core-framework-server?toc=%2Faspnet%2Fcore%2Ftoc.json&bc=%2Faspnet%2Fcore%2Fbreadcrumb%2Ftoc.json&view=aspnetcore-3.0) - Hyödyllinen linkki kertomaan näiden kahden termin eroja ja niiden eri käyttötarkoituksista.

[**.NET:n Github-repositorio**](https://github.com/dotnet)

## ASP.NET<div>
Jos C#-kielellä halutaan luoda dynaamisia nettisivuja/applikaatioita, pelkkä .NET-kehys ei siihen riitä. Tätä varten Microsoft on kehittänyt ASP.NET-ohjelmistokehyksen .NET:n rinnalle. ASP<span>.NET on vapaata lähdekoodia ja sisältää omien (ja perus .NET:n) luokkakirjastojen lisäksi valmiita kehyksiä websovellusten tekoon, kuten [MVC](https://docs.microsoft.com/fi-fi/aspnet/core/mvc/overview?view=aspnetcore-3.0), [Entity Framework](https://docs.microsoft.com/en-us/ef/) ja [Web Forms](https://docs.microsoft.com/fi-fi/aspnet/web-forms/). Blazor on ASP.NET-perheen uusin lisäys, minkä ensimmäinen versio lisättiin ASP<span>.NET Core versiossa 3.0 (kirjoitushetkellä uusin virallinen julkaisu).

```c#
@{
    var message="";
    var weekday=DateTime.Now.DayOfWeek;
    var day=weekday.ToString();
}
<html>
    <body>
        @switch(day)
        {
            case "Monday":
                message="This is the first weekday.";
                break;
            case "Thursday":
                message="Only one day before weekend.";
                break;
            case "Friday":
                message="Tomorrow is weekend!";
                break;
            default:
                message="Today is " + day;
                break;
        }
        <p>@message</p>
    </body>
</html>
```
_Yllä olevassa kuvassa [w3schools-sivulta](https://www.w3schools.com/asp/showfile_c.asp?filename=try_razor_cs_013) lainattu esimerkki ASP-sovelluksesta. ASP lyhenne tulee sanoista Active Server Pages._

[**ASP.NET Core:n dokumentaatio**](https://docs.microsoft.com/en-us/aspnet/core/?view=aspnetcore-3.0)

[**ASP.NET vs ASP.NET Core**](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/choose-aspnet-framework?view=aspnetcore-3.0) - Hyödyllinen linkki kertomaan näiden kahden termin eroja ja niiden eri käyttötarkoituksista.
# Blazor