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

<hr>

<div id="quiz"></div>
<button id="submit">Submit Quiz</button>
<div id="results"></div>

<script id="rendered-js" >
(function () {
  function buildQuiz() {
    
    // variable to store the HTML output
    const output = [];

    // for each question...
    myQuestions.forEach(
    
    (currentQuestion, questionNumber) => {

    // only render questions for the selected level
    if ( ${currentQuestion.level } != document.querySelector('input[name="quiz_level"]:checked').value ) { continue; }
      
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
    resultsContainer.innerHTML = `${numCorrect} out of ${myQuestions.length}`;
  }

  const quizContainer = document.getElementById('quiz');
  const resultsContainer = document.getElementById('results');
  const submitButton = document.getElementById('submit');
  const myQuestions = [
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

  // Kick things off
  buildQuiz();

  // Event listeners
  submitButton.addEventListener('click', showResults);
})();
</script>
