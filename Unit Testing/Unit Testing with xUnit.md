# xUnit

The xUnit framework in .NET is a widely used unit testing framework that helps developers write tests for their applications.

Used for unit testing which is a strategy of functional testing.

## How to add an xUnit project

![image](https://github.com/user-attachments/assets/7d46ffab-f02a-47c9-a6f3-cb0fdba6d365)

![image](https://github.com/user-attachments/assets/a413ef47-464a-464d-9b85-923b5feb6d2f)

![image](https://github.com/user-attachments/assets/6b8b5812-8602-45ba-ad51-f265242a3108)

Then set it up for the project you want to test on

## Writing unit test classes

Assume we have this class

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Runtime.CompilerServices;

namespace GameEngine
{
    public class PlayerCharacter : INotifyPropertyChanged
    {
        private int _health = 100;
        
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public string FullName => $"{FirstName} {LastName}";
        public string Nickname { get; set; }
        public int Health
        {
            get => _health;
            set
            {
                _health = value; 
                OnPropertyChanged();
            }
        }
        public bool IsNoob { get; set; }
        public List<string> Weapons { get; set; }

        public event EventHandler<EventArgs> PlayerSlept;

        public PlayerCharacter()
        {
            FirstName = GenerateRandomFirstName();

            IsNoob = true;

            CreateStartingWeapons();
        }

        public void Sleep()
        {           
            var healthIncrease = CalculateHealthIncrease();            

            Health += healthIncrease;

            OnPlayerSlept(EventArgs.Empty);
        }

        private int CalculateHealthIncrease()
        {
            var rnd = new Random();

            return rnd.Next(1, 101);            
        }

        
        protected virtual void OnPlayerSlept(EventArgs e)
        {
            PlayerSlept?.Invoke(this, e);
        }

        public void TakeDamage(int damage)
        {
            Health = Math.Max(1, Health -= damage);
        }

        private string GenerateRandomFirstName()
        {
            var possibleRandomStartingNames = new[]
            {
                "Danieth",
                "Derick",
                "Shalnorr",
                "G'Toth'lop",
                "Boldrakteethtop"
            };

            return possibleRandomStartingNames[
                new Random().Next(0, possibleRandomStartingNames.Length)];
        }

        private void CreateStartingWeapons()
        {
            Weapons = new List<string>
            {
                "Long Bow",
                "Short Bow",
                "Short Sword",
                //""
                //"Staff Of Wonder",
            };
        }
    }
}
```

To test it, we can write a testing class in the xUnit project and name it ClassNameShould for naming convention.

To write unit tests, we can simpply create a method, add the **Fact** data attribute to declare it as a testing method, and then follow the AAA (Arrange, Act, Assert) testing pattern:

- Arrange: Set up the conditions, objects, and any required data for the test.
- Act: Perform the action that you want to test, usually calling a method.
- Assert: Verify that the result or behavior matches the expected outcome.

```csharp
using System;
using Xunit;

namespace GameEngine.Tests
{
    public class PlayerCharacterShould
    {
        [Fact]
        public void BeInexperiencedWhenNew()
        {
            PlayerCharacter sut = new PlayerCharacter();

            Assert.True(sut.IsNoob);
        }
    }
}
```

## Testing strings

```csharp
  [Fact]
  public void CalculateFullName()
  {
      PlayerCharacter sut = new PlayerCharacter();

      sut.FirstName = "Sarah";
      sut.LastName = "Smith";

      Assert.Equal("Sarah Smith", sut.FullName);
  }

  [Fact]
  public void HaveFullNameStartingWithFirstName()
  {
      PlayerCharacter sut = new PlayerCharacter();

      sut.FirstName = "Sarah";
      sut.LastName = "Smith";

      Assert.StartsWith("Sarah", sut.FullName);
  }

  [Fact]
  public void HaveFullNameEndingWithLastName()
  {
      PlayerCharacter sut = new PlayerCharacter();

      sut.LastName = "Smith";

      Assert.EndsWith("Smith", sut.FullName);
  }

  [Fact]
  public void CalculateFullName_IgnoreCaseAssertExample()
  {
      PlayerCharacter sut = new PlayerCharacter();

      sut.FirstName = "SARAH";
      sut.LastName = "SMITH";

      Assert.Equal("Sarah Smith", sut.FullName, ignoreCase: true);
  }

  [Fact]
  public void CalculateFullName_SubstringAssertExample()
  {
      PlayerCharacter sut = new PlayerCharacter();

      sut.FirstName = "Sarah";
      sut.LastName = "Smith";

      Assert.Contains("ah Sm", sut.FullName);
  }


  [Fact]
  public void CalculateFullNameWithTitleCase()
  {
      PlayerCharacter sut = new PlayerCharacter();

      sut.FirstName = "Sarah";
      sut.LastName = "Smith";

      Assert.Matches("[A-Z]{1}[a-z]+ [A-Z]{1}[a-z]+", sut.FullName);
  }
```

## Testing neumerics

```csharp
[Fact]
public void StartWithDefaultHealth()
{
    PlayerCharacter sut = new PlayerCharacter();

    Assert.Equal(100, sut.Health);
}

[Fact]
public void StartWithDefaultHealth_NotEqualExample()
{
    PlayerCharacter sut = new PlayerCharacter();

    Assert.NotEqual(0, sut.Health);
}

[Fact]
public void IncreaseHealthAfterSleeping()
{
    PlayerCharacter sut = new PlayerCharacter();

    sut.Sleep(); // Expect increase between 1 to 100 inclusive

    //Assert.True(sut.Health >= 101 && sut.Health <= 200);
    Assert.InRange(sut.Health, 101, 200);
}
```

## Testing Null

```csharp
[Fact]
public void NotHaveNickNameByDefault()
{
    PlayerCharacter sut = new PlayerCharacter();

    Assert.Null(sut.Nickname);
}
```

## Testing Collections

```csharp
[Fact]
public void HaveALongBow()
{
    PlayerCharacter sut = new PlayerCharacter();

    Assert.Contains("Long Bow", sut.Weapons);
}

[Fact]
public void NotHaveAStaffOfWonder()
{
    PlayerCharacter sut = new PlayerCharacter();

    Assert.DoesNotContain("Staff Of Wonder", sut.Weapons);
}

[Fact]
public void HaveAtLeastOneKindOfSword()
{
    PlayerCharacter sut = new PlayerCharacter();

    Assert.Contains(sut.Weapons, weapon => weapon.Contains("Sword"));
}

[Fact]
public void HaveAllExpectedWeapons()
{
    PlayerCharacter sut = new PlayerCharacter();

    var expectedWeapons = new[]
    {
        "Long Bow",
        "Short Bow",
        "Short Sword"
    };

    Assert.Equal(expectedWeapons, sut.Weapons);
}

[Fact]
public void HaveNoEmptyDefaultWeapons()
{
    PlayerCharacter sut = new PlayerCharacter();

    Assert.All(sut.Weapons, weapon => Assert.False(string.IsNullOrWhiteSpace(weapon)));
}
```

## Testing reference types

```csharp
[Fact]
public void CreateNormalEnemyByDefault()
{
    EnemyFactory sut = new EnemyFactory();

    Enemy enemy = sut.Create("Zombie");

    Assert.IsType<NormalEnemy>(enemy);
}

[Fact]
public void CreateNormalEnemyByDefault_NotTypeExample()
{
    EnemyFactory sut = new EnemyFactory();

    Enemy enemy = sut.Create("Zombie");

    Assert.IsNotType<DateTime>(enemy);
}

[Fact]
public void CreateBossEnemy()
{
    EnemyFactory sut = new EnemyFactory();

    Enemy enemy = sut.Create("Zombie King", true);

    Assert.IsType<BossEnemy>(enemy);
}

[Fact]
public void CreateBossEnemy_CastReturnedTypeExample()
{
    EnemyFactory sut = new EnemyFactory();

    Enemy enemy = sut.Create("Zombie King", true);

    // Assert and get cast result
    BossEnemy boss = Assert.IsType<BossEnemy>(enemy);

    // Additional asserts on typed object
    Assert.Equal("Zombie King", boss.Name);
}

[Fact]
public void CreateBossEnemy_AssertAssignableTypes()
{
    EnemyFactory sut = new EnemyFactory();

    Enemy enemy = sut.Create("Zombie King", true);

    //Assert.IsType<Enemy>(enemy);
    Assert.IsAssignableFrom<Enemy>(enemy);
}

[Fact]
public void CreateSeparateInstances()
{
    EnemyFactory sut = new EnemyFactory();

    Enemy enemy1 = sut.Create("Zombie");
    Enemy enemy2 = sut.Create("Zombie");

    Assert.NotSame(enemy1, enemy2);
}
```

## Testing exception

```csharp
[Fact]
public void NotAllowNullName()
{
    EnemyFactory sut = new EnemyFactory();

    // Assert.Throws<ArgumentNullException>(() => sut.Create(null));
    Assert.Throws<ArgumentNullException>("name", () => sut.Create(null));
}

[Fact]
public void OnlyAllowKingOrQueenBossEnemies()
{
    EnemyFactory sut = new EnemyFactory();

    EnemyCreationException ex =
        Assert.Throws<EnemyCreationException>(() => sut.Create("Zombie", true));

    Assert.Equal("Zombie", ex.RequestedEnemyName);
}
```
## Running unit tests

![image](https://github.com/user-attachments/assets/eb6aeace-5f63-408b-885d-fb46879cbb4b)

![image](https://github.com/user-attachments/assets/62b4cb82-70b7-4c0e-ad18-b7c7e0c40e08)

# Data driven testing

Data-driven testing in xUnit for C# is a technique where you run the same test multiple times with different sets of input data. This allows you to test your code with various inputs without writing redundant code. I

## Inline data

```csharp
using Xunit;

public class CalculatorTests
{
    [Theory]
    [InlineData(2, 3, 5)]
    [InlineData(0, 0, 0)]
    [InlineData(-1, -1, -2)]
    public void Add_ShouldReturnCorrectSum(int num1, int num2, int expected)
    {
        // Arrange
        var calculator = new Calculator();

        // Act
        var result = calculator.Add(num1, num2);

        // Assert
        Assert.Equal(expected, result);
    }
}

public class Calculator
{
    public int Add(int a, int b) => a + b;
}
```

```csharp
using Xunit;
using System.Collections.Generic;

public class CalculatorTests
{
    public static IEnumerable<object[]> GetData()
    {
        return new List<object[]>
        {
            new object[] { 2, 3, 5 },
            new object[] { 10, 20, 30 },
            new object[] { -5, 5, 0 }
        };
    }

    [Theory]
    [MemberData(nameof(GetData))]
    public void Add_ShouldReturnCorrectSum(int num1, int num2, int expected)
    {
        // Arrange
        var calculator = new Calculator();

        // Act
        var result = calculator.Add(num1, num2);

        // Assert
        Assert.Equal(expected, result);
    }
}

public class Calculator
{
    public int Add(int a, int b) => a + b;
}
```

# Categorizing Tests

In xUnit, Traits are a way to organize and categorize tests based on custom attributes. They are useful when you want to run or group specific sets of tests

```csharp
using Xunit;

public class CalculatorTests
{
    [Fact]
    [Trait("Category", "Unit")]
    public void Add_ShouldReturnCorrectSum()
    {
        // Arrange
        var calculator = new Calculator();
        int num1 = 2;
        int num2 = 3;

        // Act
        var result = calculator.Add(num1, num2);

        // Assert
        Assert.Equal(5, result);
    }

    [Fact]
    [Trait("Category", "Integration")]
    public void Subtract_ShouldReturnCorrectDifference()
    {
        // Arrange
        var calculator = new Calculator();
        int num1 = 5;
        int num2 = 3;

        // Act
        var result = calculator.Subtract(num1, num2);

        // Assert
        Assert.Equal(2, result);
    }
}

public class Calculator
{
    public int Add(int a, int b) => a + b;
    public int Subtract(int a, int b) => a - b;
}
```

Categorizing tests in more than one category

```csharp

[Fact]
[Trait("Speed", "Slow")]
[Trait("Component", "Billing")]
public void BillingProcess_ShouldTakeLessThan5Seconds()
{
    // Test logic for billing process
}

```
