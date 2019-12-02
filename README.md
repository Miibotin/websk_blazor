# Blazor

<img src="https://devblogs.microsoft.com/aspnet/wp-content/uploads/sites/16/2019/04/BrandBlazor_nohalo_1000x.png" alt="blazor" width="225" heigth="225">

### Sisällyksen pöytä

# Yleistä
Blazor on Microsoftin kehittämä Front-end websovelluskehys, minkä avulla pystytään luomaan SPA-sovelluksia. Kyseinen kehys käyttää C#-ohjelmointikieltä ja pyörii .NET-ympäristössä. Tästä syystä websovelluskehityksen tukena on laaja kirjo Microsoftin kehittämiä kirjastoja, sekä valmis infrastruktuuri kehitystä varten.

## .NET
Kuten edellisessä kappaleessa kerrottiin, .NET-ohjelmistokehys tarjoaa laajan valikoiman kirjastoja sovelluskehitykseen. Näistä kaikille tutuin kirjasto Ohjelmoinnin Perusteet-kurssilta lienee System, mikä on C#-kielen olennaisin kirjasto.
```c#
System.Console.Writeline("Hello World!");
```
_Yllä oleva esimerkki kuvastaa System-nimiavaruudesta löytyvän Console-luokan Writeline-metodia._

Kattavan luokkakirjaston lisäksi muita .NET:n ominaisuuksia voi lukea [**tästä linkistä!**](https://docs.microsoft.com/fi-fi/dotnet/standard/)

[**.NET Core vs .NET Framework**](https://docs.microsoft.com/fi-fi/dotnet/standard/choosing-core-framework-server?toc=%2Faspnet%2Fcore%2Ftoc.json&bc=%2Faspnet%2Fcore%2Fbreadcrumb%2Ftoc.json&view=aspnetcore-3.0) - Hyödyllinen linkki kertomaan näiden kahden termin eroja ja niiden eri käyttötarkoituksista.

[**.NET:n Github-repositorio**](https://github.com/dotnet)

## ASP.NET<div>
Jos C#-kielellä halutaan luoda dynaamisia nettisivuja/applikaatioita, pelkkä .NET-kehys ei siihen riitä. Tätä varten Microsoft on kehittänyt ASP.NET-ohjelmistokehyksen .NET:n rinnalle. ASP<span>.NET on vapaata lähdekoodia ja sisältää omien (ja perus .NET:n) luokkakirjastojen lisäksi valmiita kehyksiä websovellusten tekoon, kuten [MVC](https://docs.microsoft.com/fi-fi/aspnet/core/mvc/overview?view=aspnetcore-3.0), [Entity Framework](https://docs.microsoft.com/en-us/ef/) ja [Web Forms](https://docs.microsoft.com/fi-fi/aspnet/web-forms/). Blazor on ASP.NET-perheen uusin lisäys, minkä ensimmäinen versio lisättiin ASP<span>.NET Core versiossa 3.0 (kirjoitushetkellä uusin virallinen julkaisu).

```c#
@{
    var message = "";
    var weekday = DateTime.Now.DayOfWeek;
    var day = weekday.ToString();
}
<html>
    <body>
        @switch(day)
        {
            case "Monday":
                message = "This is the first weekday.";
                break;
            case "Thursday":
                message = "Only one day before weekend.";
                break;
            case "Friday":
                message = "Tomorrow is weekend!";
                break;
            default:
                message = "Today is " + day;
                break;
        }
        <p> @message </p>
    </body>
</html>
```
_Yllä olevassa kuvassa [w3schools-sivulta](https://www.w3schools.com/asp/showfile_c.asp?filename=try_razor_cs_013) lainattu esimerkki ASP-sovelluksesta. ASP lyhenne tulee sanoista Active Server Pages._

[**ASP.NET Core:n dokumentaatio**](https://docs.microsoft.com/en-us/aspnet/core/?view=aspnetcore-3.0)

[**ASP.NET vs ASP.NET Core**](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/choose-aspnet-framework?view=aspnetcore-3.0) - Hyödyllinen linkki kertomaan näiden kahden termin eroja ja niiden eri käyttötarkoituksista.

[**ASP.NET:n Github-repositorio**](https://github.com/aspnet)

# Mikä on Blazor?

(Tähän vielä lisää)
Blazorista on kirjoitushetkellä julkaistu 2 versiota, joiden toiminnallisuus eroaa vain tavasta tuoda sovellus loppukäyttäjälle.

## Blazor Server

Blazorin ensimmäinen versio, Blazor Server, toimii suht perinteisellä tavalla. Applikaatio sekä pyörii että ajaa toimintoja ASP.NET-palvelimelta käsin, jolloin kaikki muutokset tapahtuvat loppukäyttäjän selaimen ulkopuolella ja selaimelle tuodaan vain päivitetty DOM. Eli jos käyttäjä painaa painiketta mikä vaihtaa ruudulla näkyvän luvun arvoa yhdellä, tehdään pyyntö palvelimelle missä Blazor tekee tarvittavat muutokset komponenttiin/komponentteihin ja palauttaa nämä takaisin käyttäjän selaimelle. Kaikki nämä muutokset tuodaan ja viedään SignalR-komponentin välityksellä. Blazor Server julkaistiin ASP<span>.NET Core 3.0 version mukana.

![Kuva](https://docs.microsoft.com/en-us/aspnet/core/blazor/index/_static/blazor-server.png?view=aspnetcore-3.0 "Tämä on kuva")

_Yllä olevassa kuvassa kuvattu Blazor Serverin toiminnallisuutta. Kuva on lainattu Microsoftin [Blazor-dokumentaatiosta](https://docs.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-3.0)._

Loppukäyttäjän selaimen tuen ja suorituskyvyn riippumattomuus tekee Blazor Serveristä vahvan valinnan isojenkin sovelluksien luontiin, sillä selaimelle ei tarvitse ladata kuin Blazorin luoma dynaaminen websovellus. Tällöin olisi myös käytössä täysi tuki .NET:n työkaluihin, eikä sovelluksen komponentteja/koodia tuoda käyttäjälle. Internet yhteyden välinen viive voi toisaalta koitua hankalaksi, sillä käyttäjä ei välttämättä heti koe tapahtuvaa muutosta ja se voi pilata käyttäjäkokemuksen. Hyvään verkkoinfrastruktuuriin on siis kannattavaa investoida.

### SignalR

Microsoftin kehittämän SignalR komponentin avulla Blazor Server pystyy kommunikoimaan selaimen kanssa, saaden tietoa tarvittavista käyttöliittymän muutoksista ja palauttamaan pyyntöjen mukaisen tuloksen takaisin loppukäyttäjälle. SignalR hyödyntää HTML5:n [WebSocket](https://javascript.info/websocket) APIa toimiakseen realiajassa.

## Blazor WebAssembly

Blazor Wasm, eli Blazor WebAssembly, on uudempi hostausmalli, mikä käyttää nimensä mukaisesti WebAssembly-teknologiaa pyörittämään .NET-applikaatioita suoraan selaimessa. Palvelimelta käyttäjän selaimelle ladataan C# ja Razor tiedostoista koostuvat .NET-kielikokoelmat, sekä .NET-ajoympäristö, minkä avulla Blazor Wasm pystyy konfiguroimaan kokoelmista staattiset tiedostot sovelluksen ajoa varten. Tämän toimenpiteen jälkeen Blazor applikaatio toimii ilman erillisen .NET-palvelimen riippuvuutta. Blazor Wasm:n on tarkoitus julkaista ASP.NET Core 3.1 version mukana, minkä arvioidaan julkaistavan toukokuussa 2020. (lähde)

![Kuva](https://docs.microsoft.com/en-us/aspnet/core/blazor/index/_static/blazor-webassembly.png?view=aspnetcore-3.0, "Tämä on kuva")

_Yllä olevassa kuvassa kuvattu Blazor WebAssemblyn toiminnallisuutta. Kuva on lainattu Microsoftin [Blazor-dokumentaatiosta](https://docs.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-3.0)._

Vaikka Blazor WebAssembly on vielä kehitysvaiheessa oleva vaihtoehto Blazor-applikaatioiden luontiin, on se hyväksi vaihtoehdoksi Serverin rinnalle todettu. Koska Blazor Wasm tuottaa julkaisuvaiheessa sovelluksesta staattisia tiedostoja, ei palvelimen tarvitse suoraan olla .NET-palvelin, vaan mikä tahansa tiedostojen jakotapa kelpaa. Kuhan selain tukee WebAssembly-teknologiaa ja sovellus on kevyt ladata selaimelle (Riippuu sovelluksen koosta. Buildattujen sovelluksien kokoa kehitetään vielä.), viiveetön interaktiivisuus piristää mukavasti käyttäjäkokemusta, varsinkin jos sovellukseen sisällytetään mukaan myös PWA-mahdollisuudet. Sovelluksen latauskoon lisäksi täytyy ottaa myös huomioon, että WebAssemblyn kanssa Blazor käyttää loppukäyttäjän hardwarea, joten suorituskyky on tärkeässä asemassa. Myös kaikkia .NET:n ominaisuuksia ei pystytä vielä kirjoitushetkellä toteuttamaan.

### WebAssembly

WebAssembly on matalan tason ohjelmointikieli, minkä avulla selainympäristössä voi ajaa korkean tason ohjelmointikieliä, kuten C, C++ ja Rust, kääntämällä lähdekoodi binäärimuotoon mitä selain kykenee lukemaan. Käännetty sovellus ajetaan tämän jälkeen selaimen JavaScript-moottorin(?) päällä. Wasmin avulla pystytään luomaan optimoituja websovelluksia kielillä, joiden alkup. tarkoitus on selainten ulkopuolella ja mihin JavaScriptin suorituskyky ei riitä. WebAssembly myös toimii JavaScriptin kanssa yhteistyössä. .NET hyödyntää tämän teknologian tarjoamia mahdollisuuksia kääntämään ja ajamaan Blazorin tiedostot natiivisti selainympäristössä ilman ylimääräisten lisäosien asentamista. WebAssembly on vapaata lähdekoodia ja [toimii kaikissa moderneissa selaimissa.](https://caniuse.com/#feat=wasm)

[**WebAssembly Editor**](https://mbebenita.github.io/WasmExplorer/) ja [**WebAssembly Studio(BETA)**](https://webassembly.studio/)

[**Doom 3 Wasm**](https://wasm.continuation-labs.com/d3demo/)
