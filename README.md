# Blazor

<img src="https://devblogs.microsoft.com/aspnet/wp-content/uploads/sites/16/2019/04/BrandBlazor_nohalo_1000x.png" alt="blazor" width="225" heigth="225">

# Sisällysluettelo

## [Yleistä](#yleistä-1)
>### [.NET](#NET-1)
>### [ASP.NET](#aspnet-1)
## [Mikä on Blazor?](#mikä-on-blazor-1)
>### [Rakenne](#rakenne-1)
>### [Komponentit](#komponentit-1)
>#### [@Page](#page-1)
>#### [@Layout](#layout-1)
>### [JavaScript Interop](#javascript-interop-1)
## [Blazorin mallit](#blazorin-mallit-1)
>### [Blazor Server](#blazor-server-1)
>#### [SignalR](#signalr-1)
>### [Blazor WebAssembly](#blazor-webassembly-1)
>#### [WebAssembly](#webassembly-1)
## [Esimerkki](#esimerkki-1)
## [Tehtävä](#tehtävä-1)


# Mitä tarvitset?

- [**.NET Core SDK 3.1**](https://dotnet.microsoft.com/download/dotnet-core/3.1) - Löytyy ohjeet kaikille alustoille
    - Varmista .NET:n toimivuus kirjoittamalla terminaaliin ```dotnet --info```
- Blazor WebAssembly-mallia varten lataa .NET:n Cli:tä hyödyntämällä uusin preview-templaatti
```
dotnet new -i Microsoft.AspNetCore.Blazor.Templates::3.1.0-preview4.19579.2
```
- Jos käytät Visual Studio Code-tekstieditoria, tarvitset [C#-lisäosan](https://github.com/OmniSharp/omnisharp-vscode/blob/master/README.md). _Kyseisen lisäosan IntelliSense on oman kokemuksen mukaan hyvin buginen Blazorin kehitykseen, mutta ajaa asiansa._
    - Helpommalla voit päästä käyttämällä virallista [Visual Studio-ohjelmankehitysympäristöä](https://visualstudio.microsoft.com/).

[**Get started with ASP.NET Core Blazor**](https://docs.microsoft.com/en-us/aspnet/core/blazor/get-started?view=aspnetcore-3.1&tabs=visual-studio)

# Yleistä
Blazor on Microsoftin kehittämä Front-end sovelluskehys, minkä avulla pystytään luomaan SPA-sovelluksia hyödyntämällä C#-ohjelmointikieltä ja .NET-ympäristön tarjoamia työkaluja. Tästä syystä kehityksen tukena on laaja kirjo Microsoftin kehittämiä kirjastoja, sekä valmis infrastruktuuri kehitystä varten.

## .NET

.NET on Microsoftin kehittämä kehitysympäristö, mikä sisältää kehittäjille ison infrastruktuurin työkaluja sovelluskehitykseen. .NET:n avulla pystyy luomaan lähes minkälaisia sovelluksia tahansa, aina perinteisistä työpöytäsovelluksista mobiili- ja web-sovelluksiin. Kehitysympäristö tarjoaa myös lukuisia erilaisia työkaluja kehityksen avuksi, kuten oman [komentoliittymän (CLI)](https://docs.microsoft.com/en-us/dotnet/core/tools/?tabs=netcore2x) ja [Common Language Runtime](https://docs.microsoft.com/en-us/dotnet/standard/clr)-ajoympäristön koodin kääntöön ja ajoon. .NET:llä yleisesti kehitetään Windows-alustoilla pyöriviä sovelluksia, mutta nykyään alustariippuvuudet ovat huomattavasti vähentyneet, varsinkin web-sovelluksien yleistymisen myötä. .NET tukee C#-kielen lisäksi myös F# ja Visual Basic-ohjelmointikieliä, C# on näistä se yleisin vaihtoehto.

Kuten aikaisemmin mainittiin, .NET-ohjelmistokehys tarjoaa ison valikoiman kirjastoja sovelluskehitykseen. Näistä kaikille tutuin kirjasto Ohjelmoinnin Perusteet -kurssilta lienee System, mikä on C#-kielen olennaisin kirjasto.

```c#
System.Console.Writeline("Hello World!");
```
_Yllä oleva esimerkki kuvastaa System-kirjastosta löytyvän Console-luokan Writeline-metodia. Normaalissa tilanteessa System-kirjasto on otettu käyttöön jo projektin luodessa, joten pelkkä ```Console.Writeline()``` riittää._

Kattavan luokkakirjaston lisäksi muita .NET:n ominaisuuksia voi lukea [**tästä linkistä!**](https://docs.microsoft.com/fi-fi/dotnet/standard/)

[**.NET:n etusivu**](https://dotnet.microsoft.com/)

[**.NET Core vs .NET Framework**](https://docs.microsoft.com/fi-fi/dotnet/standard/choosing-core-framework-server?toc=%2Faspnet%2Fcore%2Ftoc.json&bc=%2Faspnet%2Fcore%2Fbreadcrumb%2Ftoc.json&view=aspnetcore-3.0) - Hyödyllinen linkki kertomaan näiden kahden termin eroja ja niiden eri käyttötarkoituksista.

[**.NET:n Github-repositorio**](https://github.com/dotnet)

[**.NET ohjelmointikielet**](https://dotnet.microsoft.com/languages)

## ASP.NET<div>

Jos C#-kielellä halutaan luoda dynaamisia web-sovelluksia, pelkkä .NET-kehys ei siihen riitä. Tätä varten Microsoft on kehittänyt ASP.NET-ohjelmistokehyksen .NET:n rinnalle. ASP<span>.NET on vapaata lähdekoodia ja sisältää omien (ja perus .NET:n) luokkakirjastojen lisäksi valmiita kehyksiä websovellusten tekoon, kuten [MVC](https://docs.microsoft.com/fi-fi/aspnet/core/mvc/overview?view=aspnetcore-3.0) ja [Web Forms](https://docs.microsoft.com/fi-fi/aspnet/web-forms/). Blazor on ASP.NET-perheen uusin lisäys, minkä ensimmäinen versio lisättiin ASP<span>.NET Core versiossa 3.0 (kirjoitushetkellä uusin virallinen julkaisu).

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
_Yllä olevassa kuvassa [w3schools-sivulta](https://www.w3schools.com/asp/showfile_c.asp?filename=try_razor_cs_013) lainattu esimerkki ASP.NET-sovelluksesta._

[**ASP.NET:n etusivu**](https://dotnet.microsoft.com/apps/aspnet)

[**ASP.NET Core:n dokumentaatio**](https://docs.microsoft.com/en-us/aspnet/core/?view=aspnetcore-3.0)

[**ASP.NET vs ASP.NET Core**](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/choose-aspnet-framework?view=aspnetcore-3.0) - Hyödyllinen linkki kertomaan näiden kahden termin eroja ja niiden eri käyttötarkoituksista.

[**ASP.NET:n Github-repositorio**](https://github.com/aspnet)

# Mikä on Blazor?

Blazor toimii samalla tavalla kuten moni Front-end sovelluskehys, millä pystyy luomaan SPA-sovelluksia. Blazorin rakenne perustuu Razor-komponentteihin, millä voidaan hajauttaa sovelluksen kokonaisuuksia pienempiin osioihin. Tämä helpottaa koodin lukua, sekä myös mahdollistaa saman ominaisuuden käytön muualla sovelluksessa ilman uudelleenkirjoittamista.

Razor-komponenttien tiedostotyyppi on .razor, mikä käyttää ASP<span>.NET:n omaa [Razor-syntaksia](https://docs.microsoft.com/fi-fi/aspnet/core/mvc/views/razor?view=aspnetcore-3.1). Razor syntaksi yhdistää HTML- ja C#-kielet samaan tiedostoon, jotta komponentin logiikka ja ulkoasu pystytään tuottamaan samassa tiedostossa. ```@```-symbolin avulla voidaan sisällyttää C#-koodia HTML:n sekaan.

``` html
<div class="warning" style="display:@displaymessage">@Message</div>
```
_Ylhäällä on esimerkki kahdesta HTML-kielen sisään upotetusta C#-muuttujasta. Muuttujia voi jopa käyttää elementin tyylin määrittelyssä, kuten tässä esimerkissä vaikuttamaan kyseisen elementin renderöintiin._

ASP<span>.NET:n vuoksi Blazorin kehitykseen on ns. pellin alla valmis infrastruktuuri, joten kehittäjä voi keskittyä vaan luomaan kattavia web-sovelluksia. Blazorin keskeisimpiä ominaisuuksia ovat:

- [**Reititys**](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/routing?view=aspnetcore-3.1)
- [**Layouts**](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/layouts?view=aspnetcore-3.1)
- [**Lomakkeet ja validointi**](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/forms-validation?view=aspnetcore-3.1)
- [**Dependency injection**](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/dependency-injection?view=aspnetcore-3.1)
- [**JavaScript Interop**](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/javascript-interop?view=aspnetcore-3.1)

Tässä dokumentissa käydään läpi näitä ominaisuuksia. Lisää yllä mainituista ja myös muista ominaisuuksista voit lukea alla olevasta linkistä.

[**Blazorin dokumentaatio**](https://docs.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-3.1)

[**Blazorin Github-repositorio**](https://github.com/aspnet/Blazor)

[**Kattava ja ajankohtainen luento Blazorista**](https://www.youtube.com/watch?v=6BT2AF9PO5g)

## Rakenne

Täysin uudesta Blazor-projektista löytyy tiedostoja ja hakemistoja, joista on hyvä tietää seuraavanlaista:

- **Program.cs** - Sisältää sovelluksen aloituspisteen. Oletuksena kaikilla ASP<span>.NET:n sovelluksilla.
- **Startup.cs** - Kaikki sovelluksen käynnistykseen liittyvä logiikka sisällytetään tänne. Luokka sisältää 2 eri metodia:
    - ```ConfigureServices```-metodi konfiguroi sovelluksen mahdolliset [Dependency Injection](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-3.1)-servicet, tapa luoda kevyitä, uudelleen toistettavia ratkaisuja sovellukseen.
    - ```Configure```-metodi luo sovellukselle pipeline-prosessin. Oletuksena ```Configure``` lisää komponenttien juuren, App-komponentin DOMiin ```<app>```-elementiksi **(Vain WebAssembly-mallissa)**.
- **wwwroot**  - sisältää sovelluksen staattisen sisällön, kuten kuvat, skriptit ja tyylittelyt. Omia skripti- ja tyylitiedostoja voi laittaa tänne.
- **wwwroot/index.html** **(Blazor WebAssembly)** - Sovelluksen juuritiedosto, mihin sovelluksen logiikka renderöidään. Sisältää perus HTML-rungon lisäksi aiemmin mainitun App-komponentin. blazor.webassembly.js-tiedosto implementoidaan mukaan, mikä hoitaa .NET-ajoympäristön, sovelluksen ja sovelluksen riippuvuuksien latauksen käyttäjälle, sekä suorittaa sovelluksen ajoa selaimessa.
- **Pages/_Host.cshtml** **(Blazor Server)** - Sovelluksen juuritiedosto, mikä renderöinnin jälkeen lähetetään käyttäjälle. Sisältää Razor-syntaksia ja hoitaa App-komponentin renderöinnin. blazor.server.js-tiedosto implementoidaan mukaan, mikä asettaa yhteyden palvelimen ja selaimen välille [SignalR:n](#signalr-1) avulla.
- **App.razor** - Sovelluksen pääkomponentti, joka hoitaa [reitityksen](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/routing?view=aspnetcore-3.1) ja [ulkoasun](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/layouts?view=aspnetcore-3.1) määrittelyn.
- **Pages** - Hakemisto komponenteille mitkä on määritetty sivuiksi ```@page```-direktiivillä, joita voidaan hakea reitityksellä.
- **_Imports.razor** - Sisällyttää kaikki yleiset sovelluksen tarvittavat kirjastot ja luokat. Käyttäjä voi sisällyttää omia hakemistoja ja niiden komponentteja tai tiedostoja ```@using {projektin_nimi}.{hakemiston_nimi}```-esimerkillä.

## Komponentit

Kuten aiemmin on jo mainittu, komponenttien avulla sovellus voidaan hajauttaa pienimpiin osioihin, helpottamaan koodin luettavuutta ja vähentämään toistoa. Kehittäjän ei suotta tarvitse kirjoittaa uudelleen sovelluksen ominaisuutta, jos sen voi vaan upottaa sivulta toiselle yhdellä ```<ElementinNimi />```-tägillä.

### @Page

```@page```-direktiivillä määritetty komponentti toimii sovelluksen sivuna, minkä voi hakea sille määritetyn reitin mukaan.

``` html
@page "/"

<main>
    <h1>Hello, World!</h1>
</main>
```
_Yllä olevassa esimerkissä komponentti, mille on annettu ```@page```-direktiivillä sovelluksen juuripolku._

Yhdelle komponentille voi myös määrittää useamman reitin ja reiteille voi antaa parametreja.

``` c#
@page "/"
@page "/Homepage"
@page "/Homepage/{variable}"

<main>
    <h1>Hello, World!</h1>
</main>

@code{
    [Parameter]
    public string variable { get; set; } = "sivu";
}
```
_Nyt sivu voidaan löytää esimerkiksi osoitteesta ```localhost:5000/Homepage/sivu```_

### @Layout

``` html
<!-- MainLayout.razor -->
@inherits LayoutComponentBase

<HeaderLayout />

<main>
    @Body
</main>

<FooterLayout />
```
_Ylhäällä olevassa esimerkissä nähdään Blazorin oletus layout-komponentti ```MainLayout``` ja sen sisälle upotetut ```Header```- ja ```FooterLayout```-komponentit. ```LayoutComponentBase```-luokasta peritty ```@Body```-syntaksilla määritetään, mihin sovelluksen sisältö renderöidään._

Layout-komponenteilla voidaan määrittää sovellukselle ulkoasu, mitä koko softa tai osa siitä käyttää. Näiden avulla voidaan luoda yhtenäinen ulkoasu sovelluksen jokaiselle näkymälle. Sovellus tarvitsee yhden Layout-komponentin oletukseksi ```App.razor```-tiedostoon.

``` html
<!-- App.razor -->
<Router AppAssembly="@typeof(Program).Assembly">
    <Found Context="routeData">
        <RouteView RouteData="@routeData" DefaultLayout="@typeof(MainLayout)" />
    </Found>
    <NotFound>
        <LayoutView Layout="@typeof(MainLayout)">
            <p>Sorry, there's nothing at this address.</p>
        </LayoutView>
    </NotFound>
</Router>
```
_Ylhäällä olevassa esimerkissä ```App.razor```-tiedosto, mikä määrittää sovelluksen reitityksen ja ulkoasun, riippuen siitä, löytyykö tietystä reitistä komponenttia vai ei. Lisää Router-komponentista voit lukea [täältä.](https://docs.microsoft.com/en-us/aspnet/core/blazor/routing?view=aspnetcore-3.1#route-templates)_

Sovellukselle voi myös luoda vaihtoehtoisia näkymiä ja antaa niitä suoraan komponenttien käyttöön ```@layout {Layout-komponentin_nimi}```-direktiivillä.

``` c#
@page "/Todo"
@layout SecondLayout
```

[**Blazorin komponentit**](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/components?view=aspnetcore-3.1)

[**Blazorin ulkoasusta**](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/layouts?view=aspnetcore-3.1)

[**Blazorin reitityksestä**](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/routing?view=aspnetcore-3.1)
## JavaScript Interop

Blazor-sovellus pystyy kutsumaan JavaScript funktioita omilla metodeillaan JavaScript Interop:n avulla. Tällä voidaan vaikuttaa DOMin tai selaimen ominaisuuksiin, joihin Blazorilla ei välttämättä (vielä) pääse käsiksi. Kehittäjällä on myös tämän myötä enemmän mahdollisuuksia soveltaa kehityksessä, eikä sovellusta rajoiteta tietyn teknologian vuoksi.

Esimerkkinä käytetään yksinkertaista konsolin logausta. (Blazorilla tosin pystyy myös suoraan kirjaamaan konsoliin .NET:n omalla ```Console.Writeline```-metodilla)
``` javascript
// scripts.js
window.helloWorld = {
    console.log('Hello, World!') 
}
```

Yllä oleva skripti sijaitsee ```scripts.js```-tiedostossa, mikä pitää sijoittaa sovelluksen juuritiedostoon (_WebAssembly-mallissa wwwroot/index.html ja Server-mallissa Pages_/__Host.cshtml_). Tämän jälkeen voidaan palata takaisin Razor-komponenttiin ja lisätä tarvittava logiikka. ```@inject```-direktiivillä saadaan komponentille käyttöön Interop:n ```IJSRuntime```-rajapinta, minkä avulla luodaan asynkronisia pyyntöjä JavaScript-tiedostoihin.

``` html
<!-- Index.razor -->
@inject IJSRuntime _JSRuntime;
```
__Imports.razor-tiedostosta löytyy automaattisesti Microsoftin Interop-kirjasto, joten erikseen ei tarvitse asentaa uusia kirjastoja ominaisuuden käyttöönottoa varten._

Seuraavaksi tarvitsee vain kirjoittaa komponenttiin pyyntö oikeaan funktioon käyttämällä [dependency injection](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/dependency-injection?view=aspnetcore-3.1)-ominaisuuden avulla tuotua rajapintaa.

``` c#
// Index.razor @code-lohko
protected override void OnInitialized()
{
    _JSRuntime.InvokeVoidAsync("helloWorld");
}
```
_```protected override void OnInitialized()``` on yksi Blazor-sovelluksen lifecycle-metodeista. Lisää näistä voit lukea [täältä](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/lifecycle?view=aspnetcore-3.1)_

Ajaessa sovellusta Index.razor-tiedostosta selaimen konsoliin pitäisi tulla funktion mukainen tuloste. Lisää Interop:sta ja sen ominaisuuksista voit lukea alla olevasta linkistä.

[**JavaScript Interop**](https://docs.microsoft.com/fi-fi/aspnet/core/blazor/javascript-interop?view=aspnetcore-3.1)


# Blazorin mallit

Blazorista on kirjoitushetkellä saatavilla 2 versiota, joiden toiminnallisuus eroaa vain tavasta tuoda sovellus käyttäjälle.

## Blazor Server

Blazorin ensimmäinen versio, Blazor Server, toimii suhteellisen perinteisellä tavalla. Sovellus sekä pyörii että ajaa toimintoja ASP.NET-palvelimelta käsin, jolloin kaikki muutokset tapahtuvat loppukäyttäjän selaimen ulkopuolella ja selaimelle tuodaan vain päivitetty DOM. Eli jos käyttäjä painaa painiketta mikä vaihtaa ruudulla näkyvän luvun arvoa yhdellä, tehdään pyyntö palvelimelle missä Blazor tekee tarvittavat muutokset komponenttiin/komponentteihin ja palauttaa nämä takaisin käyttäjän selaimelle. Kaikki nämä muutokset tuodaan ja viedään SignalR-komponentin välityksellä. Blazor Server julkaistiin ASP<span>.NET Core 3.0 version mukana.

![Kuva](https://docs.microsoft.com/en-us/aspnet/core/blazor/index/_static/blazor-server.png?view=aspnetcore-3.0 "Tämä on kuva")

_Yllä olevassa kuvassa kuvattu Blazor Serverin toiminnallisuutta. Kuva on lainattu Microsoftin [Blazor-dokumentaatiosta](https://docs.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-3.1)._

Loppukäyttäjän selaimen tuen ja suorituskyvyn riippumattomuus tekee Blazor Serveristä vahvan valinnan isojenkin sovelluksien luontiin, sillä selaimelle ei tarvitse ladata kuin Blazorin luoma dynaaminen web-sovellus. Tällöin on myös käytössä täysi tuki .NET:n työkaluihin, eikä sovelluksen komponentteja/koodia tuoda käyttäjälle. Internetyhteyksien välinen viive voi toisaalta koitua hankalaksi, sillä käyttäjä ei välttämättä heti koe tapahtuvaa muutosta ja se voi mahdollisesti pilata käyttäjäkokemuksen.

[**Blazor Server**](https://docs.microsoft.com/en-us/aspnet/core/blazor/hosting-models?view=aspnetcore-3.1#blazor-server)

### SignalR

Microsoftin kehittämän SignalR-komponentin avulla Blazor Server pystyy kommunikoimaan selaimen kanssa, saaden tietoa tarvittavista käyttöliittymän muutoksista ja palauttaen pyyntöjen mukaisen tuloksen takaisin loppukäyttäjälle. SignalR hyödyntää HTML5:n [WebSocket](https://javascript.info/websocket) APIa toimiakseen reaaliajassa.

[**SignalR dokumentaatio**](https://docs.microsoft.com/en-us/aspnet/core/signalr/introduction?view=aspnetcore-3.1)

## Blazor WebAssembly

Blazor Wasm, eli Blazor WebAssembly, on uudempi hostausmalli, mikä käyttää nimensä mukaisesti [WebAssembly-teknologiaa](https://webassembly.org/) pyörittämään .NET-sovelluksia suoraan selaimessa. Palvelimelta käyttäjän selaimelle ladataan C#- ja Razor-tiedostoista koostuvat .NET assembly-tiedostot, sekä .NET-ajoympäristö, minkä avulla Blazor Wasm pystyy konfiguroimaan assembly-tiedostoista staattiset tiedostot sovelluksen ajoa varten. Tämän toimenpiteen jälkeen Blazor-sovellus toimii ilman erillisen .NET-palvelimen riippuvuutta. Blazor Wasm:n on tarkoitus julkaista ASP<span>.NET Core 3.1 version mukana, minkä arvioidaan kirjoitushetkellä julkaistavan toukokuussa 2020.

![Kuva](https://docs.microsoft.com/en-us/aspnet/core/blazor/index/_static/blazor-webassembly.png?view=aspnetcore-3.0, "Tämä on kuva")

_Yllä olevassa kuvassa on kuvattu Blazor WebAssemblyn toiminnallisuutta. Kuva on lainattu Microsoftin [Blazor-dokumentaatiosta](https://docs.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-3.1)._

Vaikka Blazor WebAssembly on vielä kehitysvaiheessa oleva vaihtoehto Blazor-sovellusten luontiin, on se todettu hyväksi vaihtoehdoksi Serverin rinnalle. Koska Blazor Wasm tuottaa julkaisuvaiheessa sovelluksesta staattisia tiedostoja, ei palvelimen tarvitse suoraan olla .NET-palvelin, vaan mikä tahansa palvelin tai sisällönjakotapa kelpaa. Kunhan selain tukee WebAssembly-teknologiaa ja sovellus on kevyt ladata selaimelle. (Tämä riippuu sovelluksen koosta. Buildattujen sovelluksien kokoa kehitetään vielä.) Viiveetön interaktiivisuus piristää mukavasti käyttäjäkokemusta, varsinkin jos sovellukseen sisällytetään mukaan myös PWA-mahdollisuudet. Sovelluksen latauskoon lisäksi täytyy ottaa myös huomioon, että WebAssemblyn kanssa Blazor käyttää käyttäjän laitteistoa, joten suorituskyky on tärkeässä asemassa. Myös kaikkia .NET:n ominaisuuksia ei pystytä vielä kirjoitushetkellä toteuttamaan.

[**Blazor WebAssembly**](https://docs.microsoft.com/en-us/aspnet/core/blazor/hosting-models?view=aspnetcore-3.1#blazor-webassembly)

### WebAssembly

WebAssembly on matalan tason binäärimuotokieli, minkä avulla korkean tason ohjelmointikielillä, kuten C:llä ja C++:lla, luotuja sovelluksia voidaan pyörittää selainympäristössä. Wasmin avulla pystytään luomaan optimoituja websovelluksia kielillä tai teknologioilla, joiden alkuperäinen tarkoitus on selainten ulkopuolella ja mihin JavaScript ei kykene suorituskyvyn tai muiden rajoitusten vuoksi. WebAssembly myös toimii JavaScriptin kanssa yhteistyössä. .NET hyödyntää tämän teknologian tarjoamia mahdollisuuksia kääntämään ja ajamaan Blazor Wasmin tiedostot natiivisti selainympäristössä ilman ylimääräisten lisäosien asentamista. WebAssembly on vapaata lähdekoodia ja [toimii kaikissa moderneissa selaimissa.](https://caniuse.com/#feat=wasm)

[**WebAssemblyn kotisivu**](https://webassembly.org/)

[**Lisätietoa WebAssemblystä**](https://blog.logrocket.com/webassembly-how-and-why-559b7f96cd71/)

[**WebAssembly:llä toimiva Raytracing-demo**](https://mtharrison.github.io/wasm-raytracer/)

[**WebAssembly-videoeditori**](https://d2jta7o2zej4pf.cloudfront.net/)

[**WebAssembly Editor**](https://mbebenita.github.io/WasmExplorer/) ja [**WebAssembly Studio(BETA)**](https://webassembly.studio/) - C ja C++ -kielten editorit selaimessa.

[**D3wasm**](https://wasm.continuation-labs.com/d3demo/) - Tech demo Doom 3:sta pyörimässä selainympäristössä

# Esimerkki

_Esimerkki on tehty käyttämällä Visual Studio Code-tekstieditoria. Jos käytät Visual Studio-ohjelmankehitysympäristöä, voit noudattaa [Microsoftin virallisia ohjeita](https://docs.microsoft.com/en-us/aspnet/core/blazor/get-started?view=aspnetcore-3.1&tabs=visual-studio). Oletuksena on, että olet tarkistanut [mitä tarvitset](#mitä-tarvitset)-kohdan huolella läpi._

Esimerkkiä varten luodaan uusi Blazor-projekti komennolla ```dotnet new blazorwasm -o {projektin nimi}```, mikä luo uuden projektin hakemistoineen päivineen Blazor-sovellukselle, käyttäen WebAssembly-mallia. Toimii myös Blazor Server-mallilla komennolla ```dotnet new blazorserver -o {projektin nimi}```. Voit testata luonnin onnistumisen siirtymällä projektin hakemistoon ja ajamalla sovellus komennolla ```dotnet run```. Uusi Blazor-sovellus pitäisi näyttää alla olevan kuvan mukaiselta ja se löytyy osoitteesta [http://localhost:5000/](http://localhost:5000/).

![](./Kuvat/blazor_newproject.png)

Jatketaan esimerkkiä lisäämällä siihen logiikkaa. Luodaan yksinkertainen valuutanvaihto-komponentti sovellukselle. Sovellus käyttää valmiiksi asennettua Bootstrap-tyylikehystä.

``` c#
<!-- CurrencyConverter.razor -komponentti -->

<h3>Eurot dollareiksi!</h3>

<div class="input-group">
    <div class="input-group-prepend">
        <span class="input-group-text" id="basic-addon1">€</span>
    </div>
    <input type="text" class="form-control" @bind=Euros>
</div>

<button type="button" @onclick=Convert class="btn btn-dark">Muuta!</button>

<div class="input-group mb-3">
    <div class="input-group-prepend">
        <span class="input-group-text" id="basic-addon1">$</span>
    </div>
    <input type="text" disabled class="form-control" @bind=Dollars>
</div>

@code {

    private double Euros { get; set; }
    private double Dollars { get; set; }

    private void Convert() 
    {
        Dollars = Euros * 1.44;
    }
}
```
Yllä luodussa CurrencyConverter-komponentissa logiikka toimii seuraavasti: Käyttäjä kirjoittaa muutettavan arvon ylempään ```<input>```-elementtiin, joka sisällyttää arvon ```@bind```-parametrin sisältävään muuttujaan ( _```@bind``` on Razor-komponentin [two-way data binding-ominaisuus](https://learn-blazor.com/pages/data-binding/)_ ). Tämän jälkeen kun käyttäjä painaa ```<button>```-painiketta, elementin sisältämä ```@onclick```-eventtiin bindattu ```Convert```-metodi kutsutaan. Dollariksi käännetty rahasumma annetaan toiselle muuttujalle, mikä on vuorostaan bindattu alempaan ```<input>```-elementtiin.

![](./Kuvat/blazor_convert.gif)

Komponentin lopputulos näyttää yllä olevan kuvan mukaiselta. Koodia pystyisi nyt käyttämään, kunhan siihen päästään käsiksi sovelluksen kautta. Kaksi vaihtoehtoa löytyy: joko komponentille asetetaan polku ```@page```-direktiivillä, tai sisällyttämällä se komponenttiin mistä löytyy jo kyseinen direktiivi.

``` html
<!-- Index.razor -komponentti. "/" merkitsee kyseisen sivukomponentin polkua, tässä tilanteessa toimien sovelluksen etusivuna. -->

@page "/"

<main>
    <h1>Blazor perusteet!</h1>

    <p>Sisällytetään vähän komponentteja!</p>

    <CurrencyConverter />
</main>
```

```<CurrencyConverter />``` elementti sisältää ylhäällä luodun valuutanvaihtokomponentin. Elementin nimi pitää täsmätä tarkkaan komponentin tiedostonimen kanssa ja tiedoston polku pitää löytyä _Imports-tiedostosta. Tämän jälkeen sovellusta voidaan nähdä jälleen ```dotnet run```-komennolla.

_Vinkki: komennolla ```dotnet watch run``` sovellus päivittyy automaattisesti ja muutoksia varten tarvitsee vain päivittää sivu. Näin vältetään jatkuvaa ```run```-komennon sulkemista ja ajamista._

![](./Kuvat/blazor_updated.png)

Komponentteihin voidaan myös sisällyttää parametreja, joiden avulla voidaan vaikuttaa komponentin logiikkaan isäntäkomponentista käsin. Jatketaan esimerkkiä siten, että lisätään mahdollisuus vaihtaa dollarit takaisin euroiksi alhaalla olevan gifin tavoin.

![](./Kuvat/blazor_choice.gif)

Ensimmäinen muutos tapahtuu CurrencyConverter-komponentissa, mihin käydään tekemään muutamia muutoksia.

``` c#
<!-- CurrencyConverter.razor -->
<h3>@ComponentTitle</h3>

<div class="input-group">
    <div class="input-group-prepend">
        <span class="input-group-text" id="basic-addon1">@(WhichCurrency == "euros" ? "€" : "$")</span>
    </div>
    <input type="text" class="form-control" @bind=Value>
</div>

<button type="button" @onclick=Convert class="btn btn-dark">Muuta!</button>

<div class="input-group">
    <div class="input-group-prepend">     
        <span class="input-group-text" id="basic-addon1">@(WhichCurrency == "euros" ? "$" : "€")</span>
    </div>
    <input type="text" disabled class="form-control" @bind=ChangedValue>
</div>

@code {

    [Parameter]
    public string WhichCurrency { get; set; }

    [Parameter]
    public string ComponentTitle { get; set; }
    
    private double Value { get; set; }
    private double ChangedValue { get; set; }

    private void Convert() {
        if(WhichCurrency == "euros") 
        {
            ChangedValue = Math.Round(Value * 1.44, 2);
        } else 
        {
            ChangedValue = Math.Round(Value * 0.71, 2);
        }
    }
}
```

Komponentin muutokset ovat seuraavat: Code-lohkoon on lisätty 2 uutta **julkista** komponenttia, ```WhichCurrency``` ja ```ComponentTitle``` ( _Huomioi myös muutokset alkuperäisiin muuttujiin ja funktioon_ ). Näille on annettu ```Component parameter```-määrittely ```[Parameter]```-ominaisuudella. Nyt näiden kahden muuttujan arvoihin pääsee käsiksi komponentin ulkopuolelta, mikä auttaa huomattavasti komponentin interaktiivisuuteen. HTML-kieleen on myös sisällytetty ```ComponentTitle```-muuttujalla bindattu otsikko ja [kolmiarvoinen ehtolauseke](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/conditional-operator#conditional-ref-expression), jolla tässä tilanteessa vain vaikutetaan oikean rahasymbolin renderöintiin ```@WhichCurrency```-muuttujan mukaan. Kyseinen lauseke pitää sisällyttää [Explicit Razor](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/conditional-operator#conditional-ref-expression)-lausekkeen sisään, jotta HTML-kielen sisällä voidaan renderöidä välejä vaativia C#-toimintojen tuloksia.

[**Implicit Razor expression**](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-3.1#implicit-razor-expressions) & [**Explicit Razor expression**](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-3.1#explicit-razor-expressions)

``` c#
<!-- Index.razor -->
@page "/"

<main>
    <h1>Blazor perusteet!</h1>

    <p>
        <button type="button" @onclick=@(() => Change(0)) class="btn btn-dark">Eurot</button>
        <button type="button" @onclick=@(() => Change(1)) class="btn btn-info">Dollarit</button>
    </p>

    <CurrencyConverter WhichCurrency=@Value ComponentTitle=@Title />
</main>

@code {
    private string Value = "euros";
    private string Title = "Eurot dollareiksi!";

    private void Change(int x) 
    {
        if(x == 0) 
        {
            Value = "euros";
            Title = "Eurot dollareiksi!";
        } else 
        {
            Value = "dollars";
            Title = "Dollarit euroiksi!";
        }
    }
}
```

Index-komponenttiin tehdyt muutokset: ```<CurrencyConverter />```-elementille on annettu nyt komponentin parametreihin arvot Index-komponentin omista muuttujista. Muuttujat saavat arvonsa painikkeiden ```@onclick```-eventtien sisällyttämien ```Change```-metodin tuloksesta. Jos eventtiin bindattuun metodiin tarvitaan parametreja, bindaukseen tarvitaan .NET:n [Lambda-lauseketta](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions). Näiden muutosten jälkeen valutaanvaihto molempiin suuntiin pitäisi toimia, kuten esimerkissä.

Ylemmässä esimerkissä opit data- ja event binding-ominaisuuksista, komponenttien sisällyttämisestä isäntäkomponentteihin, reitityksestä, Razor-syntaksin perusteita ja ehkä myös itse C#-koodia.

# Tehtävä

Luo esimerkin neuvoja käyttäen yksinkertainen Todo-sovellus. Voit luoda uuden Blazor-sovelluksen tai käyttää valmista pohjaa [Esimerkki](https://github.com/Miibotin/websk_blazor/tree/master/Esimerkki)-kansiosta. Sovelluksen logiikka täytyy olla omalla sivullaan, tai sitten etusivulla komponentista tuotuna. Varmista että sinulla on kaikki [mitä tarvitset](#mitä-tarvitset) Blazor-sovelluksen tekoa varten. Sovellusta varten sinun täytyy luoda olioluokka ja siitä taulukko. Valmista pohjaa voi käyttää esimerkkinä ja työ voi näyttää esimerkiksi [tältä](https://miibotin.github.io/blazor_page/). Kun työ on valmis, zippaa ja palauta.

Mikäli C# ei ole entuudestaan tuttu, voit saada hyödyllisiä vinkkejä [täältä](https://docs.microsoft.com/en-us/dotnet/csharp/tutorials/intro-to-csharp/).

**EXTRA**

Upota sovelluksen juureen oma JavaScript-tiedosto, minkä sisällä oleva funktio tekee jotain sovellukselle. Alert-laatikon esilletuonti on yksi hyvä esimerkki. Käytä [JavaScript Interop](#javascript-interop-1)-ominaisuutta kutsuaksesi tätä funktiota.

Jos teet Todo-logiikan omalle sivulle, tulet tutuksi myös ulkoasukomponenttien kanssa. Luo hieno ulkoasu samalla, kun laitat linkin navigaatiopalkkiin.
