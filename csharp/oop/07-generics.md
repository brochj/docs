# Generics

```csharp

static void Main(string[] args)
{

  //consigo usar o método Save(), passando diferentes tipos Complexos

  var context = new DataContext<Person>(); // É como se pudessmos escolher o Tipo no momento da criação,
  context.Save(new Person()); //OK
  context.Save(new Payment()); // Não aceita, pois context só vai aceitar tipo Person

  var context1 = new DataContext<Payment>();
  context1.Save(new Payment());

  var context2 = new DataContext<Subscription>();
  context2.Save(new Subscription());
}


class DataContext<T> // classe generica
{
  public void Save(T entity) // recebe o Tipo genérico
  {
    // Exemplo: salvar no banco de dados

    // Não posso
  }
}

class Person {}

class Payment {}

class Subscription {}
```

Posso ter vários tipos genericos em uma mesma classe

```csharp

static void Main(string[] args)
{

  var context = new DataContext<Person, Payment, Subscription>(); // É como se pudessmos escolher o Tipo no momento da criação,
  context.Save(new Person());
  context1.Save(new Payment());
  context2.Save(new Subscription());
}


class DataContext<T, U, V> // Posso ter vários tipos genericos
{
  public void Save(T entity) {}
}

class Person {}

class Payment {}

class Subscription {}
```

## Limitando os tipos genéricos (where)

```csharp

static void Main(string[] args)
{

  var context = new DataContext<Person, Payment, Subscription>(); // Aceita
  // var context = new DataContext<Subscription, Payment, Person>(); // ERRO
  context.Save(new Person());
  context.Save(new Payment());
  context.Save(new Subscription());
}


class DataContext<P, PA, S> // Posso ter vários tipos genericos
  where P : Person
  where PA : Payment
  where S : Subscription
{
  public void Save(P entity) {}
  public void Save(PA entity) {}
  public void Save(S entity) {}
}

class Person {}

class Payment {}

class Subscription {}
```

## Posso usar com interface tipos genéricos

```csharp

static void Main(string[] args)
{

  var context = new DataContext<IPerson, IPayment, ISubscription>(); // Aceita
  // var context = new DataContext<Subscription, Payment, Person>(); // ERRO
  context.Save(new Person());
  context.Save(new Payment());
  context.Save(new Subscription());
}


class DataContext<P, PA, S> // Posso ter vários tipos genericos
  where P : IPerson
  where PA : IPayment
  where S : ISubscription
{
  public void Save(P entity) {}
  public void Save(PA entity) {}
  public void Save(S entity) {}
}

class Person : IPerson {}

class Payment : IPayment {}

class Subscription : ISubscription {}

interface IPerson {}

interface IPayment {}

interface ISubscription {}
```
