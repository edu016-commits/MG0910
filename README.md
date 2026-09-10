[mg_pocket_loan_calculator.html](https://github.com/user-attachments/files/32033594/mg_pocket_loan_calculator.html)
# MG0910

## 대출상환계산기

여기는 대출상환 계산기를 올리는 저장소
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>MG 포켓 대출 계산기</title>

<style>
:root {
    --pokemon-yellow: #ffcb05;
    --pokemon-yellow-dark: #e2a900;
    --pokemon-blue: #2a75bb;
    --pokemon-blue-dark: #1b4f8a;
    --pokemon-red: #ef5350;
    --pokemon-red-dark: #c62828;
    --ink: #263238;
    --muted: #697780;
    --line: #d9e1e5;
    --white: #ffffff;
    --surface: #ffffff;
    --background: #edf5fa;
    --green: #4caf50;
    --shadow:
        0 5px 0 rgba(28, 65, 100, .10),
        0 14px 28px rgba(28, 65, 100, .13);
    --radius-xl: 24px;
    --radius-lg: 18px;
    --radius-md: 13px;
}

* { box-sizing: border-box; }
html { scroll-behavior: smooth; }

body {
    margin: 0;
    font-family: "Pretendard","Noto Sans KR","Malgun Gothic",sans-serif;
    color: var(--ink);
    background:
        radial-gradient(circle at 20% 15%, rgba(255, 203, 5, .22), transparent 20%),
        radial-gradient(circle at 85% 20%, rgba(42, 117, 187, .14), transparent 24%),
        #edf5fa;
    min-height: 100vh;
}

button, input { font: inherit; }
button { cursor: pointer; }

.hero {
    position: relative;
    overflow: hidden;
    background: linear-gradient(135deg, #2775b8 0%, #3f92cf 55%, #67b4dc 100%);
    color: #fff;
    padding: 30px 22px 76px;
    border-bottom: 7px solid var(--pokemon-yellow);
}

.hero::before {
    content: "";
    position: absolute;
    width: 360px;
    height: 360px;
    border-radius: 50%;
    right: -110px;
    top: -180px;
    background: rgba(255, 255, 255, .07);
    border: 35px solid rgba(255,255,255,.05);
}

.hero-inner {
    width: min(1180px, 100%);
    margin: auto;
    position: relative;
    z-index: 2;
}

.top-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
}

.brand {
    display: flex;
    align-items: center;
    gap: 13px;
}

.pokeball {
    width: 50px;
    height: 50px;
    flex-shrink: 0;
    border-radius: 50%;
    position: relative;
    border: 4px solid #263238;
    background:
        linear-gradient(
            to bottom,
            #ef5350 0%,
            #ef5350 44%,
            #263238 44%,
            #263238 56%,
            #ffffff 56%,
            #ffffff 100%
        );
    box-shadow: 0 4px 0 rgba(0,0,0,.12);
}

.pokeball::after {
    content: "";
    width: 15px;
    height: 15px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    border-radius: 50%;
    background: white;
    border: 4px solid #263238;
}

.brand-small {
    font-size: 12px;
    opacity: .82;
    font-weight: 700;
}

.brand-title {
    font-size: 18px;
    font-weight: 900;
    letter-spacing: -.5px;
}

.trainer-badge {
    padding: 8px 13px;
    border-radius: 999px;
    border: 2px solid rgba(255,255,255,.45);
    background: rgba(255,255,255,.15);
    font-size: 11px;
    font-weight: 800;
    backdrop-filter: blur(8px);
}

.hero-copy { max-width: 660px; }

.hero-label {
    display: inline-block;
    color: #334155;
    background: var(--pokemon-yellow);
    padding: 6px 11px;
    border-radius: 999px;
    font-weight: 900;
    font-size: 11px;
    margin-bottom: 13px;
    box-shadow: 0 4px 0 rgba(0,0,0,.10);
}

.hero h1 {
    margin: 0;
    font-size: clamp(30px, 5vw, 47px);
    letter-spacing: -2px;
    line-height: 1.15;
    text-shadow: 0 3px 0 rgba(0,0,0,.10);
}

.hero p {
    margin: 14px 0 0;
    max-width: 600px;
    font-size: 14px;
    line-height: 1.75;
    color: rgba(255,255,255,.87);
}

.container {
    width: min(1180px, calc(100% - 30px));
    margin: -43px auto 60px;
    position: relative;
    z-index: 5;
}

.grid {
    display: grid;
    grid-template-columns: minmax(330px, 410px) minmax(0, 1fr);
    gap: 22px;
    align-items: start;
}

.card {
    background: var(--surface);
    border: 3px solid #314a60;
    border-radius: var(--radius-xl);
    box-shadow: var(--shadow);
    overflow: hidden;
}

.input-panel {
    position: sticky;
    top: 20px;
}

.panel-header {
    position: relative;
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 19px 22px;
    background: linear-gradient(135deg, #ffda3d, var(--pokemon-yellow));
    border-bottom: 3px solid #314a60;
}

.panel-header-number {
    width: 36px;
    height: 36px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    background: #fff;
    border: 3px solid #314a60;
    font-weight: 900;
    font-size: 14px;
}

.panel-header h2 {
    margin: 0;
    font-size: 18px;
    font-weight: 900;
    letter-spacing: -.6px;
}

.panel-header small {
    display: block;
    margin-top: 2px;
    color: rgba(38,50,56,.68);
    font-size: 10px;
}

.fields { padding: 7px 22px 22px; }

.field {
    padding: 18px 0;
    border-bottom: 2px dashed #dbe4e9;
}

.field:last-child { border-bottom: none; }

.field-title-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
    gap: 10px;
}

.field-label {
    font-size: 14px;
    font-weight: 900;
}

.field-help {
    font-size: 10px;
    color: var(--muted);
}

.input-shell {
    display: flex;
    align-items: center;
    height: 49px;
    border: 2px solid #78909c;
    border-radius: 12px;
    background: #f9fcfd;
    transition: border-color .15s, box-shadow .15s, transform .15s;
}

.input-shell:focus-within {
    border-color: var(--pokemon-blue);
    box-shadow: 0 0 0 4px rgba(42,117,187,.12);
    transform: translateY(-1px);
}

.input-shell input {
    width: 100%;
    min-width: 0;
    border: none;
    outline: none;
    text-align: right;
    padding: 0 12px;
    background: transparent;
    color: var(--ink);
    font-weight: 900;
}

.unit {
    padding-right: 13px;
    color: var(--muted);
    font-size: 12px;
    font-weight: 800;
    white-space: nowrap;
}

.amount-preview {
    margin-top: 7px;
    text-align: right;
    color: var(--pokemon-blue-dark);
    font-weight: 900;
    font-size: 12px;
}

.quick-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 7px;
    margin-top: 10px;
}

