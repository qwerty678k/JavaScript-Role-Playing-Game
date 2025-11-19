PROJECT TITLE: DRAGON REPELLER RPG

OVERVIEW
Dragon Repeller is an interactive web application that places the user in a procedurally generated combat environment. Players must navigate a fictional economy, manage scarce resources (Gold, Health), and strategically upgrade their inventory to defeat a Dragon boss.

Unlike simple static webpages, this project functions as a "Single Page Application" (SPA). It relies on a custom-built engine to handle state transitions without page reloads, utilizing the Document Object Model (DOM) to render real-time updates based on user actions. The architecture prioritizes a data-driven approach, separating the game content (locations, dialogue) from the core logic engine, ensuring scalability and cleaner code structure.


KEY FEATURES
The application features a robust set of mechanics implemented in Vanilla JavaScript:

State-Driven Navigation: A centralized update() function acts as a Finite State Machine (FSM), seamlessly transitioning the interface between the "Town," "Store," and "Combat" modes based on an array of location objects.

Algorithmic Combat System: Combat outcomes are not pre-determined. The game utilizes a stochastic formula (Level * 5) - (Math.random() * XP) to calculate damage, balancing player progression (XP) against monster difficulty.

Dynamic Inventory Management: An array-based inventory system allows for the acquisition and tracking of multiple weapon types (push operations), gating player progress based on current assets.

Reactive UI Dashboard: The #stats panel updates instantaneously to reflect changes in Health, Gold, and XP, utilizing efficient DOM targeting strategies.

Retro Aesthetic: A custom CSS implementation utilizing high-contrast colors (#0a0a23) and fixed-width layouts to emulate handheld gaming consoles.


TECHNOLOGIES & ARCHITECTURE
This project was built to demonstrate mastery of the core web stack without reliance on external frameworks.

+--------------+------------------+---------------------------------------------+
| Component | Technology | Role in Architecture |
+--------------+------------------+---------------------------------------------+
| Structure | HTML5 | Semantic container layout using #game and |
| | | #controls divisions. |
+--------------+------------------+---------------------------------------------+
| Presentation | CSS3 | Flexbox alignment, Box Model constraints, |
| | | and "Dark Mode" styling. |
+--------------+------------------+---------------------------------------------+
| Logic | JavaScript (ES6+)| Game loop, event handling, and state |
| | | variable management. |
+--------------+------------------+---------------------------------------------+

Code Highlight: Data-Driven Locations
Instead of hard-coding if/else chains for every room, the game uses an extensible array of objects. This allows new levels to be added simply by defining data, not writing new logic.


const locations = [
    {
        name: "town square",
        "button text": ["Go to store", "Go to cave", "Fight dragon"],
        "button functions":,
        text: "You are in the town square. You see a sign that says \"Store\"."
    },
    // New locations can be added here without breaking the engine
];


GETTING STARTED
The project requires no build tools or package managers (npm/yarn), emphasizing the power of native browser technologies.

Prerequisites:
A modern web browser (Chrome, Firefox, Safari, Edge).
A text editor (VS Code) if you wish to modify the source.

Installation Steps:
Clone the repository:
git clone https://github.com/your-username/dragon-repeller-rpg.git

Navigate to the project folder:
cd dragon-repeller-rpg

Launch the Game:
Simply open index.html in your browser.


PROJECT STRUCTURE

/
├── index.html # Main application shell; defines the DOM nodes for Stats
├── styles.css # Stylesheet defining the 500px game container and colors
├── script.js # The game engine; contains State Variables, Functions, Events
└── README.txt # Documentation


DEEP DIVE: THE COMBAT LOGIC
The integrity of the game relies on the getMonsterAttackValue function. This function demonstrates the use of the Math object for game balance.

Mechanism: The monster's attack is calculated by taking its level-based strength and subtracting a random value derived from the player's Experience Points (XP).

Design Insight: This creates a mechanic where XP functions as a "Dodge Chance" or "Defense" stat. As the player grinds for XP, the variance of the monster's damage increases, skewing towards 0 damage.


// Logic balancing monster level against player experience
const hit = (level * 5) - (Math.floor(Math.random() * xp));


FUTURE ROADMAP
To further enhance the application, the following updates are planned:

Persistence: Implementing localStorage to save the inventory and gold variables, allowing players to resume sessions.

Audio: Adding the Web Audio API to trigger sound effects on button clicks and combat events.

Refactoring: Converting the global variable state into a GameState class to better encapsulate logic and prevent namespace pollution.
