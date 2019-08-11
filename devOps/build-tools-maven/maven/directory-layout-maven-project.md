# Directory layout

Maven projects have a common directory layout

NOTE: Use `tree` in command line to see this output below

This is from the project I have worked on

```
.
├── README.md
├── poker-game.iml
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── hanfak
│   │   │           ├── domain
│   │   │           │   ├── cards
│   │   │           │   │   ├── Card.java
│   │   │           │   │   ├── Rank.java
│   │   │           │   │   └── Suit.java
│   │   │           │   ├── deck
│   │   │           │   │   ├── CardDealer.java
│   │   │           │   │   ├── CardShuffler.java
│   │   │           │   │   ├── DealtCards.java
│   │   │           │   │   └── Deck.java
│   │   │           │   └── game
│   │   │           │       ├── Player.java
│   │   └── resources
│   └── test
│       └── java
│           ├── acceptancetests
│           │   └── versionone
│           │       ├── BestHandIsAFlushInFiveCardHandTest.java
│           └── com
│               └── hanfak
│                   └── domain
│                       ├── cards
│                       │   ├── CardTest.java
│                       │   └── DeckTest.java
│                       └── deck
│                           ├── CardDealerTest.java
│                           └── DealtCardsTest.java
└── target
    ├── classes
    │   └── com
    │       └── hanfak
    │           ├── domain
    │           │   ├── cards

```

NOTE: `poker-game.iml` is just an intellij file and not really needed

Things to notice:

- All code is in the `src`
- pom.xml is outside of the src directory
- Application source(ie main) and Test source(ie test) are separated
- A separate folder called `target` where all the compiled files are stored
- A resourcse folder for files such as property files