.quick-btn {
    min-height: 37px;
    border: 2px solid #314a60;
    border-radius: 11px;
    background: #fff7c5;
    color: #384752;
    font-weight: 900;
    font-size: 11px;
    box-shadow: 0 3px 0 #314a60;
    transition: transform .12s, box-shadow .12s, background .12s;
}

.quick-btn:hover {
    background: var(--pokemon-yellow);
    transform: translateY(-1px);
}

.quick-btn:active {
    transform: translateY(2px);
    box-shadow: 0 1px 0 #314a60;
}

.range-wrap { margin-top: 16px; }
input[type="range"] { width: 100%; accent-color: var(--pokemon-blue); }

.range-labels {
    display: flex;
    justify-content: space-between;
    margin-top: 2px;
    font-size: 9px;
    color: #8a99a2;
}

.segmented {
    display: flex;
    border: 2px solid #314a60;
    border-radius: 10px;
    overflow: hidden;
    background: white;
}

.segmented button {
    height: 31px;
    min-width: 43px;
    border: none;
    background: white;
    color: #697780;
    font-size: 11px;
    font-weight: 900;
}

.segmented button.active {
    background: var(--pokemon-blue);
    color: white;
}

.repayment-list {
    display: grid;
    gap: 9px;
}

.repayment-option input { display: none; }

