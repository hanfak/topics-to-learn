# Strategy Pattern

The Strategy pattern encapsulates a set of related algorithms into individual classes and makes them interchangeable with each other.
- client code can choose which algorithm to use without needing to know the internal details of how each one works.

Instead of checking an enum or some type that is passed in to a method and a case/switch statement to decide what algorithm to perform, can now new up an object with the type which then decides what algorithm to perform hence not need to change the calling code (OCP)

We choose the strategy at runtime, when we new up the dependencies in the constructor args. OR when we run the method.
## Example

Old

```java
public enum SimulationMethod {
  Quick, Complex
}

public class StockSimulatorUsingSwitch {
  public double SimulateNetGainOrLoss(string nasdaqCode, SimulationMethod method) {
    switch (method) {
      case SimulationMethod.Quick:
        return 0;
      case SimulationMethod.Complex:
        return 1;
      default:
        throw new ArgumentOutOfRangeException("method");
    }
  }
}

StockSimulatorUsingSwitch s = new StockSimulatorUsingSwitch();
doublce simulatedValue = s.SimulateNetGainOrLoss("XXXX",
                                             SimulationMethod.Quick);
```

After pattern implemented

```java
public interface IStockSimulation {
  doublce SimulateNetGainOrLoss(string nasdaqCode);
}

public class QuickSimulation implements IStockSimulation {
  public double SimulateNetGainOrLoss(string nasdaqCode) {
    return 0;
  }
}

public class ComplexSimulation implements IStockSimulation {
  public double SimulateNetGainOrLoss(string nasdaqCode) {
    return 1;
  }
}

public class StockSimulatorUsingStrategy {
  public double SimulateNetGainOrLoss(string nasdaqCode, IStockSimulation simulator) {
    return simulator.SimulateNetGainOrLoss(nasdaqCode);
  }
}

StockSimulatorUsingStrategy s=new StockSimulatorUsingStrategy();
double simulatedValue=s.SimulateNetGainOrLoss("XXXX", new QuickSimulation());
```

Can pass the IStockSimulation as a method param, or even via the constructor
