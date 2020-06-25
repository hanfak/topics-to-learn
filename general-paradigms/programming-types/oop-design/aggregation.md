# Aggregation

An aggregation describes a relationship in which one object belongs to another object, but they are still potentially independent. The first object does not control the lifecycle of the second.

This kind of relationship is usually described as has-a (or is-part-of), or on the inverse belongs-to. In our example the object Winners of Team has-a John of Player, or on the inverse John belongs-to Winners.

```java
class Team
{
    Player[50] TeamMembers

    Fire(Player dude)
    {
         TeamMembers.Remove(dude)
    }

    Hire(Player dude)
    {
         TeamMembers.Add(dude)
    }
}

Team Winners = new Team
Team Mediocre = new Team
Player John = new Player

Winners.Hire(John)
// time passes
Winners.Fire(John)
Mediocre.Hire(John)
```