.repayment-card {
    display: flex;
    gap: 10px;
    align-items: center;
    padding: 12px;
    border: 2px solid #b7c4ca;
    border-radius: 13px;
    background: #fbfdfe;
    cursor: pointer;
    transition: .15s ease;
}

.repayment-card:hover { border-color: var(--pokemon-blue); }

.repayment-option input:checked + .repayment-card {
    border-color: #314a60;
    background: #fff6b8;
    box-shadow: 3px 3px 0 #314a60;
}

.type-ball {
    width: 25px;
    height: 25px;
    border-radius: 50%;
    flex-shrink: 0;
    border: 3px solid #314a60;
    position: relative;
    background: linear-gradient(
        to bottom,
        var(--pokemon-red) 47%,
        #314a60 47%,
        #314a60 58%,
        white 58%
    );
}

.type-ball::after {
    content: "";
    width: 5px;
    height: 5px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    border-radius: 50%;
    background: #fff;
    border: 2px solid #314a60;
}

.repayment-name {
    font-size: 12px;
    font-weight: 900;
}

.repayment-desc {
    margin-top: 2px;
    font-size: 9px;
    color: var(--muted);
}

.calculate-btn {
    width: 100%;
    height: 54px;
    margin-top: 13px;
    border: 3px solid #314a60;
    border-radius: 14px;
    background: var(--pokemon-red);
    color: white;
    font-size: 15px;
    font-weight: 900;
    letter-spacing: -.3px;
    box-shadow: 0 5px 0 #9c2929;
    transition: transform .12s, box-shadow .12s, background .12s;
}

.calculate-btn:hover {
    background: #f4615f;
    transform: translateY(-1px);
}

.calculate-btn:active {
    transform: translateY(4px);
    box-shadow: 0 1px 0 #9c2929;
}

.error {
    display: none;
    margin-top: 12px;
    padding: 11px;
    border: 2px solid var(--pokemon-red-dark);
    border-radius: 10px;
    background: #ffebee;
    color: var(--pokemon-red-dark);
    font-size: 11px;
    font-weight: 700;
}

.result-title {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 18px 23px;
    background: #f6fbfe;
    border-bottom: 3px solid #314a60;
}

.result-title-left {
    display: flex;
    align-items: center;
    gap: 10px;
}

.dex-icon {
    width: 37px;
    height: 37px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: var(--pokemon-red);
    color: #fff;
    border: 3px solid #314a60;
    border-radius: 10px;
    font-size: 15px;
    font-weight: 900;
    box-shadow: 2px 2px 0 #314a60;
}

.result-title h2 {
    margin: 0;
    font-size: 18px;
    font-weight: 900;
}

.result-subtitle {
    margin-top: 2px;
    font-size: 10px;
    color: var(--muted);
}

.status-chip {
    display: flex;
    align-items: center;
    gap: 5px;
    padding: 6px 9px;
    border-radius: 999px;
    background: #e8f5e9;
    color: #287132;
    font-size: 9px;
    font-weight: 900;
}

.status-dot {
    width: 7px;
    height: 7px;
    border-radius: 50%;
    background: var(--green);
}

.summary-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
    padding: 21px 23px 15px;
}

.stat-card {
    border: 3px solid #314a60;
    border-radius: var(--radius-lg);
    padding: 19px;
    position: relative;
    overflow: hidden;
    min-height: 135px;
}

