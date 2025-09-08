
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>All-in-One Projects</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; font-family: Arial, sans-serif; }

    body { background: #f9f9f9; color: #333; line-height: 1.6; }

    header { background: #333; color: white; padding: 1rem; text-align: center; }

    nav { display: flex; justify-content: center; background: #444; flex-wrap: wrap; }
    nav a { color: white; padding: 1rem; text-decoration: none; }
    nav a:hover { background: #666; }

    section { padding: 2rem; max-width: 1000px; margin: auto; }

    /* Portfolio */
    .hero { text-align: center; padding: 50px 20px; background: #e2e2e2; }
    .hero h1 span { color: #0077cc; }
    .about img { width: 150px; border-radius: 50%; margin-bottom: 1rem; }

    /* Quiz App */
    .quiz-container { background: white; padding: 20px; border-radius: 10px; 
      max-width: 500px; margin: auto; box-shadow: 0 0 10px rgba(0,0,0,0.2); }
    .quiz-container ul { list-style: none; }
    .quiz-container button { background: #333; color: white; padding: 10px 15px; 
      border: none; border-radius: 5px; cursor: pointer; }
    .quiz-container button:hover { background: #555; }
    .result { font-size: 18px; font-weight: bold; text-align: center; }

    /* Blog */
    .post { background: white; padding: 15px; margin-bottom: 20px; border-radius: 8px; 
      box-shadow: 0 0 5px rgba(0,0,0,0.1); }

    /* Responsive Website */
    .container { display: grid; grid-template-columns: 3fr 1fr; gap: 1rem; padding: 1rem; }
    .content, .sidebar { padding: 1rem; border-radius: 8px; }
    .content { background: #f4f4f4; }
    .sidebar { background: #e2e2e2; }
    @media (max-width: 768px) { .container { grid-template-columns: 1fr; } }

    footer { text-align: center; background: #333; color: white; padding: 1rem; margin-top: 1rem; }
  </style>
</head>
<body>
  <header>
    <h1>All-in-One Projects</h1>
    <p>Portfolio | Quiz | Blog | Responsive Website</p>
  </header>

  <nav>
    <a href="#portfolio">Portfolio</a>
    <a href="#quiz">Quiz</a>
    <a href="#blog">Blog</a>
    <a href="#website">Responsive Website</a>
  </nav>

  <!-- Portfolio -->
  <section id="portfolio">
    <div class="hero">
      <h1>Hello, I'm <span>MR__ RISHI</span></h1>
      <p>I am the veti officer</p>
    </div>
    <div class="about">
      <h2>About Me</h2>
      <img src="IMG_20250908_203956.jpg" alt="Profile Photo">
      <p>I am a student enthusiastic about technology and design. I love building interactive,
        user-friendly web applications and exploring new tools in the tech world.</p>
    </div>
  </section>

  <!-- Quiz App -->
  <section id="quiz">
    <div class="quiz-container" id="quizBox">
      <h2 id="question">Question text</h2>
      <ul>
        <li><label><input type="radio" name="answer" class="answer" id="a"> <span id="a_text">Answer A</span></label></li>
        <li><label><input type="radio" name="answer" class="answer" id="b"> <span id="b_text">Answer B</span></label></li>
        <li><label><input type="radio" name="answer" class="answer" id="c"> <span id="c_text">Answer C</span></label></li>
        <li><label><input type="radio" name="answer" class="answer" id="d"> <span id="d_text">Answer D</span></label></li>
      </ul>
      <button id="submit">Submit</button>
      <div class="result" id="result"></div>
    </div>
  </section>

  <!-- Blog -->
  <section id="blog">
    <h2>My Blog</h2>
    <div class="container" id="postsContainer"></div>
  </section>

  <!-- Responsive Website -->
  <section id="website">
    <h2>Responsive Layout</h2>
    <div class="container">
      <div class="content">
        <h3>Main Content</h3>
        <p>This is the main content area. Resize the window to see the responsive effect.</p>
      </div>
      <div class="sidebar">
        <h3>Sidebar</h3>
        <p>This is a sidebar with some extra information or links.</p>
      </div>
    </div>
  </section>

  <footer>
    <p>&copy; 2025 MR__ RISHI | All Rights Reserved</p>
  </footer>

  <script>
    // QUIZ APP
    const quizData = [
      { question: "Which CSS property is used to change the background color?", a: "bgcolor", b: "background", c: "color", d: "background-color", correct: "d" },
      { question: "Which property is used to change font size?", a: "font-style", b: "text-size", c: "font-size", d: "font", correct: "c" },
      { question: "Which value hides an element completely?", a: "hidden", b: "opacity:0", c: "display:none", d: "visibility:hidden", correct: "c" },
      { question: "Which is a database?", a: "PHP", b: "MySQL", c: "HTML", d: "CSS", correct: "b" }
    ];

    const quiz = document.getElementById("quizBox");
    const answerEls = document.querySelectorAll(".answer");
    const questionEl = document.getElementById("question");
    const a_text = document.getElementById("a_text");
    const b_text = document.getElementById("b_text");
    const c_text = document.getElementById("c_text");
    const d_text = document.getElementById("d_text");
    const submitBtn = document.getElementById("submit");
    const resultEl = document.getElementById("result");

    let currentQuiz = 0, score = 0;
    loadQuiz();

    function loadQuiz() {
      deselectAnswers();
      const current = quizData[currentQuiz];
      questionEl.innerText = current.question;
      a_text.innerText = current.a;
      b_text.innerText = current.b;
      c_text.innerText = current.c;
      d_text.innerText = current.d;
    }

    function getSelected() {
      let answer;
      answerEls.forEach(el => { if (el.checked) answer = el.id; });
      return answer;
    }

    function deselectAnswers() { answerEls.forEach(el => el.checked = false); }

    submitBtn.addEventListener("click", () => {
      const answer = getSelected();
      if (answer) {
        if (answer === quizData[currentQuiz].correct) score++;
        currentQuiz++;
        if (currentQuiz < quizData.length) {
          loadQuiz();
        } else {
          quiz.innerHTML = `<h2 class="result">You answered correctly ${score}/${quizData.length} questions.</h2>
                            <button onclick="location.reload()">Restart</button>`;
        }
      }
    });

    // BLOG POSTS
    function loadPosts() {
      const postsContainer = document.getElementById("postsContainer");
      const posts = JSON.parse(localStorage.getItem("blogPosts")) || [
        { title: "First Blog Post", content: "This is a sample blog post.", date: new Date() }
      ];
      postsContainer.innerHTML = "";
      posts.reverse().forEach(post => {
        const postEl = document.createElement("div");
        postEl.classList.add("post");
        postEl.innerHTML = `<h2>${post.title}</h2>
          <small>${new Date(post.date).toLocaleString()}</small>
          <p>${post.content}</p>`;
        postsContainer.appendChild(postEl);
      });
    }
    loadPosts();
  </script>
</body>
</html>
