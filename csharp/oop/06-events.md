# Events


```csharp

class Program
{
  static void Main()
  {

    var room = new Room(3);
    room.RoomSoldOutEvent += OnRoomSoldOut;
    room.ReserveSeat();
    room.ReserveSeat();
    room.ReserveSeat();
    room.ReserveSeat();
    room.ReserveSeat();
    room.ReserveSeat();

  }

  static void OnRoomSoldOut()
  {
    Console.WriteLine("Sala lotada");
    
  }

}


class Room
{
  public Room(int seats)
  {
    Seats = seats;
    seatsInuse = 0;
  }

  public int Seats { get; set; }

  private int seatsInuse = 0;

  public void ReserveSeat()
  {
    seatsInuse++;
    if(seatsInuse >= Seats)
    {
      OnRoomSoldOut(EventArgs.Empty)
      // Evento fechado
    } else {
      // Assento reservado
    }
  }

  // Criando um evento que irá ocorrer quando o assentos se esgotarem.
  public event EventHandler RoomSoldOutEvent; // definição do evento

  protected virtual void OnRoomSoldOut(EventArgs e) // execução do evento
  {
    EventHandler handler = RoomSoldOutEvent; // Instaciando o manipulador de evento
    handler?.Invoke(this, e); // o manipulador vai invocar este método
  }
}
```