
html
=====
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rock Paper Scissors Game</title>
    <link rel="stylesheet" href="sai_css_1.css">
</head>
<body>
    <h1>Rock Paper Scissors Game</h1>
    <div class="choicesa">
    <div class="choice" id="rock">
        <img src="./images/rock.png">
    </div>
    <div class="choice" id="paper">
        <img src="./images/paper.png">
    </div>
    <div class="choice" id="scissors">
        <img src="./images/scissors.png">
    </div>
</div>
    <div class="score-board">
        <div class="score">
            <p id="user-score">0</p>
            <p>You</p>
        </div>
        <div class="score">
            <p id="comp-score">0</p>
            <p>Comp</p>
        </div>

        
        
    </div>
    <div class="msg-container">
        <p id="msg"> Play your move</p>
    </div>







<script src="sai_js_1.js"></script>
</body>
</html>





css
====

*{
    margin:0;
    padding:0;
    text-align:center;
}

h1{
    background-color:#081b31;
    color:white;
    height:5rem;
    /* width:100%; */
    line-height:5rem;  
}

.choice{
    height:165px;
    width:165px;
    border-radius:50%;
    display:flex;
    justify-content:center;
    align-items: center;
}

img{
    height:150px;
    width:150px;
    object-fit:cover;
    border-radius:50%;
}

.choices{
    display:flex;
    justify-content:center;
    align-items:center;
    gap:3rem;
    margin-top:5rem;
}

.choice:hover{
    background-color:#081b31;
    cursor:pointer;
}

.score-board{
    display:flex;
    justify-content:center;
    align-items:center;
    font-size:2rem;
    margin-top:3rem;
    gap:5rem;
}

#user-score,#comp-score{
    font-size:4rem;
}

.msg-container{
    margin-top:5rem;
}

#msg{
    margin-top:5rem;
    background-color:#081b31;
    color:white;
    font-size:2rem;
    display:inline;
    padding:1rem;
    border-radius:1rem;
}




java sript
===========

let userScore = 0;
let compScore = 0;

let choices = document.querySelectorAll(".choice");
let msg = document.querySelector("#msg");

let userScorePara = document.querySelector("#user-score");
let compScorePara = document.querySelector("#comp-score");

let drawGame = () =>{
    msg.innerText = "Game was Draw !";
    msg.style.backgroundColor = "orange"
}

let showWinner = (userWin,userChoice,compChoice) =>{
    if(userWin){
        userScore++;
        userScorePara.innerText = userScore;
        msg.innerText = `You Win :) Your ${userChoice} beats ${compChoice}`;
        msg.style.backgroundColor = "green";
    }else{
        compScore++;
        compScorePara.innerText = compScore;
        msg.innerText = `You Lose :) ${compChoice} beats Your ${userChoice}`;
        msg.style.backgroundColor = "red";
    }
}

let genCompChoice = () => {
    let options = ["rock","paper","scissors"];
    let randIdx = Math.floor(Math.random() *3);
    return options[randIdx];
}

let playGame = (userChoice)=>{
    let compChoice = genCompChoice();

    if (userChoice === compChoice){
        // Draw Game
        drawGame();
    }
    else {
        let userWin = true;
        if(userChoice === "rock"){
            // scissors,paper
            userWin = compChoice === "paper" ? false : true;
        }
        else if (userChoice === "paper"){
            // rock , scissores
            userWin =  compChoice === "scissors" ? false : true;
        }
        else{
            //rock, paper
           userWin =  compChoice === "rock" ? false : true; 
        }
        showWinner(userWin, userChoice,compChoice);
    }

};

choices.forEach((choice)=>{ 
    choice.addEventListener("click",()=>{
        let userChoice = choice.getAttribute("id");
        playGame(userChoice);        
    })
})
