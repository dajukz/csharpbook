# Zelf exceptions opwerpen

Je kan ook in je eigen code uitzonderingen ‘opgooien’, zodat deze elders opgevangen worden. Je kan hierbij zelf exceptions maken (zie volgende hoofdstukje) of gewoon gebruik maken van een bestaande Exception-klasse.

Een voorbeeld:

```csharp
static int DoeIets(int getal)
{
    if (getal == 0)
        throw new DivideByZeroException("Getal equals 0.You shouldn't do that!");
    else
        return 100 / getal;
}
 
 
static void Main(string[] args)
{
    try
    {
        Console.WriteLine(DoeIets(0));
    }
    catch(Exception e)
    {
        Console.WriteLine(e.Message);
    }
}
```

De uitvoer zal zijn:

![](../assets/20_exceptions/eigenex.png)

De lijn ``throw new DivideByZeroException("Getal equals 0.You shouldn't do that!");`` zorgt er dus voor dat we een eigen boodschap 'verpakken'

> Merk op dat het zelden aangeraden is om je foutboodschappen te hardcoden in je moedertaal.

# Een eigen exception ontwerpen

Je kan ook eigen klassen afleiden van Exception zodat je eigen uitzonderingen kan maken en gooien in je programma. Je maakt hiervoor gewoon een nieuwe klasse aan die je laat overerven van de Exception-klasse. Een voorbeeld:

```csharp
class MyException: Exception
{
    public override string ToString()
    {
        string extrainfo = "Exception Generated by Tim Dams:\n";
        return extrainfo+base.ToString();
    }
}
```

Om deze exception nu zelf op te ‘gooien’ gebruiken we het keyword `throw`. In volgende voorbeeld gooien we onze eigen exception op een bepaald punt in de code en vangen deze dan op (de reden van de exception moet je zelf verzinnen, het is maar een onnozel voorbeeld):

```csharp
static void Main(string[] args)
{
    try
    {
        TimsMethod();
    }
 
    catch (Exception e)
    {
       Console.WriteLine(e.ToString());
    }     
}
static public void TimsMethod()
{
    //do stuff
    //when suddenly: an exception! 
    MyException exp = new MyException();
    throw exp;
}
```

![](../assets/20_exceptions/myex.png)
