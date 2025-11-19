Comprehensive Technical Analysis of the "Dragon Repeller" Role-Playing Game: Architecture, Implementation, and Portfolio Documentation Strategy




Executive Summary


The transition from guided tutorial learning to professional software engineering is often bridged by the creation of a comprehensive portfolio. Among the myriad projects available to aspiring developers, the "Dragon Repeller" Role-Playing Game (RPG)—a staple of the Codecademy and freeCodeCamp JavaScript curricula—stands out as a particularly robust artifact for demonstrating core competency in web technologies.1 While superficially simple, a rigorous deconstruction of this project reveals a complex interplay of state management, Document Object Model (DOM) manipulation, modular logic design, and algorithmic thinking.3
This report provides an exhaustive, expert-level analysis of the Dragon Repeller project. It is designed not merely to describe the code, but to dissect the architectural decisions, coding conventions, and mechanical systems that underpin the application. Furthermore, this document serves as a strategic guide for developers seeking to leverage this project in their professional portfolios. By synthesizing research on portfolio best practices, resume optimization, and technical documentation 5, this report offers a blueprint for elevating a standard tutorial submission into a compelling proof of engineering aptitude. The following analysis explores the structural foundations of the game, the nuances of its JavaScript logic engine, the mathematical principles governing its combat systems, and the most effective strategies for documenting these skills for hiring managers.8


1. The Pedagogical and Technical Significance of the RPG Archetype


The choice of a Role-Playing Game as a primary learning vehicle in JavaScript courses is not arbitrary. It serves as a microcosm of enterprise-level application development. Unlike static websites, an RPG requires the maintenance of persistent state (health, gold, experience), the handling of complex user events (combat, purchasing, navigation), and the dynamic rendering of data.8


1.1 The Transition from Static to Dynamic Web Development


The Dragon Repeller project represents a pivotal moment in a developer's journey where they graduate from declarative languages (HTML/CSS) to imperative logic (JavaScript). The project forces the developer to grapple with the concept of "application state"—data that changes over time and drives the user interface. In this specific instance, the game models a closed economic and combat system where every user action triggers a chain reaction of variable updates and DOM repainting.1
The pedagogical model employed here typically involves a "Code-Along" structure, yet the resulting artifact allows for significant divergence and personalization, which is critical for portfolio differentiation. By analyzing the project's adherence to concepts like the Finite State Machine (FSM) and data-driven programming, we can identify specific "employability signals" that a hiring manager looks for when reviewing entry-level code.


1.2 Project Scope and Objectives


The core objective of the Dragon Repeller is to build a browser-based game where a player acts as a hero defeating a dragon. The technical requirements include:
* State Tracking: Monitoring variable integers for health, gold, and experience points (XP).
* Inventory Management: Utilizing array data structures to manage strings representing weapons.11
* Conditional Logic: Implementing control flow to handle game-over states, victory conditions, and location changes.
* DOM Interaction: Using JavaScript to "hook" into HTML elements and modify their content dynamically.3
Understanding these objectives is the first step in documenting the project effectively. A high-quality README must articulate not just what the game does, but how it achieves these technical goals through specific architectural choices.12


2. Architectural Analysis: The Structural Layer (HTML)


The skeleton of the Dragon Repeller is built upon HyperText Markup Language (HTML5). While the JavaScript logic often garners the most attention, the structural decisions made in the HTML file impose constraints and opportunities for the logic layer. A professional analysis must scrutinize the semantic quality and structural integrity of this foundation.


2.1 The Container Model and ID Strategy


The interface relies heavily on the div element to create logical groupings of content. The primary container, identifiable by the ID #game, serves as the viewport for the application.13


HTML




<div id="game">
   </div>