.stat-card.payment {
    background: linear-gradient(145deg, #ffe354, var(--pokemon-yellow));
}

.stat-card.interest {
    background: linear-gradient(145deg, #d9ebfa, #b8dcf3);
}

.stat-card::after {
    content: "";
    width: 70px;
    height: 70px;
    position: absolute;
    right: -25px;
    bottom: -27px;
    border: 12px solid rgba(49,74,96,.08);
    border-radius: 50%;
}

.stat-label {
    position: relative;
    z-index: 1;
    font-size: 11px;
    font-weight: 900;
    color: #59656d;
}

.stat-value {
    position: relative;
    z-index: 1;
    display: flex;
    align-items: baseline;
    gap: 4px;
    margin-top: 12px;
    font-weight: 900;
    font-size: clamp(23px, 3.3vw, 31px);
    letter-spacing: -1.5px;
}

.stat-won { font-size: 12px; }

.stat-caption {
    position: relative;
    z-index: 1;
    margin-top: 8px;
    font-size: 9px;
    color: #697780;
}

.loan-info {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    padding: 0 23px 20px;
}

.info-chip {
    padding: 6px 9px;
    border-radius: 999px;
    border: 1px solid #c8d3d9;
    background: #f4f8fa;
    color: #566570;
    font-size: 9px;
    font-weight: 800;
}

.schedule { border-top: 3px solid #314a60; }

.schedule-heading {
    padding: 17px 23px 13px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #fff;
}

.schedule-heading strong {
    font-size: 14px;
    font-weight: 900;
}

.schedule-heading span {
    padding: 4px 8px;
    border-radius: 999px;
    background: var(--pokemon-blue);
    color: white;
    font-size: 9px;
    font-weight: 900;
}

.table-wrap {
    width: 100%;
    max-height: 590px;
    overflow: auto;
    border-top: 1px solid #d6e0e5;
}

table {
    width: 100%;
    min-width: 650px;
    border-collapse: collapse;
    table-layout: fixed;
}

th {
    position: sticky;
    top: 0;
    z-index: 3;
    padding: 11px 9px;
    border-bottom: 2px solid #314a60;
    background: #e8f4fb;
    color: #4d5f6b;
    text-align: right;
    font-size: 10px;
    font-weight: 900;
}

td {
    padding: 11px 9px;
    border-bottom: 1px solid #e4eaed;
    text-align: right;
    white-space: nowrap;
    font-size: 11px;
}

th:first-child,
td:first-child {
    width: 70px;
    text-align: center;
    font-weight: 900;
}

tbody tr:nth-child(even) { background: #fafcfd; }
tbody tr:hover { background: #fff9ce; }

.payment-cell {
    color: var(--pokemon-blue-dark);
    font-weight: 900;
}

.notice {
    display: flex;
    gap: 10px;
    margin: 20px 23px 23px;
    padding: 13px;
    border: 2px dashed #adbcc4;
    border-radius: 12px;
    background: #f5f8fa;
    color: #72808a;
    font-size: 9px;
    line-height: 1.6;
}

.notice-icon {
    width: 23px;
    height: 23px;
    flex-shrink: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    background: var(--pokemon-yellow);
    color: #314a60;
    border: 2px solid #314a60;
    font-weight: 900;
}

@media (max-width: 900px) {
    .grid { grid-template-columns: 1fr; }
    .input-panel { position: static; }
}

@media (max-width: 600px) {
    .hero { padding: 22px 15px 63px; }
    .trainer-badge { display: none; }
    .container { width: min(100% - 20px, 1180px); }
    .summary-grid {
        grid-template-columns: 1fr;
        padding-left: 15px;
        padding-right: 15px;
    }
    .fields {
        padding-left: 16px;
        padding-right: 16px;
    }
    .result-title {
        padding-left: 15px;
        padding-right: 15px;
    }
    .loan-info {
        padding-left: 15px;
        padding-right: 15px;
    }
    .schedule-heading {
        padding-left: 15px;
        padding-right: 15px;
    }
    .notice {
        margin-left: 15px;
        margin-right: 15px;
    }
    .brand-title { font-size: 15px; }
}
</style>
</head>

<body>

<header class="hero">
    <div class="hero-inner">
        <div class="top-bar">
            <div class="brand">
                <div class="pokeball"></div>
                <div>
                    <div class="brand-small">MG FINANCE ADVENTURE</div>
                    <div class="brand-title">MG 포켓 대출 계산기</div>
                </div>
            </div>
            <div class="trainer-badge">★ FINANCE TRAINER</div>
        </div>

        <div class="hero-copy">
            <div class="hero-label">LOAN QUEST</div>
            <h1>나에게 딱 맞는<br>상환 플랜을 찾아보세요!</h1>
            <p>
                대출 금액, 기간, 금리를 선택하고 나만의 상환 스케줄을 확인하세요.
                조건을 바꾸면 계산 결과가 즉시 업데이트됩니다.
            </p>
        </div>
    </div>
</header>

<main class="container">
<div class="grid">

<section class="card input-panel">
    <div class="panel-header">
        <div class="panel-header-number">01</div>
        <div>
            <h2>대출 조건 선택</h2>
            <small>나만의 대출 정보를 설정하세요</small>
        </div>
    </div>

    <div class="fields">
        <div class="field">
            <div class="field-title-row">
                <div>
                    <div class="field-label">💰 대출 금액</div>
                    <div class="field-help">만원 단위로 입력합니다.</div>
                </div>
            </div>

            <div class="input-shell">
                <input type="number" id="loanAmount" value="1000" min="10" max="100000" step="1">
                <span class="unit">만원</span>
            </div>

            <div class="amount-preview" id="amountPreview">10,000,000원</div>

            <div class="quick-grid">
                <button class="quick-btn" data-amount="100">+ 100만원</button>
                <button class="quick-btn" data-amount="500">+ 500만원</button>
                <button class="quick-btn" data-amount="1000">+ 1,000만원</button>
            </div>

            <div class="range-wrap">
                <input type="range" id="amountRange" min="10" max="10000" value="1000" step="10">
                <div class="range-labels">
                    <span>10만원</span>
                    <span>1억원</span>
                </div>
            </div>
        </div>

        <div class="field">
            <div class="field-title-row">
                <div>
                    <div class="field-label">⏱️ 대출 기간</div>
                    <div class="field-help">상환 기간을 설정하세요.</div>
                </div>

                <div class="segmented">
                    <button id="monthBtn" class="active" type="button">개월</button>
                    <button id="yearBtn" type="button">년</button>
                </div>
            </div>

            <div class="input-shell">
                <input type="number" id="loanTerm" value="36" min="1" max="360">
                <span class="unit" id="termUnitLabel">개월</span>
            </div>

            <div class="range-wrap">
                <input type="range" id="termRange" min="1" max="360" value="36" step="1">
                <div class="range-labels">
                    <span id="termMinLabel">1개월</span>
                    <span id="termMaxLabel">360개월</span>
                </div>
            </div>
        </div>

        <div class="field">
            <div class="field-title-row">
                <div>
                    <div class="field-label">⚡ 연 이자율</div>
                    <div class="field-help">적용 금리를 입력하세요.</div>
                </div>
            </div>

            <div class="input-shell">
                <input type="number" id="annualRate" value="4.5" min="0" max="30" step="0.01">
                <span class="unit">%</span>
            </div>

            <div class="range-wrap">
                <input type="range" id="rateRange" min="0" max="20" value="4.5" step="0.1">
                <div class="range-labels">
                    <span>0%</span>
                    <span>20%</span>
                </div>
            </div>
        </div>

        <div class="field">
            <div class="field-title-row">
                <div>
                    <div class="field-label">🔴 상환 타입 선택</div>
                    <div class="field-help">상환 방식을 선택하세요.</div>
                </div>
            </div>

            <div class="repayment-list">
                <label class="repayment-option">
                    <input type="radio" name="repayment" value="annuity" checked>
                    <div class="repayment-card">
                        <div class="type-ball"></div>
                        <div>
                            <div class="repayment-name">원리금균등분할상환</div>
                            <div class="repayment-desc">매월 비슷한 금액을 납부합니다.</div>
                        </div>
                    </div>
                </label>

                <label class="repayment-option">
                    <input type="radio" name="repayment" value="principal">
                    <div class="repayment-card">
                        <div class="type-ball"></div>
                        <div>
                            <div class="repayment-name">원금균등분할상환</div>
                            <div class="repayment-desc">매월 동일한 원금을 상환합니다.</div>
                        </div>
                    </div>
                </label>

                <label class="repayment-option">
                    <input type="radio" name="repayment" value="bullet">
                    <div class="repayment-card">
                        <div class="type-ball"></div>
                        <div>
                            <div class="repayment-name">만기일시상환</div>
                            <div class="repayment-desc">만기에 원금을 한 번에 상환합니다.</div>
                        </div>
                    </div>
                </label>
            </div>
        </div>

        <button id="calculateBtn" class="calculate-btn">⚡ 상환 플랜 계산하기</button>
        <div class="error" id="errorMessage"></div>
    </div>
</section>

<section class="card">
    <div class="result-title">
        <div class="result-title-left">
            <div class="dex-icon">#</div>
            <div>
                <h2>상환 도감</h2>
                <div class="result-subtitle">MY LOAN DATA</div>
            </div>
        </div>

        <div class="status-chip">
            <span class="status-dot"></span>
            계산 완료
        </div>
    </div>

    <div class="summary-grid">
        <div class="stat-card payment">
            <div class="stat-label">첫 번째 월 상환액</div>
            <div class="stat-value">
                <span id="firstPayment">0</span>
                <span class="stat-won">원</span>
            </div>
            <div class="stat-caption">1회차 기준 원금 + 이자</div>
        </div>

        <div class="stat-card interest">
            <div class="stat-label">총 예상 이자</div>
            <div class="stat-value">
                <span id="totalInterest">0</span>
                <span class="stat-won">원</span>
            </div>
            <div class="stat-caption">전체 기간 예상 이자 합계</div>
        </div>
    </div>

    <div class="loan-info">
        <span class="info-chip" id="infoPrincipal">대출금</span>
        <span class="info-chip" id="infoTerm">기간</span>
        <span class="info-chip" id="infoRate">금리</span>
        <span class="info-chip" id="infoType">상환방식</span>
    </div>

    <div class="schedule">
        <div class="schedule-heading">
            <strong>📘 월별 상환 스케줄</strong>
            <span id="scheduleCount">0회</span>
        </div>

        <div class="table-wrap">
            <table>
                <thead>
                    <tr>
                        <th>LV.</th>
                        <th>원금</th>
                        <th>이자</th>
                        <th>월 납입금</th>
                        <th>남은 대출금</th>
                    </tr>
                </thead>
                <tbody id="scheduleBody"></tbody>
            </table>
        </div>
    </div>

    <div class="notice">
        <div class="notice-icon">!</div>
        <div>
            본 계산기는 상담 및 예상 금액 확인을 위한 참고용 도구입니다.
            실제 상환금액은 대출 실행일, 납입일, 적용 금리, 금리변동,
            일수계산 방식 및 금융기관의 상품 조건에 따라 달라질 수 있습니다.
        </div>
    </div>
</section>

</div>
</main>

<script>
(() => {
"use strict";

const loanAmount = document.getElementById("loanAmount");
const amountRange = document.getElementById("amountRange");
const amountPreview = document.getElementById("amountPreview");

const loanTerm = document.getElementById("loanTerm");
const termRange = document.getElementById("termRange");
const monthBtn = document.getElementById("monthBtn");
const yearBtn = document.getElementById("yearBtn");
const termUnitLabel = document.getElementById("termUnitLabel");
const termMinLabel = document.getElementById("termMinLabel");
const termMaxLabel = document.getElementById("termMaxLabel");

const annualRate = document.getElementById("annualRate");
const rateRange = document.getElementById("rateRange");

const calculateBtn = document.getElementById("calculateBtn");
const errorMessage = document.getElementById("errorMessage");

const firstPayment = document.getElementById("firstPayment");
const totalInterest = document.getElementById("totalInterest");
const scheduleBody = document.getElementById("scheduleBody");
const scheduleCount = document.getElementById("scheduleCount");

const infoPrincipal = document.getElementById("infoPrincipal");
const infoTerm = document.getElementById("infoTerm");
const infoRate = document.getElementById("infoRate");
const infoType = document.getElementById("infoType");

let termUnit = "month";

const repaymentLabels = {
    annuity: "원리금균등분할상환",
    principal: "원금균등분할상환",
    bullet: "만기일시상환"
};

const formatter = new Intl.NumberFormat("ko-KR");

function formatNumber(value) {
    return formatter.format(Math.round(value));
}

function formatWon(value) {
    return `${formatNumber(value)}원`;
}

function clamp(value, min, max) {
    return Math.min(Math.max(value, min), max);
}

function getRepaymentType() {
    return document.querySelector('input[name="repayment"]:checked').value;
}

function getLoanMonths() {
    const term = Number(loanTerm.value);
    return termUnit === "year" ? Math.round(term * 12) : Math.round(term);
}

function showError(message) {
    errorMessage.textContent = message;
    errorMessage.style.display = "block";
}

function hideError() {
    errorMessage.style.display = "none";
}

function updateAmountPreview() {
    const manwon = Number(loanAmount.value) || 0;
    amountPreview.textContent = formatWon(manwon * 10000);
}

function syncAmount() {
    const value = Number(loanAmount.value);
    if (Number.isFinite(value)) {
        amountRange.value = clamp(
            value,
            Number(amountRange.min),
            Number(amountRange.max)
        );
    }
    updateAmountPreview();
}

function setTermUnit(unit) {
    if (unit === termUnit) return;

    if (unit === "year") {
        const months = Number(loanTerm.value) || 12;
        loanTerm.value = Math.max(1, Math.round(months / 12));
        termUnit = "year";
        loanTerm.min = 1;
        loanTerm.max = 30;
        termRange.min = 1;
        termRange.max = 30;
        termRange.value = loanTerm.value;
        termUnitLabel.textContent = "년";
        termMinLabel.textContent = "1년";
        termMaxLabel.textContent = "30년";
        monthBtn.classList.remove("active");
        yearBtn.classList.add("active");
    } else {
        const years = Number(loanTerm.value) || 1;
        loanTerm.value = Math.max(1, Math.round(years * 12));
        termUnit = "month";
        loanTerm.min = 1;
        loanTerm.max = 360;
        termRange.min = 1;
        termRange.max = 360;
        termRange.value = loanTerm.value;
        termUnitLabel.textContent = "개월";
        termMinLabel.textContent = "1개월";
        termMaxLabel.textContent = "360개월";
        yearBtn.classList.remove("active");
        monthBtn.classList.add("active");
    }

    calculate();
}

function validate() {
    const amount = Number(loanAmount.value);
    const months = getLoanMonths();
    const rate = Number(annualRate.value);

    if (!Number.isFinite(amount) || amount <= 0) {
        showError("대출 금액을 0보다 크게 입력해 주세요.");
        return false;
    }

    if (!Number.isFinite(months) || months < 1 || months > 360) {
        showError("대출 기간은 1개월 이상 360개월 이하로 입력해 주세요.");
        return false;
    }

    if (!Number.isFinite(rate) || rate < 0 || rate > 30) {
        showError("연 이자율은 0% 이상 30% 이하로 입력해 주세요.");
        return false;
    }

    hideError();
    return true;
}

function calculateAnnuity(principal, months, monthlyRate) {
    const schedule = [];
    let balance = principal;
    let standardPayment;

    if (monthlyRate === 0) {
        standardPayment = Math.round(principal / months);
    } else {
        const factor = Math.pow(1 + monthlyRate, months);
        standardPayment = Math.round(
            principal * monthlyRate * factor / (factor - 1)
        );
    }

    for (let i = 1; i <= months; i++) {
        const interest = Math.round(balance * monthlyRate);
        let principalPayment;
        let payment;

        if (i === months) {
            principalPayment = balance;
            payment = principalPayment + interest;
        } else {
            principalPayment = standardPayment - interest;
            principalPayment = Math.max(0, principalPayment);
            principalPayment = Math.min(principalPayment, balance);
            payment = principalPayment + interest;
        }

        balance -= principalPayment;

        if (Math.abs(balance) < 1) {
            balance = 0;
        }

        schedule.push({
            round: i,
            principal: principalPayment,
            interest,
            payment,
            balance
        });
    }

    return schedule;
}

function calculatePrincipal(principal, months, monthlyRate) {
    const schedule = [];
    let balance = principal;

    const standardPrincipal = Math.floor(principal / months);

    for (let i = 1; i <= months; i++) {
        const interest = Math.round(balance * monthlyRate);

        const principalPayment =
            i === months
                ? balance
                : Math.min(standardPrincipal, balance);

        const payment = principalPayment + interest;

        balance -= principalPayment;

        if (Math.abs(balance) < 1) {
            balance = 0;
        }

        schedule.push({
            round: i,
            principal: principalPayment,
            interest,
            payment,
            balance
        });
    }

    return schedule;
}

function calculateBullet(principal, months, monthlyRate) {
    const schedule = [];
    let balance = principal;

    for (let i = 1; i <= months; i++) {
        const interest = Math.round(balance * monthlyRate);
        const principalPayment = i === months ? principal : 0;
        const payment = principalPayment + interest;

        if (i === months) {
            balance = 0;
        }

        schedule.push({
            round: i,
            principal: principalPayment,
            interest,
            payment,
            balance
        });
    }

    return schedule;
}

function renderSchedule(schedule) {
    const fragment = document.createDocumentFragment();

    schedule.forEach(item => {
        const row = document.createElement("tr");
        row.innerHTML = `
            <td>${item.round}</td>
            <td>${formatNumber(item.principal)}원</td>
            <td>${formatNumber(item.interest)}원</td>
            <td class="payment-cell">${formatNumber(item.payment)}원</td>
            <td>${formatNumber(item.balance)}원</td>
        `;
        fragment.appendChild(row);
    });

    scheduleBody.innerHTML = "";
    scheduleBody.appendChild(fragment);
}

function calculate() {
    if (!validate()) return;

    const principal = Math.round(Number(loanAmount.value) * 10000);
    const months = getLoanMonths();
    const rate = Number(annualRate.value);
    const monthlyRate = rate / 100 / 12;
    const type = getRepaymentType();

    let schedule;

    if (type === "annuity") {
        schedule = calculateAnnuity(principal, months, monthlyRate);
    } else if (type === "principal") {
        schedule = calculatePrincipal(principal, months, monthlyRate);
    } else {
        schedule = calculateBullet(principal, months, monthlyRate);
    }

    const totalInterestValue = schedule.reduce(
        (sum, row) => sum + row.interest,
        0
    );

    const firstPaymentValue = schedule.length ? schedule[0].payment : 0;

    firstPayment.textContent = formatNumber(firstPaymentValue);
    totalInterest.textContent = formatNumber(totalInterestValue);

    infoPrincipal.textContent = `💰 ${formatWon(principal)}`;
    infoTerm.textContent = `⏱ ${months}개월`;
    infoRate.textContent = `⚡ 연 ${rate}%`;
    infoType.textContent = `🔴 ${repaymentLabels[type]}`;

    scheduleCount.textContent = `${months}회`;
    renderSchedule(schedule);
}

loanAmount.addEventListener("input", () => {
    syncAmount();
    calculate();
});

amountRange.addEventListener("input", () => {
    loanAmount.value = amountRange.value;
    updateAmountPreview();
    calculate();
});

document.querySelectorAll(".quick-btn").forEach(button => {
    button.addEventListener("click", () => {
        const amount = Number(button.dataset.amount);
        loanAmount.value = amount;
        amountRange.value = clamp(
            amount,
            Number(amountRange.min),
            Number(amountRange.max)
        );
        updateAmountPreview();
        calculate();
    });
});

loanTerm.addEventListener("input", () => {
    const value = Number(loanTerm.value);

    if (Number.isFinite(value)) {
        termRange.value = clamp(
            value,
            Number(termRange.min),
            Number(termRange.max)
        );
    }

    calculate();
});

termRange.addEventListener("input", () => {
    loanTerm.value = termRange.value;
    calculate();
});

monthBtn.addEventListener("click", () => {
    setTermUnit("month");
});

yearBtn.addEventListener("click", () => {
    setTermUnit("year");
});

annualRate.addEventListener("input", () => {
    const value = Number(annualRate.value);

    if (Number.isFinite(value)) {
        rateRange.value = clamp(
            value,
            Number(rateRange.min),
            Number(rateRange.max)
        );
    }

    calculate();
});

rateRange.addEventListener("input", () => {
    annualRate.value = rateRange.value;
    calculate();
});

document
    .querySelectorAll('input[name="repayment"]')
    .forEach(input => {
        input.addEventListener("change", calculate);
    });

calculateBtn.addEventListener("click", calculate);

updateAmountPreview();
calculate();

})();
</script>

</body>
</html>
