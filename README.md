# stage-lab---I-am
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>성격 유형 테스트</title>
  <style>
    body { font-family: sans-serif; text-align: center; padding: 40px; }
    .question-box { margin-bottom: 20px; }
    .option-btn { display: block; margin: 10px auto; padding: 10px 20px; border: 1px solid #ccc; cursor: pointer; }
    #result { margin-top: 30px; font-size: 1.2em; font-weight: bold; }
  </style>
</head>
<body>

  <div id="quiz">
    <div id="question" class="question-box">질문이 여기에 나옵니다</div>
    <div id="options"></div>
  </div>
  <div id="result"></div>

  <script>
    const questions = [
      { q: "혼자 있는 게 편한가요?", options: ["예", "아니오"], score: ["I", "E"] },
      { q: "계획적인 걸 좋아하나요?", options: ["예", "아니오"], score: ["J", "P"] },
    ];

    let current = 0;
    let resultScore = {};

    function showQuestion() {
      const q = questions[current];
      document.getElementById("question").textContent = q.q;
      const optionsDiv = document.getElementById("options");
      optionsDiv.innerHTML = "";
      q.options.forEach((opt, i) => {
        const btn = document.createElement("button");
        btn.className = "option-btn";
        btn.textContent = opt;
        btn.onclick = () => {
          const key = q.score[i];
          resultScore[key] = (resultScore[key] || 0) + 1;
          current++;
          if (current < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsDiv.appendChild(btn);
      });
    }

    function showResult() {
      let result = Object.entries(resultScore)
        .sort((a, b) => b[1] - a[1])
        .map(e => e[0])
        .join("");
      document.getElementById("quiz").style.display = "none";
      document.getElementById("result").textContent = `당신의 유형: ${result}`;
    }

    showQuestion();
  </script>

</body>
</html>