This "single-container" approach is standard for small browser games as it simplifies CSS centering and creates a defined coordinate system for the user interface (UI). Within this parent container, the architecture subdivides into three functional areas:
1. The Dashboard (#stats): This section displays the real-time metrics of the player.
2. The Control Plane (#controls): This section houses the interactive elements (buttons).
3. The Narrative Output (#text): This section acts as the system's log, communicating game state changes to the user.
The specific use of id attributes (e.g., #xp, #health, #gold) rather than classes for the numerical spans is a deliberate choice.14 In the context of DOM manipulation performance, selecting by ID (document.querySelector("#id") or document.getElementById("id")) is generally faster and more specific than class selection. This structure implies that there will be exactly one instance of these stats on the page, reinforcing the "Singleton" nature of the game state.


2.2 Semantic Analysis and Accessibility Considerations


While the tutorial code functions correctly, a rigorous portfolio review might identify areas for semantic improvement. The heavy reliance on div tags is typical for older tutorials, but modern HTML5 standards might suggest the use of <main> for the game container, <section> for the stats, and <article> for the narrative text.
Furthermore, the controls are implemented as button elements:


HTML




<div id="controls">
   <button id="button1">Go to store</button>
   <button id="button2">Go to cave</button>
   <button id="button3">Fight dragon</button>
</div>

The reuse of generic IDs (button1, button2, button3) is a critical architectural decision.14 It suggests that the meaning of the buttons will change dynamically via JavaScript, rather than having distinct buttons for every possible action in the game. This necessitates an abstraction layer in the JavaScript to handle the reassignment of button text and event listeners, a complexity that demonstrates intermediate coding ability.4


3. Presentation Layer Analysis (CSS)


The Cascading Style Sheets (CSS) for Dragon Repeller define the visual language of the application. The styling choices are not merely aesthetic; they dictate the usability and layout stability of the game.


3.1 The "Retro" Console Aesthetic


The research indicates a specific color palette and layout strategy designed to evoke a terminal or retro-gaming feel.
* Background Colors: The body is typically styled with a dark blue hue, specifically #0a0a23, which is the brand color for freeCodeCamp, suggesting the tutorial's origin.16 The game container itself is often white or light gray (#ffffff or lightgray) to create high contrast.14
* Layout Constraints: The #game container is restricted by max-width: 500px and max-height: 400px.14 This constraint is vital for ensuring the game remains playable on various screen sizes without reflowing into an unreadable layout. It mimics the fixed-resolution nature of handheld gaming consoles.


3.2 Centering and Box Model


The layout utilizes the margin: 0 auto technique to center the game container horizontally within the viewport.14


CSS




#game {
   max-width: 500px;
   background-color: lightgray;
   margin: 0 auto;
   padding: 10px;
}

This snippet demonstrates an understanding of the CSS Box Model. The padding: 10px ensures that text does not abut the edges of the container, maintaining readability. The separation of the CSS into a distinct styles.css file linked via <link rel="stylesheet"> 13 demonstrates adherence to the "Separation of Concerns" principle, distinguishing the visual layer from the structural (HTML) and behavioral (JS) layers.


3.3 Interactive Feedback


The CSS also plays a role in user feedback. The button elements often include hover states or cursor modifications (cursor: pointer) to signal interactivity.17 Although the research snippets do not detail complex animations, the foundational CSS allows for future enhancements, such as CSS transitions on the health bar or shake animations during damage events, which are excellent candidates for portfolio extensions.


4. The Engine Core: JavaScript Implementation


The heart of the Dragon Repeller is the script.js file. This is where the static markup is transformed into a dynamic experience. The analysis of this layer reveals the developer's grasp of control flow, scope, and data structures.


4.1 Variable Initialization and State Scope


The application begins by defining the state of the world. This is done using the let and const keywords, reflecting modern ES6 standards, though older iterations might use var.
Table 1: Core State Variables and Initialization Analysis


Variable
	Initial Value
	Type
	Scope
	Function
	Source
	xp
	0
	Number
	Global
	Accumulates over time; acts as a defensive modifier in combat.
	1
	health
	100
	Number
	Global
	Decrements during combat; triggers "Game Over" state at <=0.
	14
	gold
	50
	Number
	Global
	Currency resource; exchanged for health or items.
	14
	currentWeapon
	0
	Number
	Global
	Index pointer for the weapons array.
	18
	inventory
	["stick"]
	Array
	Global
	Stores string identifiers of possessed items.
	11
	The choice to place these variables in the global scope (or the top-level scope of the script) is necessary for this specific architectural pattern, where multiple functions need to access and modify the same state. While "global variables" are often discouraged in larger applications due to namespace pollution, in a contained single-script game, they act as the "Store" or "Single Source of Truth." A sophisticated README might acknowledge this trade-off, perhaps suggesting that a class GameState object would be a more encapsulated approach in a refactored version.3


4.2 DOM Element Caching


Before the logic executes, the script establishes references to the HTML elements.


JavaScript




const button1 = document.querySelector("#button1");
const text = document.querySelector("#text");
const xpText = document.querySelector("#xp");

The use of const here is appropriate because the reference to the HTML element does not change, even if the properties of that element (like innerText) do.14 This caching technique improves performance by preventing the browser from having to query the DOM tree every time a variable needs to be updated.


4.3 Variable Naming Conventions


The project strictly adheres to CamelCase naming conventions (e.g., currentWeapon, monsterHealth, goTown).18 This is the standard for JavaScript. Research highlights common pitfalls for beginners, such as confusing variable names like camperbot with xp during the tutorial phase.19 A clean codebase in a portfolio must reflect consistent naming standards. The distinction is also made between the variable name (e.g., monsterName) and the DOM element reference (e.g., monsterNameText), a practice that prevents type confusion between the data string and the HTML span object.14


5. Data-Driven Architecture and State Machines


One of the most sophisticated aspects of the Dragon Repeller project is its shift from hard-coded logic to a data-driven architecture for location management. This is a key differentiator between a novice "spaghetti code" project and a structured application.


5.1 The Locations Array


Instead of writing unique functions for every location transition (e.g., function enterCave(), function enterStore()), the project utilizes an array of objects to define the world.4


JavaScript




const locations = [
   {
       name: "town square",
       "button text": ["Go to store", "Go to cave", "Fight dragon"],
       "button functions":,
       text: "You are in the town square. You see a sign that says \"Store\"."
   },
   {
       name: "store",
       "button text":,
       "button functions":,
       text: "You enter the store."
   }
];

Architectural Insight: This structure essentially creates a configuration file for the game logic. New locations can be added simply by appending a new object to the locations array without writing new control flow logic.21 This adheres to the "Open/Closed Principle" of software design (open for extension, closed for modification), a high-level concept worth mentioning in a technical README.


5.2 The Update Function as a State Engine


The engine that drives this data structure is the update(location) function.


JavaScript




function update(location) {
   monsterStats.style.display = "none";
   button1.innerText = location["button text"];
   button2.innerText = location["button text"];
   button3.innerText = location["button text"];
   button1.onclick = location["button functions"];
   button2.onclick = location["button functions"];
   button3.onclick = location["button functions"];
   text.innerText = location.text;
}

This function acts as the transition mechanism of a Finite State Machine (FSM).4 The location argument represents the next state. The function maps the data from the state object onto the UI elements.
* Dynamic Event Binding: Note how button1.onclick is assigned a function reference (goStore) directly from the array.22 This dynamic binding capability of JavaScript functions (treating functions as first-class citizens) is a critical concept demonstrated here.
* String Escaping: The text property often contains quotes ("You see a sign that says \"Store\"."). The project demonstrates the necessity of string escaping (\") to prevent syntax errors when strings are wrapped in double quotes.3


6. Algorithmic Complexity: Combat and Mathematics


The combat system introduces stochastic elements and mathematical formulas, moving the project beyond simple navigation.


6.1 The Combat Formula


The core mechanic for calculating damage is found in the getMonsterAttackValue function (or similar logic within the fight loop). The formula is cited as:
\begin{equation}
Damage = (Level \times 5) - \lfloor \text{Math.random}() \times XP \rfloor
\end{equation}
Ref: (level * 5) - (Math.floor(Math.random() * xp));.24
Mathematical Analysis:
* Base Damage: The monster's base strength is deterministic: level * 5. A level 2 slime deals 10 base damage.
* Mitigation Factor: The player's Experience Points (XP) act as a reduction to incoming damage.
* Variance: Math.random() generates a float between 0 and 1. Multiplied by xp, this creates a range of damage reduction from 0 to the player's full XP amount.
* Implication: This formula creates an interesting game design dynamic where XP is defensive. High XP means the player has a chance to completely negate damage (if random * xp > level * 5). However, the Math.random() element ensures that even high-level players can take a "lucky hit" from a low-level monster.


6.2 Game Balance and Logic


Implementing this requires using the Math object in JavaScript.
* Math.random(): Essential for RNG (Random Number Generation).
* Math.floor(): Essential for converting the floating-point result of the random calculation into an integer, as health points are typically tracked as whole numbers.24
The logic controls ensuring the player cannot buy health if they lack gold, or cannot buy a weapon if they already have the best one, involves conditional comparators (if (gold >= 30)). This demonstrates "Gatekeeping Logic," fundamental to secure transaction processing in real-world apps.


7. Inventory Systems and Array Manipulation


The inventory system is an excellent demonstration of array manipulation methods.


7.1 Array Methods


The inventory is initialized as ["stick"]. As the player buys weapons, the new items are added using the push() method:


JavaScript




inventory.push(newWeapon);

This mutates the array in place.11 The game also tracks the currentWeapon index. When the player buys a weapon, the code often checks the length of the weapons array to ensure the player doesn't exceed the available distinct items (Stick -> Dagger -> Claw -> Hammer -> Sword).


7.2 Display Logic


The interface doesn't always show the full inventory list, but often shows the current weapon text: text.innerText = "You now have a " + newWeapon + ".". More advanced versions of the tutorial might iterate through the inventory array to display a list of all owned items, requiring a for loop or .map() function, though the standard Dragon Repeller focuses on the current active item.14


8. Portfolio Documentation Strategy


Having analyzed the code, we turn to the critical task of documentation. A project in a portfolio is only as good as its README. The research highlights that a README must answer "What, Why, and How".7


8.1 Structuring the README


A standard "school project" README is insufficient for a professional portfolio. The structure should mirror open-source software documentation.25
Proposed Structure:
1. Title & Badges: Use Shields.io badges to display technologies (JS, HTML, CSS).27
2. Project Description: A high-level summary avoiding "tutorial" language. Use terms like "Browser-based RPG" and "State-managed application."
3. Features: Bullet points translating game mechanics into technical features (e.g., "Dynamic DOM updates," "RNG-based combat logic").
4. Technical Implementation: A deep dive into the code choices (e.g., "Why I used an array of objects for locations"). This is where the developer proves they understand the code they wrote.
5. Installation/Usage: git clone instructions.1
6. Future Improvements: Acknowledging limitations (e.g., "Currently lacks local storage persistence") shows professional self-awareness.


8.2 Visuals and Media


Research strongly suggests the use of visuals.28 Since the game is interactive, a static screenshot is less effective than a GIF.
* Action: Record a short loop of buying a weapon and fighting a monster.
* Tools: Tools like Gifski or LICEcap can generate lightweight GIFs to embed directly in the README.6 This allows a recruiter to see the "Dynamic DOM Manipulation" in action without running the code.


8.3 Resume Integration


The README supports the resume. The research provides specific guidance on how to frame this project in a CV.9
* Avoid: "Created a game with JavaScript."
* Adopt: "Developed a state-driven interactive application using Vanilla JavaScript, utilizing algorithm-based logic for combat simulations and DOM API for real-time interface rendering."
* Key Terms: Finite State Machine, Array Manipulation, Event Handling, CSS Box Model.


9. Extension and Refactoring: Moving Beyond the Tutorial


To truly stand out, the code should be refactored or extended beyond the base tutorial instructions. The research indicates several paths for this.


9.1 ES6 Refactoring


The original tutorials often use standard function declarations. A "Pro" move is to refactor these into Arrow Functions.30
* From: function goTown() {... }
* To: const goTown = () => {... };
This demonstrates familiarity with modern JavaScript (ES6+) syntax. It also helps in handling this contexts if the game were ever converted to a Class-based structure.


9.2 Adding "Easter Eggs" and Features


Some versions of the tutorial suggest adding a hidden "Easter Egg" feature, such as a number guessing game.24 Implementing this shows the ability to create sub-modules within a larger codebase. Additionally, adding a "Save Game" feature using localStorage would address the main limitation of the current app (state loss on refresh) and demonstrate knowledge of the Web Storage API.


9.3 Accessibility Enhancements


The buttons should ideally have aria-label attributes if the text is vague, though in this game the text is descriptive. Ensuring high contrast (which the #0a0a23 background helps with) is also a valid point to mention in the "Accessibility" section of the README.


10. Comprehensive README Deliverable


Below is a complete, professional-grade README template derived from the analysis above. It integrates the "expert" persona's insights directly into the documentation.
________________


Dragon Repeller RPG 🐉


!(https://img.shields.io/badge/JavaScript-ES6-yellow?style=flat-square&logo=javascript)!(https://img.shields.io/badge/HTML5-Semantic-orange?style=flat-square&logo=html5)!(https://img.shields.io/badge/CSS3-Retro-blue?style=flat-square&logo=css3)!(https://img.shields.io/badge/Status-Playable-brightgreen?style=flat-square!(https://img.shields.io/badge/HTML5-Semantic-orange?style=flat-square&logo=html5)!(https://img.shields.io/badge/CSS3-Retro-blue?style=flat-square&logo=css3)!(https://img.shields.io/badge/Status-Playable-brightgreen?style=flat-square!(https://img.shields.io/badge/CSS3-Retro-blue?style=flat-square&logo=css3)!(https://img.shields.io/badge/Status-Playable-brightgreen?style=flat-square)))
A browser-based Role Playing Game (RPG) demonstrating fundamental JavaScript mastery through state management, dynamic DOM manipulation, and interactive game loops.


📖 Overview


Dragon Repeller is an interactive web application that places the user in a procedurally generated combat environment. Players must navigate a fictional economy, manage scarce resources (Gold, Health), and strategically upgrade their inventory to defeat a Dragon boss.
Unlike simple static webpages, this project functions as a Single Page Application (SPA). It relies on a custom-built engine to handle state transitions without page reloads, utilizing the Document Object Model (DOM) to render real-time updates based on user actions. The architecture prioritizes a data-driven approach, separating the game content (locations, dialogue) from the core logic engine, ensuring scalability and cleaner code structure.


✨ Key Features


The application features a robust set of mechanics implemented in Vanilla JavaScript:
   * State-Driven Navigation: A centralized update() function acts as a Finite State Machine (FSM), seamlessly transitioning the interface between the "Town," "Store," and "Combat" modes based on an array of location objects.4
   * Algorithmic Combat System: Combat outcomes are not pre-determined. The game utilizes a stochastic formula (Level * 5) - (Math.random() * XP) to calculate damage, balancing player progression (XP) against monster difficulty.24
   * Dynamic Inventory Management: An array-based inventory system allows for the acquisition and tracking of multiple weapon types (push operations), gating player progress based on current assets.11
   * Reactive UI Dashboard: The #stats panel updates instantaneously to reflect changes in Health, Gold, and XP, utilizing efficient DOM targeting strategies (querySelector, innerText).15
   * Retro Aesthetic: A custom CSS implementation utilizing high-contrast colors (#0a0a23) and fixed-width layouts to emulate handheld gaming consoles.13


🛠️ Technologies & Architecture


This project was built to demonstrate mastery of the core web stack without reliance on external frameworks.
Component
	Technology
	Role in Architecture
	Structure
	HTML5
	Semantic container layout using #game and #controls divisions.
	Presentation
	CSS3
	Flexbox alignment, Box Model constraints, and "Dark Mode" styling.
	Logic
	JavaScript (ES6+)
	Game loop, event handling, and state variable management.
	

Code Highlight: Data-Driven Locations


Instead of hard-coding if/else chains for every room, the game uses an extensible array of objects. This allows new levels to be added simply by defining data, not writing new logic.


JavaScript




// Example of the scalable data structure used
const locations = [
   {
       name: "town square",
       "button text": ["Go to store", "Go to cave", "Fight dragon"],
       "button functions":,
       text: "You are in the town square. You see a sign that says \"Store\"."
   },
   // New locations can be added here without breaking the engine
];



🚀 Getting Started


The project requires no build tools or package managers (npm/yarn), emphasizing the power of native browser technologies.


Prerequisites


   * A modern web browser (Chrome, Firefox, Safari, Edge).
   * A text editor (VS Code) if you wish to modify the source.


Installation Steps


   1. Clone the repository:
Bash
git clone https://github.com/your-username/dragon-repeller-rpg.git

   2. Navigate to the project folder:
Bash
cd dragon-repeller-rpg

   3. Launch the Game:
Simply open index.html in your browser.
      * Mac: open index.html
      * Windows: start index.html


📂 Project Structure


/
├── index.html # Main application shell; defines the DOM nodes for Stats and Controls
├── styles.css # Stylesheet defining the 500px game container and color scheme
├── script.js # The game engine; contains State Variables, Functions, and Event Listeners
└── README.md # Documentation


🧠 Deep Dive: The Combat Logic


The integrity of the game relies on the getMonsterAttackValue function. This function demonstrates the use of the Math object for game balance.
      * Mechanism: The monster's attack is calculated by taking its level-based strength and subtracting a random value derived from the player's Experience Points (XP).
      * Design Insight: This creates a mechanic where XP functions as a "Dodge Chance" or "Defense" stat. As the player grinds for XP, the variance of the monster's damage increases, skewing towards 0 damage.
      * Code Implementation:
JavaScript
// Logic balancing monster level against player experience
const hit = (level * 5) - (Math.floor(Math.random() * xp));



🔮 Future Roadmap


To further enhance the application, the following updates are planned:
         * Persistence: Implementing localStorage to save the inventory and gold variables, allowing players to resume sessions.
         * Audio: Adding the Web Audio API to trigger sound effects on button clicks and combat events.
         * Refactoring: Converting the global variable state into a GameState class to better encapsulate logic and prevent namespace pollution.


🤝 Contributing


Contributions are welcome! Please open an issue to discuss proposed changes or submit a Pull Request.
________________
This project is based on the JavaScript Algorithms and Data Structures certification curriculum.
________________


11. Conclusion


The "Dragon Repeller" RPG is more than a simple tutorial; it is a microcosm of full-stack logical flow. By dissecting its HTML structure, CSS styling, and JavaScript logic, we reveal a project that touches on essential engineering concepts: the separation of concerns, state management, and algorithmic efficiency.
For the aspiring developer, the value lies not in the completion of the tutorial, but in the comprehension of these underlying systems. A portfolio that documents this project with the depth presented in this report—highlighting the "why" behind the "how"—will serve as a powerful signal to hiring managers. It demonstrates that the candidate does not just write code, but understands architecture, appreciates clean design patterns, and can communicate complex technical ideas effectively.
Works cited
         1. Project No. 1 of 21 of the freeCodeCamp course "JavaScript Algorithms and Data Structures". In this practice project, you'll learn fundamental programming concepts in JavaScript by coding your own Role Playing Game. You'll learn how to work with arrays, strings, objects, functions, loops, if/else statements, and more. - GitHub, accessed November 18, 2025, https://github.com/Erikote04/Role-Playing-Game
         2. RPG Practice Project - Code Feedback - The freeCodeCamp Forum, accessed November 18, 2025, https://forum.freecodecamp.org/t/rpg-practice-project/746826
         3. (ARCHIVED) Learn JavaScript by Building a Role Playing Game: Step 50 | freeCodeCamp, accessed November 18, 2025, https://www.youtube.com/watch?v=BycNKz5Ct8c
         4. (ARCHIVED) Learn JavaScript by Building a Role Playing Game - Step 61 - YouTube, accessed November 18, 2025, https://www.youtube.com/watch?v=zyPYIzRXjyI
         5. How to build a portfolio - Codecademy, accessed November 18, 2025, https://www.codecademy.com/resources/videos/setting-up/how-to-build-a-portfolio
         6. matiassingers/awesome-readme - GitHub, accessed November 18, 2025, https://github.com/matiassingers/awesome-readme
         7. Markdown and README.md Files - Codecademy, accessed November 18, 2025, https://www.codecademy.com/article/markdown-and-readmemd-files
         8. Learn JavaScript - Codecademy, accessed November 18, 2025, https://www.codecademy.com/learn/introduction-to-javascript
         9. JavaScript developer Resume Profile - Hire IT People - We get IT done, accessed November 18, 2025, https://www.hireitpeople.com/resume-database/72-web-developer-resumes/28180--javascript-developer-resume-profile
         10. How To Learn JavaScript In 2024 - DreamHost, accessed November 18, 2025, https://www.dreamhost.com/blog/learn-javascript/
         11. (ARCHIVED) Learn JavaScript by Building a Role Playing Game: Step 28 | freeCodeCamp, accessed November 18, 2025, https://www.youtube.com/watch?v=fJ01PKDE0hs
         12. Professional README Guide | The Full-Stack Blog - GitHub Pages, accessed November 18, 2025, https://coding-boot-camp.github.io/full-stack/github/professional-readme-guide/
         13. (ARCHIVED) Learn JavaScript by Building a Role Playing Game: Step 1 | freeCodeCamp, accessed November 18, 2025, https://www.youtube.com/watch?v=WyR1eML1KCA
         14. Dragon Repeller - RPG - CodePen, accessed November 18, 2025, https://codepen.io/beaucarnes/pen/BbLWpe
         15. (ARCHIVED) Learn JavaScript by Building a Role Playing Game - Step 16 | freeCodeCamp, accessed November 18, 2025, https://www.youtube.com/watch?v=1m0dIqD1JmU
         16. Learn Basic JavaScript by Building a Role Playing Game - Step 51, accessed November 18, 2025, https://forum.freecodecamp.org/t/learn-basic-javascript-by-building-a-role-playing-game-step-51/679614
         17. (RPG - Dragon Repeller) run the projet in local - JavaScript - The freeCodeCamp Forum, accessed November 18, 2025, https://forum.freecodecamp.org/t/rpg-dragon-repeller-run-the-projet-in-local/668026
         18. (ARCHIVED) Learn JavaScript by Building a Role Playing Game - Step 9 | freeCodeCamp, accessed November 18, 2025, https://www.youtube.com/watch?v=uORF5VbC-Ts
         19. Learn Basic JavaScript by Building a Role Playing Game - Step 6, accessed November 18, 2025, https://forum.freecodecamp.org/t/learn-basic-javascript-by-building-a-role-playing-game-step-6/685849
         20. Learn Basic JavaScript by Building a Role Playing Game - Step 54, accessed November 18, 2025, https://forum.freecodecamp.org/t/learn-basic-javascript-by-building-a-role-playing-game-step-54/671590
         21. (ARCHIVED) Learn JavaScript by Building a Role Playing Game: Step 59 | freeCodeCamp, accessed November 18, 2025, https://www.youtube.com/watch?v=06wJuT4VIj4
         22. Learn Basic JavaScript by Building a Role Playing Game - Step 68, accessed November 18, 2025, https://forum.freecodecamp.org/t/learn-basic-javascript-by-building-a-role-playing-game-step-68/700281
         23. (ARCHIVED) Learn JavaScript by Building a Role Playing Game - Step 57 | freeCodeCamp, accessed November 18, 2025, https://www.youtube.com/watch?v=Sfo3-RG8TVw
         24. (ARCHIVED) Learn JavaScript by Building a Role Playing Game - Step 143 - YouTube, accessed November 18, 2025, https://www.youtube.com/watch?v=-fBGhp9Vc7A
         25. othneildrew/Best-README-Template: An awesome README template to jumpstart your projects! - GitHub, accessed November 18, 2025, https://github.com/othneildrew/Best-README-Template
         26. How to Write a Good README File for Your GitHub Project - freeCodeCamp, accessed November 18, 2025, https://www.freecodecamp.org/news/how-to-write-a-good-readme-file/
         27. Make GitHub Readme Like Pro - DEV Community, accessed November 18, 2025, https://dev.to/anmolbaranwal/make-github-readme-like-pro-15am
         28. How to Design an Attractive GitHub Profile Readme… | by Piyush Malhotra - Medium, accessed November 18, 2025, https://medium.com/design-bootcamp/how-to-design-an-attractive-github-profile-readme-3618d6c53783
         29. 2025 Entry Level Game Developer Resume Example (+Free Template) - Teal, accessed November 18, 2025, https://www.tealhq.com/resume-example/entry-level-game-developer
         30. Refactor es5 functions to es6 arrow functions - Egghead.io, accessed November 18, 2025, https://egghead.io/lessons/javascript-refactor-es5-functions-to-es6-arrow-functions
         31. Rewriting an Javascript Arrow-function - Stack Overflow, accessed November 18, 2025, https://stackoverflow.com/questions/41698880/rewriting-an-javascript-arrow-function