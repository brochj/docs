# Datetime

- `Datetime` é um `struct`


## Data padrão

```csharp
var data = new DateTime();
// 1/1/0001 12:00:00 AM
```

## Data atual

```csharp
var data = DateTime.Now;
// 4/5/2022 11:00:00 AM
```

## Criar uma Data

```csharp
var data = new DateTime(2022, 10, 25, 8, 21, 14);
// 10/25/2022 8:21:14 AM
```

## Acessar uma Data

```csharp
var data = new DateTime(2022, 10, 25, 8, 21, 14);
Console.WriteLine(data.Year);
Console.WriteLine(data.Month);
Console.WriteLine(data.Day);
Console.WriteLine(data.Hour);
Console.WriteLine(data.Minute);
Console.WriteLine(data.Second);

Console.WriteLine(data.DayOfweek);
Console.WriteLine((int)data.DayOfweek);

Console.WriteLine(data.DayOfYear);
```

## Formatação de Datas

```csharp
var data = DateTime.Now;

var formatted = String.Format("{0:yyyy}", data); // 2022
var formatted = String.Format("{0:yyy}", data);  // 2022
var formatted = String.Format("{0:yy}", data);   // 22
var formatted = String.Format("{0:y}", data);    // May 2022

var formatted = String.Format("{0:M}", data);    // May "day"
var formatted = String.Format("{0:mm}", data);    // 05

var formatted = String.Format("{0:yyyy-MM-dd}", data); // 2022-05-04
var formatted = String.Format("{0:dd/MM/yyyy}", data); // 04/05/2022

var formatted = String.Format("{0:s}", data); //
var formatted = String.Format("{0:u}", data); //
var formatted = String.Format("{0:r}", data); //

Console.WriteLine(formatted)
```

## Adicionar ou remover data

```csharp
var data = DateTime.Now;
Console.WriteLine(data);

data.AddDays(12)
data.AddDays(-14)
data.AddMonths(-9)
data.AddYears(6)
data.AddHours(6)
```

## Comparando Datas

Como inicializar um data como `null`
```csharp
Datetime? data = null
```

```csharp
var data = DateTime.Now;

if (data.Date == DateTime.now.Date) 
{
  Console.WriteLine("é igual")
}
```
## Localização

```csharp
using System.Globalization;

var pt = new CultureInfo("pt-BR");
var de = new CultureInfo("de-DE");
var current = CultureInfo.CurrentCulture;

// Essas duas linhas sao iguais.
Console.WriteLine(DateTime.Now.toString("d"))
Console.WriteLine(string.Format("{0:d}", DateTime.Now))

Console.WriteLine(DateTime.Now.toString("D", pt))
Console.WriteLine(string.Format("{0:d}", DateTime.Now))
```     

## Timezones (RECOMENDADO SEMPRE)

```csharp
var utcDate = DateTime.UtcNow;

// Convertendo a data para horario (culture) da maquina
var localTime = utcDate.ToLocalTime(); // horario (culture) da maquina

// Convertendo a data para horario (culture) especifico
var timezoneAustralia = TimeZoneInfo.FindSystemTimeZoneById("Pacific/Auckland");
var horaAustralia = TimeZoneInfo.ConvertTimeFromUtc(utcDate, timezoneAustralia);

```

## Timespan

Usar quando for realizar operacoes entre HORARIOS
- Exemplo: entrada e saida de funcionarios

```csharp
var timeSpan = new TimeSpan(); // 00:00:00

var timeSpanNanoSegundos = new TimeSpan(1); // 00:00:00.0000001 

var timeSpanHoraMinSeg = new TimeSpan(5, 12, 8); // 05:12:08
 

```

```csharp
Console.WritelLine(timeSpanHoraMinutoSegundo - timeSpanDiaHoraMinutoSegundo);
Console.Writeline(timeSpanDiaHoraMinutoSegundo.Days);
Console.WriteLine(timeSpanDiaHoraMinutoSegundo.Add(new TimeSpan (12, 0, 0)));
```