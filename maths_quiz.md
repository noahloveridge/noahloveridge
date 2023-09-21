<style>
  .answers {
    margin-bottom: 20px;
  }
  .answers label{
    display: block;
  }
</style>

# Maths Quiz

UNDER CONSTRUCTION - come back soon.

There are three levels. Which one are you going to choose?

<input type="radio" id="level_easy" name="quiz_level" value="easy" checked>
<label for="level_easy">Easy</label><br>

<input type="radio" id="level_medium" name="quiz_level" value="medium">
<label for="level_medium">Medium</label><br>

<input type="radio" id="level_hard" name="quiz_level" value="hard">
<label for="level_hard">Hard</label><br>

<button id="start_quiz_btn">Start Quiz</button>

<div id="quiz"></div>
<button id="submit">Submit Quiz</button>
<div id="results"></div>

<script id="rendered-js" >
(function () {
  function buildQuiz() {

    // disable level selector radio buttons when the quiz starts
    document.getElementById('level_easy').disabled = true;
    document.getElementById('level_medium').disabled = true;
    document.getElementById('level_hard').disabled = true;
    
    // variable to store the HTML output
    const output = [];

    // for each question...
    myQuestions.forEach(
    
    (currentQuestion, questionNumber) => {

      // variable to store the list of possible answers
      const answers = [];

      // and for each available answer...
      for (letter in currentQuestion.answers) {

        // ...add an HTML radio button
        answers.push(
        `<label>
              <input type="radio" name="question${questionNumber}" value="${letter}">
              ${letter} :
              ${currentQuestion.answers[letter]}
            </label>`);
      }

      // add this question and its answers to the output
      output.push(
      `<div class="question"> ${currentQuestion.question} </div>
          <div class="answers"> ${answers.join('')} </div>`);
    });

    // finally combine our output list into one string of HTML and put it on the page
    quizContainer.innerHTML = output.join('');
  }

  function showResults() {

    // gather answer containers from our quiz
    const answerContainers = quizContainer.querySelectorAll('.answers');

    // keep track of user's answers
    let numCorrect = 0;

    // for each question...
    myQuestions.forEach((currentQuestion, questionNumber) => {
  
      // find selected answer
      const answerContainer = answerContainers[questionNumber];
      const selector = `input[name=question${questionNumber}]:checked`;
      const userAnswer = (answerContainer.querySelector(selector) || {}).value;

      // if answer is correct
      if (userAnswer === currentQuestion.correctAnswer) {
        // add to the number of correct answers
        numCorrect++;

        // color the answers green
        answerContainers[questionNumber].style.color = 'lightgreen';
      }
      // if answer is wrong or blank
      else {
          // color the answers red
          answerContainers[questionNumber].style.color = 'red';
        }
    });

    // show number of correct answers out of total
    resultsContainer.innerHTML = `${numCorrect} correct!`;
  }

  const quizContainer = document.getElementById('quiz');
  const resultsContainer = document.getElementById('results');
  const submitButton = document.getElementById('submit');
  const startQuizButton = document.getElementById('start_quiz_btn');

  let myQuestions;
  
  switch ( document.querySelector('input[name="quiz_level"]:checked').value ) {
    case "easy":
      myQuestions = easyQuestions;
      break;
    case "medium":
      myQuestions = mediumQuestions;
      break;
    case "hard":
      myQuestions = hardQuestions;
  }
  
  const easyQuestions = [
  {
    level: "easy",
    question: "What is 7 * 9?",
    answers: {
      a: "79",
      b: "69",
      c: "63"
    },
    correctAnswer: "c"
  },
  {
    level: "easy",
    question: "What is 12 * 11?",
    answers: {
      a: "144",
      b: "132",
      c: "121"
    },
    correctAnswer: "b"
  },
  {
    level: "easy",
    question: "What is 60-29?",
    answers: {
      a: "30",
      b: "29",
      c: "21"
    },
    correctAnswer: "b"
  },
  {
    level: "easy",
    question: "What is 120+60?",
    answers: {
      a: "188",
      b: "80",
      c: "180"
    },
    correctAnswer: "c"
  },
 {
    level: "easy",
    question: "What is 1 * 60?",
    answers: {
      a: "54",
      b: "60",
      c: "79"
    },
    correctAnswer: "b"
  }];

  const mediumQuestions = [
  {
    level: "medium",
    question: "What is 27 * 2?",
    answers: {
      a: "56",
      b: "90",
      c: "60"
    },
    correctAnswer: "a"
  },
  {
    level: "medium",
    question: "What is 13 * 13?",
    answers: {
      a: "244",
      b: "169",
      c: "160",
      d: "194"
    },
    correctAnswer: "b"
  }];

  const hardQuestions = [
  {
    level: "hard",
    question: "What is 7 * 9?",
    answers: {
      a: "79",
      b: "69",
      c: "63"
    },
    correctAnswer: "c"
  }];

  // Kick things off
  // buildQuiz();

  // Event listeners
  submitButton.addEventListener('click', showResults);
  startQuizButton.addEventListener('click', buildQuiz);
})();
</script>
