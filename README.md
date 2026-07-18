# schduelerforhighschool.com
수행평가와 공부를 양립하기 어려운 학생들을 위한 스케쥴러
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>K-고등학생 맞춤형 성취도 연계형 AI 플래너</title>
    <style>
        :root {
            --primary: #4f46e5;
            --primary-hover: #4338ca;
            --bg-main: #f8fafc;
            --bg-card: #ffffff;
            --text-main: #0f172a;
            --text-muted: #475569;
            --border: #e2e8f0;
            --accent-red: #ef4444;
            --accent-green: #10b981;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, system-ui, Roboto, sans-serif;
        }

        body {
            background-color: var(--bg-main);
            color: var(--text-main);
            padding: 40px 20px;
            display: flex;
            justify-content: center;
        }

        .container {
            width: 100%;
            max-width: 900px;
        }

        header {
            text-align: center;
            margin-bottom: 40px;
        }

        header h1 {
            font-size: 28px;
            color: var(--primary);
            margin-bottom: 10px;
        }

        header p {
            color: var(--text-muted);
            font-size: 15px;
        }

        /* 그리드 레이아웃 */
        .step-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 24px;
            margin-bottom: 30px;
        }

        .card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 24px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
        }

        .card-title {
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
            color: var(--text-main);
        }

        .badge {
            background: #e0e7ff;
            color: var(--primary);
            font-size: 12px;
            padding: 4px 8px;
            border-radius: 6px;
            font-weight: 600;
        }

        .form-group {
            margin-bottom: 14px;
        }

        label {
            display: block;
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 6px;
            color: var(--text-muted);
        }

        input, select {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid var(--border);
            border-radius: 8px;
            font-size: 14px;
            outline: none;
            transition: border 0.2s;
        }

        input:focus, select:focus {
            border-color: var(--primary);
        }

        .grid-3col {
            display: grid;
            grid-template-columns: 2fr 1fr 1fr;
            gap: 10px;
            align-items: center;
            margin-bottom: 10px;
        }

        button.btn-primary {
            width: 100%;
            background: var(--primary);
            color: white;
            border: none;
            padding: 14px;
            font-size: 16px;
            font-weight: 700;
            border-radius: 10px;
            cursor: pointer;
            transition: background 0.2s;
            margin-top: 10px;
        }

        button.btn-primary:hover {
            background: var(--primary-hover);
        }

        /* 결과 화면 디자인 */
        .result-section {
            margin-top: 30px;
            background: #ffffff;
            border: 2px solid var(--primary);
        }

        .schedule-list {
            list-style: none;
            margin-top: 15px;
        }

        .schedule-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 16px;
            background: var(--bg-main);
            border-radius: 8px;
            margin-bottom: 10px;
            border-left: 4px solid var(--primary);
        }

        .schedule-item.urgent {
            border-left-color: var(--accent-red);
            background: #fef2f2;
        }

        .subject-name {
            font-weight: 700;
        }

        .time-badge {
            background: #312e81;
            color: white;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 13px;
            font-weight: 600;
        }

        .alert-box {
            background: #fff7ed;
            border: 1px solid #ffedd5;
            color: #c2410c;
            padding: 12px;
            border-radius: 8px;
            font-size: 13px;
            margin-bottom: 15px;
            display: none;
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>🤖 Dynamic AI 학업 플래너 실습 프로토타입</h1>
        <p>목표 등급 격차 분석 및 수행평가 시급성을 반영한 실시간 동적 스케줄링 시스템</p>
    </header>

    <div class="step-grid">
        <div class="card">
            <div class="card-title"><span class="badge">STEP 1</span> 학교 및 학사일정 입력</div>
            <div class="form-group">
                <label for="school-name">학교명</label>
                <input type="text" id="school-name" value="서울고등학교" placeholder="학교명을 입력하세요">
            </div>
            <div class="form-group">
                <label for="exam-date">가장 가까운 지필평가(시험) 시작일</label>
                <input type="date" id="exam-date" value="2026-10-12">
            </div>
        </div>

        <div class="card">
            <div class="card-title"><span class="badge">STEP 2</span> 목표 등급 설정 (가중치 원천)</div>
            <div class="grid-3col" style="font-weight: bold; font-size: 12px; color: var(--text-muted);">
                <div>과목명</div>
                <div>현재 등급</div>
                <div>목표 등급</div>
            </div>
            <div class="grid-3col">
                <div class="subject-name">수학</div>
                <input type="number" id="math-curr" value="4" min="1" max="9">
                <input type="number" id="math-tgt" value="2" min="1" max="9">
            </div>
            <div class="grid-3col">
                <div class="subject-name">국어</div>
                <input type="number" id="kor-curr" value="2" min="1" max="9">
                <input type="number" id="kor-tgt" value="2" min="1" max="9">
            </div>
            <div class="grid-3col">
                <div class="subject-name">영어</div>
                <input type="number" id="eng-curr" value="3" min="1" max="9">
                <input type="number" id="eng-tgt" value="2" min="1" max="9">
            </div>
        </div>

        <div class="card">
            <div class="card-title"><span class="badge">STEP 3</span> 마감 임박 과업 (수행평가 등)</div>
            <div class="form-group">
                <label for="pa-subject">수행평가 과목</label>
                <select id="pa-subject">
                    <option value="영어">영어 수행평가 (에세이 제출)</option>
                    <option value="수학">수학 수행평가 (탐구보고서)</option>
                    <option value="국어">국어 수행평가 (독서활동)</option>
                </select>
            </div>
            <div class="grid-3col" style="grid-template-columns: 1fr 1fr; gap: 15px;">
                <div>
                    <label for="pa-dday">남은 기간 (D-Day)</label>
                    <input type="number" id="pa-dday" value="2" min="1">
                </div>
                <div>
                    <label for="pa-hours">예상 필요 시간 (시간)</label>
                    <input type="number" id="pa-hours" value="2" min="1">
                </div>
            </div>
        </div>

        <div class="card">
            <div class="card-title"><span class="badge">CONFIG</span> 기본 가용 시간</div>
            <div class="form-group">
                <label for="total-time">오늘 자습 가능 시간 (총 시간)</label>
                <input type="number" id="total-time" value="4" min="1" max="15">
            </div>
            <button class="btn-primary" onclick="generateSchedule()">⚡ AI 동적 스케줄링 시작</button>
        </div>
    </div>

    <div class="card result-section">
        <div class="card-title" style="color: var(--primary);">🎯 STEP 4: AI 최적화 동적 시간표 출력 결과</div>
        <div id="alert-zone" class="alert-box"></div>
        <ul class="schedule-list" id="schedule-result">
            </ul>
    </div>
</div>

<script>
    function generateSchedule() {
        // 1. 입력 폼으로부터 데이터 수집
        const totalHours = parseFloat(document.getElementById('total-time').value) || 4;
        const totalMinutes = totalHours * 60;

        // 등급 격차(Gap) 계산 알고리즘: (현재 등급 - 목표 등급) + 1 -> 격차가 클수록 가중치 상승
        const mathGap = Math.max(1, (parseInt(document.getElementById('math-curr').value) - parseInt(document.getElementById('math-tgt').value)) + 1);
        const korGap = Math.max(1, (parseInt(document.getElementById('kor-curr').value) - parseInt(document.getElementById('kor-tgt').value)) + 1);
        const engGap = Math.max(1, (parseInt(document.getElementById('eng-curr').value) - parseInt(document.getElementById('eng-tgt').value)) + 1);

        let weights = { "수학": mathGap, "국어": korGap, "영어": engGap };
        let totalWeight = weights["수학"] + weights["국어"] + weights["영어"];

        // 1차 공부시간 수학적 배분 (총 시간 * 내 과목 가중치 비율)
        let allocated = {
            "수학": Math.round((weights["수학"] / totalWeight) * totalMinutes),
            "국어": Math.round((weights["국어"] / totalWeight) * totalMinutes),
            "영어": Math.round((weights["영어"] / totalWeight) * totalMinutes)
        };

        // 2. 수행평가 마감 임박에 따른 동적 예외 조건 제어(Dynamic Exception Handling)
        const paSubject = document.getElementById('pa-subject').value;
        const paDday = parseInt(document.getElementById('pa-dday').value) || 3;
        const paHours = parseFloat(document.getElementById('pa-hours').value) || 2;
        
        const alertZone = document.getElementById('alert-zone');
        alertZone.style.display = "none";

        let urgentSubject = "";
        // 마감 D-Day가 3일 이하로 남았을 경우 시스템이 우선순위를 강제로 깨뜨리고 스케줄링 조정
        if (paDday <= 3) {
            urgentSubject = paSubject;
            const extraMinutes = Math.round((paHours * 60) / paDday);
            allocated[paSubject] += extraMinutes;
            
            alertZone.innerHTML = `⚠️ <strong>[AI 실시간 제어 알림]</strong> ${paSubject} 수행평가 마감이 ${paDday}일 남았습니다. 오늘 자습 일정에 ${extraMinutes}분을 긴급 추가 배치하여 위험 요소를 분산시켰습니다.`;
            alertZone.style.display = "block";
        }

        // 3. 계산된 정량적 스케줄 데이터를 HTML 문서에 동적 바인딩 및 렌더링
        const resultUl = document.getElementById('schedule-result');
        resultUl.innerHTML = "";

        for (const [subject, mins] of Object.entries(allocated)) {
            const hrs = Math.floor(mins / 60);
            const rMins = mins % 60;
            
            const li = document.createElement('li');
            // 마감 임박 과목은 시각적 강조 피드백 제공 (빨간 테두리)
            li.className = `schedule-item ${subject === urgentSubject ? 'urgent' : ''}`;
            
            li.innerHTML = `
                <div>
                    <span class="subject-name">${subject}</span>
                    ${subject === urgentSubject ? ' <span style="color:var(--accent-red); font-size:12px; font-weight:bold;">[🔥 수행평가 집중 기간]</span>' : ''}
                    <div style="font-size: 12px; color: var(--text-muted); margin-top: 2px;">
                        등급 Gap 분석에 따른 배정 가중치: ${weights[subject]}점
                    </div>
                </div>
                <span class="time-badge">${hrs > 0 ? hrs + '시간 ' : ''}${rMins}분</span>
            `;
            resultUl.appendChild(li);
        }
    }

    // 문서 로드 시 최초 1회 실행하여 초기값 매핑
    window.onload = generateSchedule;
</script>

</body>
</html>
