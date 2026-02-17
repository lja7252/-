<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>궁합 테스트</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Gaegu:wght@400;700&display=swap');

        body {
            font-family: 'Gaegu', cursive;
            background-color: #ffdee9; 
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            color: #555;
        }

        .container {
            background-color: white;
            padding: 2.5rem 1.5rem;
            border-radius: 30px;
            box-shadow: 0 10px 25px rgba(255, 133, 161, 0.2);
            text-align: center;
            width: 85%;
            max-width: 380px;
            border: 5px solid #ffb7c5;
        }

        .title {
            font-size: 2.5rem;
            color: #ff85a1;
            margin-top: 0;
            margin-bottom: 5px;
            font-weight: 700;
        }

        /* 문구가 한 줄로 나오도록 수정된 부분 */
        .intro-text {
            font-size: 1.2rem; /* 글자 크기를 살짝 줄임 */
            margin-bottom: 20px;
            color: #777;
            white-space: nowrap; /* 줄바꿈 방지 */
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .input-group input {
            width: 85%;
            padding: 15px;
            margin: 10px 0;
            border: 2px solid #b5fffc; 
            border-radius: 20px;
            font-family: 'Gaegu', cursive;
            font-size: 1.3rem;
            text-align: center;
            outline: none;
        }

        .heart { 
            color: #ff85a1; 
            font-size: 2rem; 
            margin: 5px 0; 
            animation: pulse 1s infinite alternate;
        }

        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.15); }
        }

        #calcBtn {
            background-color: #ff85a1;
            color: white;
            border: none;
            padding: 15px 0;
            width: 90%;
            max-width: 300px;
            font-size: 1.6rem;
            border-radius: 50px;
            cursor: pointer;
            font-family: 'Gaegu', cursive;
            margin-top: 15px;
            transition: 0.2s;
            white-space: nowrap;
            box-shadow: 0 4px 0 #e6738e;
        }

        #calcBtn:hover { background-color: #ff6b8d; transform: scale(1.02); }

        #resultArea {
            margin-top: 20px;
            display: none; 
        }

        .score-text {
            font-size: 4rem;
            color: #ff4d6d;
            font-weight: bold;
            margin: 10px 0;
        }

        #msgDisplay {
            font-size: 1.3rem;
            line-height: 1.6;
            margin-bottom: 20px;
            white-space: pre-line;
            color: #444;
        }

        .retry-btn {
            background-color: #87ceeb;
            border: none;
            color: white;
            padding: 8px 25px;
            border-radius: 20px;
            font-family: 'Gaegu';
            cursor: pointer;
            font-size: 1.1rem;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="title">궁합 테스트</div>
    <div class="intro-text">우리 둘은 얼마나 잘 어울릴까?</div>

    <div class="input-group">
        <input type="text" id="name1" placeholder="내 이름" maxlength="5">
        <div class="heart">♥</div>
        <input type="text" id="name2" placeholder="상대방 이름" maxlength="5">
    </div>

    <button id="calcBtn" onclick="startTest()">결과 확인하기!</button>

    <div id="resultArea">
        <p>두 분의 궁합 점수는...</p>
        <div class="score-text" id="scoreDisplay">0%</div>
        <p id="msgDisplay"></p>
        <button class="retry-btn" onclick="location.reload()">다시 하기</button>
    </div>
</div>

<script>
    function startTest() {
        const n1 = document.getElementById('name1').value.trim();
        const n2 = document.getElementById('name2').value.trim();

        if (!n1 || !n2) {
            alert("이름을 꼭 입력해 주세요!");
            return;
        }

        document.getElementById('calcBtn').style.display = "none";
        document.getElementById('resultArea').style.display = "block";

        let total = 0;
        for (let i = 0; i < n1.length; i++) total += n1.charCodeAt(i);
        for (let i = 0; i < n2.length; i++) total += n2.charCodeAt(i);
        const finalScore = (total % 41) + 60; 

        let current = 0;
        const timer = setInterval(() => {
            if (current >= finalScore) {
                clearInterval(timer);
                showFinalMessage(finalScore);
            } else {
                current++;
                document.getElementById('scoreDisplay').innerText = current + "%";
            }
        }, 20);
    }

    function showFinalMessage(score) {
        let msg = "";
        if (score >= 90) {
            msg = "운명적인 만남이네요!\n오늘부터 1일?";
        } else if (score >= 80) {
            msg = "아주 좋은 사이예요!\n더 가까워져 보세요!";
        } else if (score >= 70) {
            msg = "무난한 사이!\n조금 더 노력이 필요할지도?";
        } else {
            msg = "친구부터 차근차근\n시작해보는 건 어때요?";
        }
        document.getElementById('msgDisplay').innerText = msg;
    }
</script>

</body>
