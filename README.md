# Quiz-Flashcards
A simple and interactive Flashcard Quiz App built using HTML, CSS, and JavaScript. Users can study with flashcards, reveal answers, navigate between cards, and manage their own flashcard collection by adding, editing, and deleting cards. The application features a clean, responsive, and user-friendly interface for effective learning and revision.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Flashcard Quiz App</title>
<style>
    *{
        margin:0;
        padding:0;
        box-sizing:border-box;
        font-family:Arial, sans-serif;
    }

    body{
        background:#f4f6f9;
        display:flex;
        justify-content:center;
        align-items:center;
        min-height:100vh;
        padding:20px;
    }

    .container{
        width:100%;
        max-width:700px;
        background:white;
        padding:25px;
        border-radius:12px;
        box-shadow:0 4px 12px rgba(0,0,0,0.1);
    }

    h1{
        text-align:center;
        margin-bottom:20px;
        color:#333;
    }

    .card{
        border:2px solid #ddd;
        border-radius:10px;
        padding:30px;
        text-align:center;
        min-height:180px;
        display:flex;
        flex-direction:column;
        justify-content:center;
        margin-bottom:20px;
    }

    .card h2{
        color:#222;
        margin-bottom:15px;
    }

    .answer{
        color:#1d4ed8;
        font-size:18px;
        margin-top:10px;
        display:none;
    }

    .btn-group{
        display:flex;
        flex-wrap:wrap;
        gap:10px;
        justify-content:center;
        margin-bottom:20px;
    }

    button{
        padding:10px 18px;
        border:none;
        border-radius:8px;
        cursor:pointer;
        font-size:15px;
    }

    .primary{
        background:#2563eb;
        color:white;
    }

    .success{
        background:#16a34a;
        color:white;
    }

    .warning{
        background:#f59e0b;
        color:white;
    }

    .danger{
        background:#dc2626;
        color:white;
    }

    button:hover{
        opacity:0.9;
    }

    .form{
        display:grid;
        gap:10px;
    }

    input, textarea{
        padding:10px;
        border:1px solid #ccc;
        border-radius:8px;
        width:100%;
    }

    .counter{
        text-align:center;
        color:#666;
        margin-bottom:15px;
    }
</style>
</head>
<body>

<div class="container">
    <h1>📚 Flashcard Quiz App</h1>

    <div class="counter" id="counter"></div>

    <div class="card">
        <h2 id="question">Question</h2>
        <p id="answer" class="answer"></p>
    </div>

    <div class="btn-group">
        <button class="primary" onclick="showAnswer()">Show Answer</button>
        <button class="primary" onclick="prevCard()">Previous</button>
        <button class="primary" onclick="nextCard()">Next</button>
    </div>

    <div class="btn-group">
        <button class="warning" onclick="editCard()">Edit</button>
        <button class="danger" onclick="deleteCard()">Delete</button>
    </div>

    <hr style="margin:20px 0">

    <h3>Add New Flashcard</h3>

    <div class="form">
        <input type="text" id="newQuestion" placeholder="Enter question">
        <textarea id="newAnswer" rows="3" placeholder="Enter answer"></textarea>
        <button class="success" onclick="addCard()">Add Flashcard</button>
    </div>

</div>

<script>
let flashcards = [
    {
        question: "What is HTML?",
        answer: "HTML stands for HyperText Markup Language."
    },
    {
        question: "What is CSS?",
        answer: "CSS is used to style web pages."
    },
    {
        question: "What is JavaScript?",
        answer: "JavaScript adds interactivity to websites."
    }
];

let currentIndex = 0;

function displayCard() {
    if (flashcards.length === 0) {
        document.getElementById("question").textContent =
            "No flashcards available.";
        document.getElementById("answer").style.display = "none";
        document.getElementById("counter").textContent = "";
        return;
    }

    document.getElementById("question").textContent =
        flashcards[currentIndex].question;

    document.getElementById("answer").textContent =
        flashcards[currentIndex].answer;

    document.getElementById("answer").style.display = "none";

    document.getElementById("counter").textContent =
        Card ${currentIndex + 1} of ${flashcards.length};
}

function showAnswer() {
    document.getElementById("answer").style.display = "block";
}

function nextCard() {
    if (flashcards.length === 0) return;

    currentIndex = (currentIndex + 1) % flashcards.length;
    displayCard();
}

function prevCard() {
    if (flashcards.length === 0) return;

    currentIndex =
        (currentIndex - 1 + flashcards.length) % flashcards.length;

    displayCard();
}

function addCard() {
    const question =
        document.getElementById("newQuestion").value.trim();

    const answer =
        document.getElementById("newAnswer").value.trim();

    if (!question || !answer) {
        alert("Please enter both question and answer.");
        return;
    }

    flashcards.push({
        question,
        answer
    });

    document.getElementById("newQuestion").value = "";
    document.getElementById("newAnswer").value = "";

    currentIndex = flashcards.length - 1;
    displayCard();
}

function editCard() {
    if (flashcards.length === 0) return;

    let newQuestion = prompt(
        "Edit Question:",
        flashcards[currentIndex].question
    );

    if (newQuestion === null) return;

    let newAnswer = prompt(
        "Edit Answer:",
        flashcards[currentIndex].answer
    );

    if (newAnswer === null) return;

    flashcards[currentIndex].question = newQuestion;
    flashcards[currentIndex].answer = newAnswer;

    displayCard();
}

function deleteCard() {
    if (flashcards.length === 0) return;

    if (confirm("Delete this flashcard?")) {
        flashcards.splice(currentIndex, 1);

        if (currentIndex >= flashcards.length) {
            currentIndex = flashcards.length - 1;
        }

        displayCard();
    }
}

displayCard();
</script>

</body>
</html>
