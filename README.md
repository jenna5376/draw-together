# Draw Together :art: 

[View full case study here](https://www.hanjenna.com/#/draw-together)

[Try out the game here](https://fine-outgoing-hornet.glitch.me/)
(might take a few seconds to load)

Draw Together is a web app that allows two people to draw collaboratively with each other online! Since coming to college, our team has experienced how hard it is to maintain relationships with all of our friends and families back home, and we wanted to build something that we could use to stay connected. We drew inspiration from a social media trend where couples would draw on a small canvas for a few minutes and swap with each other every few minutes. We wanted to expand on this idea and create games that allow friends to work collaboratively to create more meaningful artwork. There are three game modes you and your friend can play: Draw Together (you and your friend both draw together on one canvas), Top Bottom (you and your friend each draw on either the top half or bottom half of the canvas without being able to see the other half), and Canvas Swap (you and your friend draw on two different canvases and swap canvases every few minutes until the time is up). Our team included one UI/UX Designer, one UI/UX Designer / Front-End Developer, and one Full-Stack Developer. I worked as a UI/UX Designer / Front-End Developer in this project.

## Demo :popcorn: 

https://github.com/jenna5376/draw-together/assets/62906996/6014d8e6-4da6-49b6-9a47-4ffe78bb3449

## How to run 🛠
First, you need to download all the packages used in this project. You can do so by cding into backend first and typing:

`npm i socket.io`

`npm i express concurrently`

`npm i cors`

`npm i http`

`npm i --save-dev nodemon`

For the client side, you will need to type

`npm i socket.io-client`

You can then compile the code and run it on local host by cding into server side and typing

`npm run dev`

## Tech Stack Details :computer: 
For our project, we used React for frontend, Node for backend, and Socket.io to connect server side and client side. Since our app needed constant communication between backend and frontend, we found Socket to be our best choice due to the low latency communication. We stored user and key data in server side, so that when we needed to store any long-term information we retrieved from the players in client side or needed to validate something, we would have our client side Socket emit to backend where our service side Socket would be listening. We would then retrieve the necessary data from backend, and use our server side Socket to emit to our client side Socket, so that our client side will now also hold the information. 

## Challenges :question: 
We had never worked with Node, React, or Socket.io before, so this project provided us with an opportunity to learn the three new frameworks. However, we had a few obstacles that we ran into while we were programming our project. Socket kept firing twice even when we wrapped the socket.emit code in React.useEffect, and there existed timing inconsistencies between both players' web app caused by different renderings and delays between the time it takes for the client side Socket to emit to back end and for server side Socket to emit back. To fix the former problem, instead of passing Socket into our client side files, we passed a boolean variable that would turn true if Socket needs to emit. In our App.js file, we used multiple useEffect functions so that once a boolean variable becomes true, Socket emits a certain message associated with the specific boolean variable to server side. After server side Socket emits back to the client side, we turn the variable false. For the latter problem, instead of forcing our previous ideas, we took a step back and asked ourselves how we could approach the problem differently, and remodeled some of our past ideas to accommodate for the delay time. For example, the two players' timers for Canvas Swap sometimes would not match, so one player would reach the 0 second countdown before the other. When we attempted to fix this, we realized the delays were caused by some things that were out of our control. Since we still had many other functions that needed to be implemented, we decided to run a simple cost-benefit analysis and concluded that attempting to make sure every second was counted down correctly would not be worth our time. Instead, we made it so that the canvases would only swap when both players have reached 0 in their respective countdowns.
