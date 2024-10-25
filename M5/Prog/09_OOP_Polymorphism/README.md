# PROG les 9: OOP Polymorfisme / Polymorphism

Polymorfisme is een van de vier pijlers van Objectgeoriënteerd Programmeren (OOP), samen met Encapsulatie, Overerving en Abstractie. Het maakt het mogelijk om objecten van verschillende typen te behandelen als objecten van een gemeenschappelijk basistype.

Stel je een game voor met verschillende personages, zoals krijgers, magiërs en boogschutters. Elk personage kan op een andere manier "aanvallen", maar ze delen allemaal dezelfde actie: "Aanvallen".

Voor elk type komt er dus een andere code-"implementatie" van de aanval.

![attacks](../src/09_01_attacks.png)

Om dit te doen gebruik je overerving en de keywords **virtual** en **override**.

```
public class Character : MonoBehaviour
{
    public virtual void Attack()
    {
        Debug.Log("Character valt aan");
    }

}
```

Je baseclass / parent class heeft een methode die **virtual** is. En dus overschreven kan worden.

```
public class Warrior : Character
{
    public override void Attack()
    {
        Debug.Log("Krijger zwaait met een zwaard!");
    }
}
```

Net als bij abstraction gebruik je het **override** keyword om de daadwerkelijke implementatie van de code uit te voeren.

```
public class Mage : Character
{
    public override void Attack()
    {
        Debug.Log("Magiër werpt een vuurbal!");
    }
}
```
