# Abstract Factory Example

Цей репозиторій містить приклад патерну проектування "Абстрактна фабрика".

## Абстрактна фабрика (Abstract Factory)

Абстрактна фабрика надає інтерфейс для створення родин взаємозалежних або пов'язаних об'єктів без необхідності вказувати їх конкретні типи.

### Приклад коду:

```csharp
// Abstract Product A
public interface IChair
{
    void SitOn();
}

// Abstract Product B
public interface ISofa
{
    void LieOn();
}

// Concrete Product A1
public class VictorianChair : IChair
{
    public void SitOn()
    {
        Console.WriteLine("Sitting on a Victorian chair.");
    }
}

// Concrete Product B1
public class VictorianSofa : ISofa
{
    public void LieOn()
    {
        Console.WriteLine("Lying on a Victorian sofa.");
    }
}

// Concrete Product A2
public class ModernChair : IChair
{
    public void SitOn()
    {
        Console.WriteLine("Sitting on a Modern chair.");
    }
}

// Concrete Product B2
public class ModernSofa : ISofa
{
    public void LieOn()
    {
        Console.WriteLine("Lying on a Modern sofa.");
    }
}

// Abstract Factory
public interface IFurnitureFactory
{
    IChair CreateChair();
    ISofa CreateSofa();
}

// Concrete Factory 1
public class VictorianFurnitureFactory : IFurnitureFactory
{
    public IChair CreateChair()
    {
        return new VictorianChair();
    }

    public ISofa CreateSofa()
    {
        return new VictorianSofa();
    }
}

// Concrete Factory 2
public class ModernFurnitureFactory : IFurnitureFactory
{
    public IChair CreateChair()
    {
        return new ModernChair();
    }

    public ISofa CreateSofa()
    {
        return new ModernSofa();
    }
}

// Client code
public class FurnitureStore
{
    private readonly IChair _chair;
    private readonly ISofa _sofa;

    public FurnitureStore(IFurnitureFactory factory)
    {
        _chair = factory.CreateChair();
        _sofa = factory.CreateSofa();
    }

    public void Furnish()
    {
        _chair.SitOn();
        _sofa.LieOn();
    }
}

class Program
{
    static void Main(string[] args)
    {
        IFurnitureFactory victorianFactory = new VictorianFurnitureFactory();
        FurnitureStore victorianStore = new FurnitureStore(victorianFactory);
        victorianStore.Furnish();

        IFurnitureFactory modernFactory = new ModernFurnitureFactory();
        FurnitureStore modernStore = new FurnitureStore(modernFactory);
        modernStore.Furnish();
    }
}
