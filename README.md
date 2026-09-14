[Uploading index.html…]()
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="健身工作台">
<meta name="theme-color" content="#000000">
<title>我的健身工作台</title>
<style>
  * { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }
  :root {
    --black:#000; --g900:#1A1A1A; --g700:#4A4A4A; --g500:#767676;
    --g300:#C4C4C4; --g200:#E8E8E8; --g100:#F4F4F4; --white:#fff;
  }
  body { font-family:-apple-system,BlinkMacSystemFont,"PingFang SC","Microsoft YaHei",sans-serif;
    background:var(--g100); color:var(--black); padding-bottom:80px; -webkit-font-smoothing:antialiased; }
  .header { background:var(--black); color:var(--white); padding:18px 16px 22px; }
  .header h1 { font-size:18px; font-weight:500; letter-spacing:.5px; }
  .header .sub { font-size:11.5px; opacity:.65; margin-top:5px; }
  .streak-pill { display:inline-flex; align-items:center; gap:5px; background:rgba(255,255,255,.14);
    padding:5px 11px; border-radius:20px; font-size:11.5px; margin-top:9px; }
  .streak-pill .flame { font-size:13px; }

  .kpi-grid { display:grid; grid-template-columns:1fr 1fr; gap:10px; padding:0 14px; margin-top:-14px; }
  .kpi { background:var(--white); border:1px solid var(--g200); border-radius:12px; padding:14px; }
  .kpi .label { font-size:10.5px; color:var(--g500); letter-spacing:.5px; }
  .kpi .value { font-size:25px; font-weight:500; margin-top:4px; letter-spacing:-.5px; }
  .kpi .value small { font-size:11.5px; color:var(--g500); margin-left:2px; font-weight:400; }
  .kpi .delta { font-size:11px; margin-top:4px; color:var(--g500); }

  .section { background:var(--white); border:1px solid var(--g200); border-radius:12px; margin:12px 14px; padding:16px; }
  .section h2 { font-size:14px; font-weight:500; margin-bottom:13px; display:flex; align-items:center; justify-content:space-between; }
  .section h2 .tag { font-size:10px; background:var(--black); color:var(--white); padding:3px 8px; border-radius:20px; }

  .progress-bar { background:var(--g200); border-radius:20px; height:8px; overflow:hidden; }
  .progress-fill { background:var(--black); height:100%; transition:width .5s; }
  .progress-labels { display:flex; justify-content:space-between; font-size:11px; color:var(--g500); margin-top:8px; }

  .chart-box { width:100%; height:160px; margin:4px 0; }
  .insight-row { display:flex; justify-content:space-around; text-align:center; padding:12px 0 2px; border-top:1px solid var(--g200); margin-top:10px; }
  .insight-num { font-size:21px; font-weight:500; letter-spacing:-.5px; }
  .insight-row .lbl { font-size:10.5px; color:var(--g500); margin-top:3px; }

  .advice-item { padding:11px 13px; background:var(--g100); border-left:2px solid var(--black);
    border-radius:0 6px 6px 0; margin-bottom:8px; font-size:13px; color:var(--g700); line-height:1.65; }
  .advice-item b { color:var(--black); font-weight:500; }

  .cal-grid { display:grid; grid-template-columns:repeat(7,1fr); gap:5px; margin-top:4px; }
  .cal-cell { aspect-ratio:1; border-radius:5px; background:var(--g200); display:flex; align-items:center;
    justify-content:center; font-size:9.5px; color:var(--g500); }
  .cal-cell.done { background:var(--black); color:var(--white); }
  .cal-cell.today { border:1.5px solid var(--black); }
  .cal-head { display:grid; grid-template-columns:repeat(7,1fr); gap:5px; margin-bottom:5px; }
  .cal-head div { text-align:center; font-size:9.5px; color:var(--g500); }

  .badge-grid { display:grid; grid-template-columns:repeat(3,1fr); gap:10px; }
  .badge { text-align:center; padding:13px 6px; border:1px solid var(--g200); border-radius:11px; background:var(--white); }
  .badge.on { border-color:var(--black); background:var(--black); color:var(--white); }
  .badge .bicon { font-size:22px; filter:grayscale(1); opacity:.35; }
  .badge.on .bicon { filter:none; opacity:1; }
  .badge .bname { font-size:11px; margin-top:6px; }
  .badge .bdesc { font-size:9.5px; opacity:.6; margin-top:2px; }

  .week-cmp { display:flex; justify-content:space-between; padding:11px 0; border-bottom:1px solid var(--g200); font-size:13px; }
  .week-cmp:last-child { border-bottom:none; }
  .week-cmp .wl { color:var(--g500); font-size:12.5px; }
  .week-cmp .wv { font-weight:500; }
  .week-cmp .wc { font-size:11.5px; color:var(--g500); }

  .field label { display:block; font-size:10.5px; color:var(--g500); margin-bottom:5px; }
  .field input, .field select { width:100%; padding:10px 12px; border:1px solid var(--g200); border-radius:9px;
    font-size:15px; background:var(--white); outline:none; font-family:inherit; }
  .field input:focus, .field select:focus { border-color:var(--black); }
  .form-row { display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-bottom:11px; }
  .form-row.three { grid-template-columns:1fr 1fr 1fr; }

  .btn { width:100%; padding:13px; background:var(--black); color:var(--white); border:none; border-radius:10px;
    font-size:14px; font-weight:500; cursor:pointer; font-family:inherit; }
  .btn:active { opacity:.8; }
  .btn.secondary { background:var(--white); color:var(--black); border:1px solid var(--g300); }

  .search-box { width:100%; padding:11px 14px; border:1px solid var(--g200); border-radius:10px;
    font-size:14px; margin-bottom:12px; outline:none; font-family:inherit; }
  .search-box:focus { border-color:var(--black); }
  .chips { display:flex; gap:7px; overflow-x:auto; padding-bottom:10px; margin-bottom:4px; -webkit-overflow-scrolling:touch; }
  .chips::-webkit-scrollbar { display:none; }
  .chip { flex:0 0 auto; padding:7px 13px; border:1px solid var(--g200); border-radius:20px;
    font-size:12px; color:var(--g700); cursor:pointer; background:var(--white); white-space:nowrap; }
  .chip.active { background:var(--black); color:var(--white); border-color:var(--black); }

  .food-item { display:flex; justify-content:space-between; align-items:center; padding:11px 0; border-bottom:1px solid var(--g200); }
  .food-item:last-child { border-bottom:none; }
  .food-name { font-size:14px; display:flex; align-items:center; gap:5px; }
  .food-meta { font-size:11px; color:var(--g500); margin-top:2px; }
  .food-right { display:flex; align-items:center; gap:8px; }
  .food-kcal { font-size:15px; font-weight:500; text-align:right; }
  .food-kcal small { font-size:10px; color:var(--g500); font-weight:400; display:block; }
  .icon-btn { width:26px; height:26px; border:1px solid var(--g300); border-radius:50%; display:flex;
    align-items:center; justify-content:center; font-size:12px; cursor:pointer; flex:0 0 auto; }
  .icon-btn.add { border-color:var(--black); font-size:16px; }
  .icon-btn.add:active { background:var(--black); color:var(--white); }
  .icon-btn.fav-on { background:var(--black); color:var(--white); border-color:var(--black); }

  .today-bar { background:var(--black); color:var(--white); border-radius:10px; padding:13px 15px;
    margin-bottom:14px; display:flex; justify-content:space-between; align-items:center; }
  .today-bar .num { font-size:19px; font-weight:500; }
  .today-bar .lbl { font-size:10.5px; opacity:.65; margin-top:2px; }

  .log-item { display:flex; justify-content:space-between; align-items:center; padding:11px 0; border-bottom:1px solid var(--g200); font-size:14px; }
  .log-item:last-child { border-bottom:none; }
  .log-sub { font-size:11px; color:var(--g500); margin-top:2px; }
  .log-del { font-size:11px; color:var(--g500); cursor:pointer; padding:4px 8px; border:1px solid var(--g200); border-radius:6px; }

  .tab-bar { position:fixed; bottom:0; left:0; right:0; background:var(--white); display:flex;
    border-top:1px solid var(--g200); padding:6px 0 max(6px,env(safe-area-inset-bottom)); }
  .tab { flex:1; text-align:center; padding:6px 0; font-size:10px; color:var(--g500); cursor:pointer; }
  .tab.active { color:var(--black); }
  .tab .icon { display:block; font-size:16px; margin-bottom:3px; }

  .hidden { display:none; }
  .empty { text-align:center; color:var(--g500); font-size:12.5px; padding:20px 0; }
  .hint { font-size:11.5px; color:var(--g500); line-height:1.7; }
  .hint b { color:var(--black); font-weight:500; }

  .toast { position:fixed; top:16px; left:50%; transform:translateX(-50%); background:var(--black);
    color:var(--white); padding:11px 20px; border-radius:22px; font-size:13px; z-index:1000;
    opacity:0; transition:opacity .3s; pointer-events:none; }
  .toast.show { opacity:1; }
  .unlock { position:fixed; top:0; left:0; right:0; bottom:0; background:rgba(0,0,0,.5); display:flex;
    align-items:center; justify-content:center; z-index:2000; opacity:0; pointer-events:none; transition:opacity .3s; }
  .unlock.show { opacity:1; pointer-events:auto; }
  .unlock-card { background:var(--white); border-radius:16px; padding:28px 30px; text-align:center; transform:scale(.85); transition:transform .3s; }
  .unlock.show .unlock-card { transform:scale(1); }
  .unlock-card .uicon { font-size:44px; }
  .unlock-card .utitle { font-size:12px; color:var(--g500); margin-top:10px; letter-spacing:1px; }
  .unlock-card .uname { font-size:17px; font-weight:500; margin-top:5px; }
  .unlock-card .udesc { font-size:12px; color:var(--g500); margin-top:7px; }
</style>
</head>
<body>

<div class="header">
  <h1>我的健身工作台</h1>
  <div class="sub" id="headerSub">体重 · 饮食 · AI 预测</div>
  <div class="streak-pill"><span class="flame">🔥</span><span id="streakText">连续 0 天</span></div>
</div>

<!-- 概览 -->
<div id="tab-home">
  <div class="kpi-grid">
    <div class="kpi"><div class="label">当前体重</div>
      <div class="value"><span id="kpiWeight">--</span><small>kg</small></div>
      <div class="delta" id="kpiWeightDelta"></div></div>
    <div class="kpi"><div class="label">目标完成度</div>
      <div class="value"><span id="kpiProgress">--</span><small>%</small></div>
      <div class="delta" id="kpiGoalText"></div></div>
  </div>

  <div class="section">
    <h2>体重趋势 <span class="tag" id="trendTag"></span></h2>
    <div class="chart-box" id="chart"></div>
    <div class="insight-row">
      <div><div class="insight-num" id="insightWeekly">--</div><div class="lbl">周变化 kg</div></div>
      <div><div class="insight-num" id="insight30d">--</div><div class="lbl">30天后</div></div>
      <div><div class="insight-num" id="insightEta">--</div><div class="lbl">达标周数</div></div>
    </div>
  </div>

  <div class="section">
    <h2>目标进度</h2>
    <div class="progress-bar"><div class="progress-fill" id="goalFill" style="width:0%"></div></div>
    <div class="progress-labels"><span id="goalFrom">--</span><span id="goalTo">--</span></div>
  </div>

  <div class="section">
    <h2>打卡日历 <span class="tag" id="calTag"></span></h2>
    <div class="cal-head"><div>一</div><div>二</div><div>三</div><div>四</div><div>五</div><div>六</div><div>日</div></div>
    <div class="cal-grid" id="calGrid"></div>
  </div>

  <div class="section">
    <h2>AI 建议</h2>
    <div id="adviceBox"></div>
  </div>
</div>

<!-- 记录 -->
<div id="tab-log" class="hidden">
  <div class="section">
    <h2>今日记录</h2>
    <div class="field" style="margin-bottom:12px"><label>日期</label><input type="date" id="logDate"></div>
    <div class="form-row">
      <div class="field"><label>体重 (kg)</label><input type="number" step="0.1" id="logWeight" placeholder="55.5"></div>
      <div class="field"><label>热量 (kcal)</label><input type="number" id="logCal" placeholder="2200"></div>
    </div>
    <div class="form-row three">
      <div class="field"><label>蛋白质 g</label><input type="number" id="logProtein" placeholder="90"></div>
      <div class="field"><label>碳水 g</label><input type="number" id="logCarb" placeholder="250"></div>
      <div class="field"><label>脂肪 g</label><input type="number" id="logFat" placeholder="70"></div>
    </div>
    <button class="btn" onclick="saveLog()">保存记录</button>
  </div>
  <div class="section">
    <h2>历史记录</h2>
    <div id="logList"></div>
  </div>
</div>

<!-- 食物 -->
<div id="tab-food" class="hidden">
  <div class="section">
    <div class="today-bar">
      <div><div class="lbl">今日已摄入</div><div class="num" id="todayKcal">0 kcal</div></div>
      <div style="text-align:right"><div class="lbl">目标摄入</div><div class="num" id="targetKcal">-- kcal</div></div>
    </div>
    <input type="text" class="search-box" id="foodSearch" placeholder="搜索：米饭 / 奶茶 / 黄焖鸡" oninput="renderFood()">
    <div class="chips" id="foodChips"></div>
    <div id="foodList"></div>
  </div>
  <div class="section">
    <h2>增重点餐指南</h2>
    <div class="hint">
      · 主食别省：<b>米饭 / 面条 / 馒头</b> 是热量主力<br>
      · 蛋白优先：<b>鸡胸、牛肉、鸡蛋、虾、豆腐</b><br>
      · 加餐神器：<b>坚果、牛奶、香蕉、全麦面包</b><br>
      · 少喝含糖饮料，把热量留给固体食物<br>
      · 点 ⭐ 收藏常吃的，下次秒找
    </div>
  </div>
</div>

<!-- 周报 -->
<div id="tab-week" class="hidden">
  <div class="section">
    <h2>本周 vs 上周 <span class="tag" id="weekTag"></span></h2>
    <div id="weekCmp"></div>
  </div>
  <div class="section">
    <h2>AI 周总结</h2>
    <div id="weekAdvice"></div>
  </div>
  <div class="section">
    <h2>成就徽章 <span class="tag" id="badgeCount"></span></h2>
    <div class="badge-grid" id="badgeGrid"></div>
  </div>
</div>

<!-- 设置 -->
<div id="tab-set" class="hidden">
  <div class="section">
    <h2>我的资料</h2>
    <div class="form-row">
      <div class="field"><label>起始体重 (kg)</label><input type="number" step="0.1" id="setStart"></div>
      <div class="field"><label>目标体重 (kg)</label><input type="number" step="0.1" id="setGoal"></div>
    </div>
    <div class="form-row">
      <div class="field"><label>身高 (cm)</label><input type="number" id="setHeight"></div>
      <div class="field"><label>年龄</label><input type="number" id="setAge"></div>
    </div>
    <div class="form-row">
      <div class="field"><label>性别</label><select id="setSex"><option value="male">男</option><option value="female">女</option></select></div>
      <div class="field"><label>目标日期</label><input type="date" id="setTarget"></div>
    </div>
    <button class="btn" onclick="saveProfile()">保存资料</button>
  </div>
  <div class="section">
    <h2>数据管理</h2>
    <button class="btn secondary" onclick="exportData()">导出备份</button>
    <button class="btn secondary" style="margin-top:10px" onclick="document.getElementById('importFile').click()">导入数据</button>
    <input type="file" id="importFile" class="hidden" accept=".json" onchange="importData(event)">
    <button class="btn secondary" style="margin-top:10px" onclick="clearData()">清空记录</button>
  </div>
  <div class="section">
    <h2>使用说明</h2>
    <div class="hint">
      · 数据存<b>本浏览器</b>，换设备用导出/导入<br>
      · 记录越多，AI 预测和建议越准<br>
      · 「周报」页每周自动生成对比和总结<br>
      · 记得<b>定期导出备份</b>
    </div>
  </div>
</div>

<div class="tab-bar">
  <div class="tab active" id="t-home" onclick="switchTab('home')"><span class="icon">▤</span>概览</div>
  <div class="tab" id="t-log" onclick="switchTab('log')"><span class="icon">✎</span>记录</div>
  <div class="tab" id="t-food" onclick="switchTab('food')"><span class="icon">☰</span>食物</div>
  <div class="tab" id="t-week" onclick="switchTab('week')"><span class="icon">◫</span>周报</div>
  <div class="tab" id="t-set" onclick="switchTab('set')"><span class="icon">⚙</span>设置</div>
</div>

<div class="toast" id="toast"></div>
<div class="unlock" id="unlockModal" onclick="this.classList.remove('show')">
  <div class="unlock-card">
    <div class="uicon" id="uIcon">🏆</div>
    <div class="utitle">解锁新成就</div>
    <div class="uname" id="uName"></div>
    <div class="udesc" id="uDesc"></div>
  </div>
</div>

<script>
const KEY='my_fitness_dashboard_v2';
const DEFAULT={
  profile:{name:'我',start_weight:55,goal_weight:63,start_date:'2026-09-14',
           target_date:'2026-12-13',height_cm:178,age:22,sex:'male'},
  logs:[
    {date:'2026-09-09',weight:55.0,calories:1850,protein:85},
    {date:'2026-09-10',weight:55.05,calories:1850,protein:85},
    {date:'2026-09-11',weight:55.1,calories:1850,protein:85},
    {date:'2026-09-12',weight:55.15,calories:1850,protein:85},
    {date:'2026-09-13',weight:55.2,calories:1850,protein:85},
  ],
  badges:[], favorites:[]
};

const FOODS={
'主食':[['米饭','1碗 150g',175,4],['白米饭(大)','1大碗 250g',290,7],['白粥','1碗',130,3],
  ['馒头','1个 100g',220,7],['花卷','1个',210,6],['面条','1碗 200g',280,9],
  ['拉面','1碗',450,20],['炒面','1份',500,15],['全麦面包','1片 35g',80,4],
  ['吐司','1片',75,2.5],['红薯','1个 150g',130,2],['玉米','1根 200g',110,4],
  ['饺子','10个',350,15],['包子','1个 100g',200,8],['小笼包','8个',400,20],
  ['馄饨','10个',300,14],['蛋炒饭','1份 400g',500,14],['盖浇饭','1份',600,25],
  ['燕麦','40g 干重',150,5],['小米粥','1碗',120,3],['意面','1份 200g',320,11],
  ['乌冬面','1碗',320,10],['河粉','1份',400,10],['米粉','1碗',350,8],
  ['糯米鸡','1个',350,14],['烧饼','1个',250,7],['油条','1根',230,5],
  ['手抓饼','1个',350,8],['凉皮','1份',350,7],['热干面','1碗',450,14]],
'早餐':[['豆浆','250ml 无糖',80,7],['甜豆浆','250ml',130,7],['茶叶蛋','1个',80,7],
  ['煎蛋','1个',110,8],['蒸饺','8个',300,14],['肠粉','1份',350,12],
  ['饭团','1个',250,7],['三明治','1个',320,15],['汉堡早餐','1个',350,16],
  ['生煎包','4个',320,14],['煎饼果子','1个',400,12],['豆腐脑','1碗',120,9],
  ['胡辣汤','1碗',200,8],['碱水粽','1个',250,6]],
'肉蛋':[['鸡胸肉','100g',165,31],['鸡腿','1个 120g',180,22],['鸡翅','1个 50g',90,8],
  ['猪里脊','100g',155,20],['五花肉','100g',340,13],['排骨','100g',280,18],
  ['红烧肉','100g',350,12],['牛排','100g',125,26],['牛肉(瘦)','100g',106,20],
  ['牛肉干','50g',180,20],['羊肉','100g',200,20],['培根','1片',60,4],
  ['火腿肠','1根',150,7],['午餐肉','100g',230,12],['鸡蛋','1个 50g',70,6],
  ['蛋白','1个',17,4],['豆腐','100g',80,8],['豆干','100g',140,16],
  ['腐竹','100g',460,44],['鸡米花','1份 100g',280,15],['肉丸','100g',200,14]],
'水产':[['三文鱼','100g',140,20],['虾','100g',100,20],['基围虾','100g',100,18],
  ['鱼豆腐','100g',150,12],['带鱼','100g',130,18],['鲈鱼','100g',105,18],
  ['金枪鱼','100g',100,22],['鱿鱼','100g',85,17],['扇贝','100g',80,15],
  ['花甲','100g',60,10],['小龙虾','100g',100,16],['鳕鱼','100g',90,18]],
'蔬菜':[['西兰花','100g',35,3],['菠菜','100g',25,3],['白菜','100g',20,1.5],
  ['黄瓜','100g',15,0.8],['番茄','100g',20,1],['土豆','100g',80,2],
  ['胡萝卜','100g',40,1],['生菜','100g',15,1.4],['蘑菇','100g',25,3],
  ['青椒','100g',25,1.4],['茄子','100g',25,1],['豆芽','100g',30,3],
  ['金针菇','100g',30,2.5],['韭菜','100g',25,2],['洋葱','100g',40,1],
  ['南瓜','100g',25,1],['秋葵','100g',30,2],['海带','100g',20,1.5],
  ['木耳','100g',25,3],['笋','100g',25,2.5],['芋头','100g',80,2],['山药','100g',55,2]],
'外卖':[['巨无霸','1个',550,25],['汉堡(普通)','1个',300,15],['炸鸡','1块',250,15],
  ['薯条','中份',340,4],['披萨','1片',250,12],['麻辣烫','1份 500g',600,25],
  ['黄焖鸡米饭','1份',650,35],['兰州拉面','1碗',450,20],['螺蛳粉','1碗',400,12],
  ['肉夹馍','1个',400,18],['沙县拌面','1份',450,14],['麻辣香锅','1份',700,30],
  ['寿司','6个',300,12],['烤肉拌饭','1份',700,35],['酸菜鱼饭','1份',600,40],
  ['石锅拌饭','1份',550,20],['咖喱饭','1份',650,25],['煲仔饭','1份',600,25],
  ['意面外卖','1份',550,20],['炸鸡桶','2块',500,30],['塔可','1个',200,10],
  ['炸酱面','1碗',500,18],['炒河粉','1份',550,15],['蛋包饭','1份',550,20],
  ['烤鸭卷','1个',350,18],['关东煮','1份',300,15],['便当(普通)','1份',700,30]],
'火锅':[['火锅(清汤)','1餐',800,40],['火锅(麻辣)','1餐',1100,45],['肥牛','100g',200,18],
  ['肥羊','100g',220,18],['毛肚','100g',90,14],['鸭肠','100g',100,13],
  ['虾滑','100g',120,15],['午餐肉(锅)','100g',230,12],['冻豆腐','100g',100,10],
  ['宽粉','100g',150,1],['羊肉串','1串',70,6],['牛肉串','1串',70,7],
  ['烤茄子','1份',150,3],['烤韭菜','1份',80,3],['烤玉米','1根',150,5],
  ['烤翅中','1串',90,8],['芝麻酱','1勺',100,3],['香油碟','1份',200,1]],
'饮品':[['可乐','330ml',140,0],['无糖可乐','330ml',0,0],['雪碧','330ml',140,0],
  ['橙汁','250ml',110,2],['苹果汁','250ml',115,0.5],['美式咖啡','1杯',10,0],
  ['拿铁','中杯',150,8],['卡布奇诺','中杯',120,7],['牛奶','250ml',150,8],
  ['脱脂牛奶','250ml',85,8],['运动饮料','500ml',120,0],['矿泉水','500ml',0,0],
  ['柠檬水','500ml',20,0],['啤酒','330ml',140,1],['白酒','50ml',150,0],
  ['红酒','150ml',125,0],['威士忌','45ml',110,0],['豆浆(瓶装)','300ml',120,10],
  ['椰奶','250ml',180,2],['酸奶饮品','250ml',180,6]],
'奶茶':[['全糖奶茶','500ml',350,3],['半糖奶茶','500ml',250,3],['无糖奶茶','500ml',150,3],
  ['珍珠奶茶','700ml',550,5],['芋泥波波','700ml',600,7],['杨枝甘露','500ml',450,5],
  ['水果茶','500ml',250,2],['纯茶(无糖)','500ml',5,0],['奶盖茶','500ml',400,5],
  ['黑糖珍珠','700ml',600,6],['芝士葡萄','500ml',400,4],['柠檬茶','500ml',200,1],
  ['珍珠(加料)','1份',100,1],['椰果(加料)','1份',60,0]],
'水果':[['苹果','1个 中等',95,0.5],['香蕉','1根',105,1.3],['橙子','1个',70,1.3],
  ['西瓜','1块 200g',60,1],['葡萄','100g',70,0.5],['草莓','100g',35,1],
  ['蓝莓','100g',60,0.7],['芒果','1个',135,2],['梨','1个',100,0.5],
  ['猕猴桃','1个',50,1],['菠萝','100g',50,0.5],['桃子','1个',60,1],
  ['火龙果','1个',120,2],['车厘子','100g',65,1],['榴莲','100g',150,3]],
'零食':[['薯片','1包 70g',380,4],['巧克力','50g',270,3],['坚果','30g',180,6],
  ['混合坚果','1包 25g',155,5],['饼干','2片',100,2],['蛋糕','1块',300,4],
  ['冰淇淋','1个',200,4],['酸奶(加糖)','100g',90,3],['希腊酸奶','100g',60,10],
  ['肉脯','50g',180,15],['辣条','1包 80g',400,8],['蛋卷','2根',120,2],
  ['软糖','50g',180,2],['花生','50g',300,13],['瓜子','50g',300,12],
  ['面包(甜)','1个',250,7],['蛋挞','1个',220,5],['凤梨酥','1个',180,2]],
'便利':[['饭团','1个',200,6],['三明治(便利)','1个',300,14],['便当(便利)','1份',650,28],
  ['关东煮(3串)','3串',200,12],['包子(便利)','1个',200,8],['玉米(便利)','1根',200,6],
  ['茶叶蛋(便利)','1个',80,7],['咖啡(罐装)','1罐',120,3],['能量棒','1根',220,10],
  ['蛋白棒','1根',200,20],['鸡胸肉即食','100g',130,25]]
};

const BADGES=[
  ['🌱','初出茅庐','完成第一次记录', d=>d.logs.length>=1],
  ['📅','三日之约','累计记录 3 天', d=>d.logs.length>=3],
  ['🔥','七日成习','累计记录 7 天', d=>d.logs.length>=7],
  ['📊','数据达人','累计记录 20 天', d=>d.logs.length>=20],
  ['👑','百日坚持','累计记录 50 天', d=>d.logs.length>=50],
  ['💪','蛋白达标','连续 3 天蛋白质达标', d=>{
    const t=(latestW(d)||0)*1.6; let c=0;
    const s=d.logs.slice().sort((a,b)=>b.date.localeCompare(a.date));
    for(const l of s){ if(l.protein!=null&&l.protein>=t*0.9) c++; else break; }
    return c>=3 && t>0; }],
  ['🍽️','热量盈余','单日摄入超 2400 kcal', d=>d.logs.some(l=>(l.calories||0)>=2400)],
  ['⚖️','初见成效','体重上升 0.5 kg', d=>{
    const w=d.logs.filter(l=>l.weight!=null).sort((a,b)=>a.date.localeCompare(b.date));
    return w.length>=2 && (w[w.length-1].weight-w[0].weight)>=0.5; }],
  ['🎯','小目标','体重上升 1 kg', d=>{
    const w=d.logs.filter(l=>l.weight!=null).sort((a,b)=>a.date.localeCompare(b.date));
    return w.length>=2 && (w[w.length-1].weight-w[0].weight)>=1; }],
  ['🏆','达成目标','达到目标体重', d=>{
    const w=latestW(d); return w!=null && d.profile.goal_weight && w>=d.profile.goal_weight-0.3; }],
  ['🧮','全餐记录','单日完整记录体重+热量+蛋白', d=>d.logs.some(l=>l.weight!=null&&l.calories!=null&&l.protein!=null)],
  ['🥗','饮食专家','累计记录 20 条饮食', d=>d.logs.filter(l=>l.calories!=null).length>=20]
];

function load(){
  try{
    let raw=localStorage.getItem(KEY);
    if(!raw){
      // 从 v1 迁移旧数据，避免升级丢记录
      const old=localStorage.getItem('my_fitness_dashboard_v1');
      if(old){
        try{
          const o=JSON.parse(old);
          const d={profile:o.profile||DEFAULT.profile, logs:o.logs||[], badges:[], favorites:[]};
          localStorage.setItem(KEY,JSON.stringify(d));
          return d;
        }catch(e){}
      }
      localStorage.setItem(KEY,JSON.stringify(DEFAULT));
      return JSON.parse(JSON.stringify(DEFAULT));
    }
    const d=JSON.parse(raw);
    if(!d.badges) d.badges=[]; if(!d.favorites) d.favorites=[];
    return d;
  }catch(e){ return JSON.parse(JSON.stringify(DEFAULT)); }
}
function save(d){ localStorage.setItem(KEY,JSON.stringify(d)); }
let DATA=load();

function toast(m){ const t=document.getElementById('toast'); t.textContent=m; t.classList.add('show'); setTimeout(()=>t.classList.remove('show'),1700); }
function today(){ return new Date().toISOString().slice(0,10); }
function dd(a,b){ return Math.round((new Date(a)-new Date(b))/86400000); }
function latestW(d){ const w=d?d.logs.filter(l=>l.weight!=null).sort((a,b)=>b.date.localeCompare(a.date)):DATA.logs.filter(l=>l.weight!=null).sort((a,b)=>b.date.localeCompare(a.date)); return w.length?w[0].weight:null; }

function switchTab(n){
  ['home','log','food','week','set'].forEach(x=>{
    document.getElementById('tab-'+x).classList.toggle('hidden',x!==n);
    document.getElementById('t-'+x).classList.toggle('active',x===n);
  });
  if(n==='log') renderLogList();
  if(n==='food') renderFood();
  if(n==='week') renderWeek();
}

function streak(){
  const s=DATA.logs.map(l=>l.date).sort().reverse();
  if(!s.length) return 0;
  let c=0; const t=today();
  for(let i=0;i<400;i++){
    const d=new Date(); d.setDate(d.getDate()-i); const ds=d.toISOString().slice(0,10);
    if(s.includes(ds)) c++;
    else if(i>0) break;
    else if(!s.includes(t)) continue;
  }
  const has=s.includes(t);
  let n=0;
  const cur=new Date(); if(!has) cur.setDate(cur.getDate()-1);
  for(let i=0;i<400;i++){
    const ds=cur.toISOString().slice(0,10);
    if(s.includes(ds)){ n++; cur.setDate(cur.getDate()-1); } else break;
  }
  return n;
}

function checkBadges(){
  const newOnes=[];
  BADGES.forEach((b,i)=>{
    if(!DATA.badges.includes(i)){
      try{ if(b[3](DATA)){ DATA.badges.push(i); newOnes.push(b); } }catch(e){}
    }
  });
  if(newOnes.length){ save(DATA); newOnes.forEach((b,k)=>setTimeout(()=>showUnlock(b),k*900)); }
}
function showUnlock(b){
  document.getElementById('uIcon').textContent=b[0];
  document.getElementById('uName').textContent=b[1];
  document.getElementById('uDesc').textContent=b[2];
  const m=document.getElementById('unlockModal');
  m.classList.add('show');
  setTimeout(()=>m.classList.remove('show'),2600);
}

function predict(){
  const p=DATA.logs.filter(l=>l.weight!=null).sort((a,b)=>a.date.localeCompare(b.date));
  if(p.length<3) return {ok:false,n:p.length};
  const base=new Date(p[0].date);
  const xs=p.map(x=>dd(x.date,base)), ys=p.map(x=>x.weight), n=xs.length;
  const mx=xs.reduce((a,b)=>a+b,0)/n, my=ys.reduce((a,b)=>a+b,0)/n;
  let num=0,den=0;
  for(let i=0;i<n;i++){ num+=(xs[i]-mx)*(ys[i]-my); den+=(xs[i]-mx)**2; }
  const sl=den===0?0:num/den, it=my-sl*mx;
  const lw=ys[n-1], ld=xs[n-1];
  const weekly=sl*7, proj=it+sl*(ld+30);
  let eta=null; const g=DATA.profile.goal_weight;
  if(g&&sl!==0){ const d2=(g-lw)/sl; if(d2>0) eta=d2/7; }
  return {ok:true,n,weekly,proj,eta,lw,conf:n>=14?'高':n>=7?'中':'低',
    trend:weekly<-0.1?'下降':weekly>0.1?'上升':'持平'};
}

function tdeeVal(){
  const p=DATA.profile, w=latestW();
  if(w&&p.height_cm&&p.age&&p.sex){
    const bmr=10*w+6.25*p.height_cm-5*p.age+(p.sex==='male'?5:-161);
    return Math.round(bmr*1.2);
  }
  return null;
}

function advice(){
  const t=tdeeVal(), p=DATA.profile;
  const r=DATA.logs.filter(l=>dd(today(),l.date)<7);
  const cals=r.map(l=>l.calories).filter(x=>x!=null);
  const pros=r.map(l=>l.protein).filter(x=>x!=null);
  const ac=cals.length?cals.reduce((a,b)=>a+b,0)/cals.length:null;
  const ap=pros.length?pros.reduce((a,b)=>a+b,0)/pros.length:null;
  const w=latestW();
  const out=[];
  const target=t?t+400:null;
  if(t&&ac){
    const diff=Math.round(ac-t);
    if(diff>200) out.push(`近 7 天日均 <b>${Math.round(ac)} kcal</b>，高于消耗（${t}）约 <b>${diff}</b>。增重可以，但注意别全变成脂肪，力量训练跟上。`);
    else if(diff<-300) out.push(`近 7 天日均 <b>${Math.round(ac)} kcal</b>，比消耗（${t}）低 <b>${-diff}</b>。这个缺口会掉肌肉，至少吃到 <b>${t-300} kcal</b>。`);
    else out.push(`近 7 天日均 <b>${Math.round(ac)} kcal</b>，与消耗（${t}）基本持平，是<b>维持期</b>。想增重建议每天吃到 <b>${target} kcal</b>（消耗 +400 盈余）。`);
  } else if(!w) out.push('先记一条<b>体重</b>，才能给个性化建议。');
  else { const m=[]; if(!p.height_cm)m.push('身高'); if(!p.age)m.push('年龄');
    out.push(m.length?`补齐 <b>${m.join('、')}</b>（设置页）即可估算每日消耗。`:'多记几天数据，建议会更准。'); }
  if(w&&ap!=null){
    const tp=Math.round(w*1.6);
    if(ap<tp*0.8) out.push(`近 7 天日均蛋白质 <b>${Math.round(ap)} g</b>，低于建议 <b>${tp} g/天</b>（1.6 g/kg）。加餐试试：牛奶+鸡蛋，或即食鸡胸。`);
    else out.push(`近 7 天日均蛋白质 <b>${Math.round(ap)} g</b>，达标 ✓（目标 ${tp} g）。`);
  }
  const nw=DATA.logs.filter(l=>l.weight!=null).length;
  if(nw<7) out.push(`目前 <b>${nw} 条</b>体重记录，满 7 条后 AI 预测会开启。`);
  const st=streak();
  if(st>=3) out.push(`已连续打卡 <b>${st} 天</b>，节奏很好，保持住 💪`);
  return {out,t,ac:ac?Math.round(ac):null,target};
}

function renderWeek(){
  const now=new Date();
  const mk=i=>{const d=new Date(now); d.setDate(d.getDate()-i); return d.toISOString().slice(0,10);};
  const thisW=[],lastW=[];
  for(let i=0;i<7;i++) thisW.push(mk(i));
  for(let i=7;i<14;i++) lastW.push(mk(i));
  const pick=(ds,f)=>{const v=DATA.logs.filter(l=>ds.includes(l.date)).map(f).filter(x=>x!=null); return v.length?v.reduce((a,b)=>a+b,0)/v.length:null;};
  const tw=pick(thisW,l=>l.weight), lw=pick(lastW,l=>l.weight);
  const tc=pick(thisW,l=>l.calories), lc=pick(lastW,l=>l.calories);
  const tp=pick(thisW,l=>l.protein), lp=pick(lastW,l=>l.protein);
  const days=thisW.filter(d=>DATA.logs.some(l=>l.date===d)).length;
  document.getElementById('weekTag').textContent=`打卡 ${days}/7 天`;
  const clr=(a,b,inv)=>{
    if(a==null||b==null) return {txt:'—',c:'var(--g500)'};
    const d=a-b; const good=inv?d<0:d>0;
    return {txt:(d>=0?'+':'')+d.toFixed(1), c:Math.abs(d)<0.05?'var(--g500)':(good?'var(--black)':'var(--g500)')};
  };
  const wd=tw!=null&&lw!=null?(tw-lw):null;
  const rows=[];
  rows.push(['平均体重', tw!=null?tw.toFixed(2)+' kg':'—', wd!=null?(wd>=0?'+':'')+wd.toFixed(2)+' kg':'—']);
  rows.push(['平均热量', tc!=null?Math.round(tc)+' kcal':'—', tc!=null&&lc!=null?(tc-lc>=0?'+':'')+Math.round(tc-lc)+' kcal':'—']);
  rows.push(['平均蛋白质', tp!=null?Math.round(tp)+' g':'—', tp!=null&&lp!=null?(tp-lp>=0?'+':'')+Math.round(tp-lp)+' g':'—']);
  const t=tdeeVal();
  rows.push(['热量目标达成', t?(tc!=null?Math.round(tc/(t+400)*100)+'%':'—'):'—', t?`目标 ${t+400} kcal`:'补资料后显示']);
  rows.push(['本周打卡', days+' / 7 天', days>=5?'很稳':days>=3?'还行':'要加油']);
  document.getElementById('weekCmp').innerHTML=rows.map(r=>`<div class="week-cmp">
    <div class="wl">${r[0]}</div><div style="text-align:right"><div class="wv">${r[1]}</div><div class="wc">${r[2]}</div></div></div>`).join('');

  const wa=[];
  if(wd!=null){
    if(wd>0.2) wa.push(`本周体重较上周<b>上升 ${wd.toFixed(2)} kg</b>，方向对了，增肌期每周 +0.2~0.4 kg 是理想速度。`);
    else if(wd<-0.2) wa.push(`本周体重较上周<b>下降 ${Math.abs(wd).toFixed(2)} kg</b>。你在增重，要检查是不是吃少了。`);
    else wa.push(`本周体重基本持平，离目标还差一点推动力。`);
  } else wa.push('再记录几天，下周就能生成完整对比。');
  if(tc!=null&&t){
    if(tc<t) wa.push(`本周日均摄入低于消耗，<b>盈余不足</b>。建议每天多吃 1 份主食或加一次加餐（坚果+牛奶约 400 kcal）。`);
    else if(tc<t+200) wa.push(`本周摄入接近维持量，建议再<b>增加 300 kcal/天</b>，让盈余更明确。`);
    else wa.push(`本周摄入已形成盈余 ✓，配合力量训练效果更好。`);
  }
  const w=latestW();
  if(w&&tp!=null){ const need=Math.round(w*1.6);
    if(tp<need) wa.push(`蛋白质还差 <b>${Math.round(need-tp)} g/天</b>，等于 1 个鸡蛋 + 1 杯牛奶 + 100g 鸡胸。`); }
  if(days>=5) wa.push(`本周打卡 <b>${days}/7</b>，自律程度不错 👍`);
  else if(days<3) wa.push(`本周只打卡 <b>${days}</b> 天。建议固定时间：早上称体重、睡前补饮食，养成习惯。`);
  document.getElementById('weekAdvice').innerHTML=wa.map(s=>`<div class="advice-item">${s}</div>`).join('');

  document.getElementById('badgeCount').textContent=`${DATA.badges.length}/${BADGES.length}`;
  document.getElementById('badgeGrid').innerHTML=BADGES.map((b,i)=>{
    const on=DATA.badges.includes(i);
    return `<div class="badge${on?' on':''}"><div class="bicon">${on?b[0]:'🔒'}</div>
      <div class="bname">${b[1]}</div><div class="bdesc">${b[2]}</div></div>`;
  }).join('');
}

function renderChart(){
  const p=DATA.logs.filter(l=>l.weight!=null).sort((a,b)=>a.date.localeCompare(b.date));
  const box=document.getElementById('chart');
  if(p.length<2){ box.innerHTML='<div class="empty">记录 2 天以上显示趋势</div>'; return; }
  const W=340,H=160,pad=28;
  const ws=p.map(x=>x.weight);
  let mn=Math.min(...ws),mx=Math.max(...ws);
  if(mx-mn<1){mn-=0.5;mx+=0.5;}else{mn-=0.2;mx+=0.2;}
  const X=i=>pad+i*(W-2*pad)/(p.length-1), Y=w=>H-pad-(w-mn)*(H-2*pad)/(mx-mn);
  const line=p.map((x,i)=>`${i?'L':'M'}${X(i).toFixed(1)},${Y(x.weight).toFixed(1)}`).join(' ');
  const area=line+` L${X(p.length-1).toFixed(1)},${H-pad} L${X(0).toFixed(1)},${H-pad} Z`;
  let ci='',lb='';
  p.forEach((x,i)=>{
    ci+=`<circle cx="${X(i).toFixed(1)}" cy="${Y(x.weight).toFixed(1)}" r="3.2" fill="#fff" stroke="#000" stroke-width="1.8"/>`;
    if(i%Math.ceil(p.length/5)===0||i===p.length-1)
      lb+=`<text x="${X(i).toFixed(1)}" y="${H-7}" font-size="9" fill="#767676" text-anchor="middle">${x.date.slice(5)}</text>`;
  });
  const g=DATA.profile.goal_weight;
  const gy=(g>=mn&&g<=mx)?`<line x1="${pad}" y1="${Y(g).toFixed(1)}" x2="${W-pad}" y2="${Y(g).toFixed(1)}" stroke="#000" stroke-width="1" stroke-dasharray="3,3" opacity=".45"/>
    <text x="${W-pad}" y="${(Y(g)-5).toFixed(1)}" font-size="9" fill="#000" text-anchor="end" opacity=".6">目标 ${g}</text>`:'';
  box.innerHTML=`<svg viewBox="0 0 ${W} ${H}" style="width:100%;height:100%">
    <defs><linearGradient id="gg" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#000" stop-opacity=".10"/><stop offset="100%" stop-color="#000" stop-opacity="0"/></linearGradient></defs>
    <path d="${area}" fill="url(#gg)"/><path d="${line}" fill="none" stroke="#000" stroke-width="2.2" stroke-linejoin="round"/>
    ${gy}${ci}${lb}
    <text x="${pad}" y="13" font-size="9" fill="#767676">${mx.toFixed(1)}</text>
    <text x="${pad}" y="${H-pad+4}" font-size="9" fill="#767676">${mn.toFixed(1)}</text></svg>`;
}

function renderFood(){
  const chips=document.getElementById('foodChips');
  const cats=['⭐收藏'].concat(Object.keys(FOODS));
  if(!chips.dataset.init){
    chips.innerHTML=cats.map((c,i)=>`<div class="chip${i===0?' active':''}" data-cat="${c}" onclick="pickCat('${c}')">${c}</div>`).join('');
    chips.dataset.init='1';
  }
  const act=chips.querySelector('.chip.active');
  const cat=act?act.dataset.cat:'主食';
  const q=(document.getElementById('foodSearch').value||'').trim();
  let list=[];
  if(q){ Object.values(FOODS).forEach(a=>a.forEach(f=>{ if(f[0].includes(q)) list.push(f); })); }
  else if(cat==='⭐收藏'){
    list=[]; Object.values(FOODS).forEach(a=>a.forEach(f=>{ if(DATA.favorites.includes(f[0])) list.push(f); }));
  }
  else list=FOODS[cat]||[];
  const el=document.getElementById('foodList');
  if(!list.length){ el.innerHTML=`<div class="empty">${cat==='⭐收藏'?'还没有收藏，点 ⭐ 添加':'没找到「'+q+'」'}</div>`; return; }
  el.innerHTML=list.map(f=>{
    const fav=DATA.favorites.includes(f[0]);
    return `<div class="food-item"><div><div class="food-name">${f[0]}</div>
      <div class="food-meta">${f[1]} · 蛋白 ${f[3]}g</div></div>
      <div class="food-right">
        <div class="icon-btn${fav?' fav-on':''}" onclick="toggleFav('${f[0]}')">${fav?'★':'☆'}</div>
        <div class="food-kcal">${f[2]}<small>kcal</small></div>
        <div class="icon-btn add" onclick="addFood('${f[0]}',${f[2]},${f[3]})">+</div>
      </div></div>`;
  }).join('');
}
function pickCat(c){
  document.querySelectorAll('#foodChips .chip').forEach(el=>el.classList.toggle('active',el.dataset.cat===c));
  document.getElementById('foodSearch').value=''; renderFood();
}
function toggleFav(n){
  const i=DATA.favorites.indexOf(n);
  if(i>=0){ DATA.favorites.splice(i,1); toast('已取消收藏'); }
  else { DATA.favorites.push(n); toast('已收藏 '+n); }
  save(DATA); renderFood();
}
function addFood(n,k,p){
  const d=today();
  let l=DATA.logs.find(x=>x.date===d);
  if(!l){ l={date:d}; DATA.logs.push(l); }
  l.calories=(l.calories||0)+k; l.protein=(l.protein||0)+p;
  save(DATA); checkBadges(); render();
  toast('+'+k+' kcal · '+n);
}

function renderCal(){
  const g=document.getElementById('calGrid');
  const now=new Date();
  const start=new Date(now); start.setDate(start.getDate()-start.getDay()+1-28);
  let h='';
  for(let i=0;i<35;i++){
    const d=new Date(start); d.setDate(d.getDate()+i);
    const ds=d.toISOString().slice(0,10);
    const has=DATA.logs.some(l=>l.date===ds);
    const isT=ds===today();
    if(d<=now) h+=`<div class="cal-cell${has?' done':''}${isT?' today':''}">${d.getDate()}</div>`;
    else h+=`<div class="cal-cell" style="opacity:.35">${d.getDate()}</div>`;
  }
  g.innerHTML=h;
  const s=streak();
  document.getElementById('calTag').textContent=`连续 ${s} 天`;
}

function render(){
  const p=DATA.profile;
  const ws=DATA.logs.filter(l=>l.weight!=null).sort((a,b)=>b.date.localeCompare(a.date));
  const lw=ws.length?ws[0].weight:null;
  document.getElementById('kpiWeight').textContent=lw!=null?lw.toFixed(1):'--';
  if(ws.length>=2){
    const d=ws[0].weight-ws[1].weight;
    document.getElementById('kpiWeightDelta').textContent=(d>=0?'+':'')+d.toFixed(2)+' kg 较上次';
  }
  const pr=predict();
  if(pr.ok){
    document.getElementById('trendTag').textContent=`${pr.trend} · ${pr.conf}`;
    document.getElementById('insightWeekly').textContent=(pr.weekly>=0?'+':'')+pr.weekly.toFixed(2);
    document.getElementById('insight30d').textContent=pr.proj.toFixed(1);
    document.getElementById('insightEta').textContent=pr.eta!=null?pr.eta.toFixed(1):'—';
  } else {
    document.getElementById('trendTag').textContent=`需 ${3-pr.n} 条`;
    ['insightWeekly','insight30d','insightEta'].forEach(i=>document.getElementById(i).textContent='--');
  }
  if(lw!=null&&p.start_weight&&p.goal_weight){
    const tot=p.goal_weight-p.start_weight, done=lw-p.start_weight;
    const pct=tot!==0?Math.max(0,Math.min(100,done/tot*100)):0;
    document.getElementById('kpiProgress').textContent=pct.toFixed(1);
    document.getElementById('goalFill').style.width=pct+'%';
    document.getElementById('goalFrom').textContent=`起始 ${p.start_weight} kg`;
    document.getElementById('goalTo').textContent=`目标 ${p.goal_weight} kg`;
    document.getElementById('kpiGoalText').textContent=`还差 ${(p.goal_weight-lw).toFixed(1)} kg`;
  }
  const ad=advice();
  document.getElementById('adviceBox').innerHTML=ad.out.length?ad.out.map(s=>`<div class="advice-item">${s}</div>`).join(''):'<div class="empty">继续记录</div>';
  document.getElementById('headerSub').textContent=ad.t?`消耗 ${ad.t} · 摄入 ${ad.ac||'—'} kcal`:'体重 · 饮食 · AI 预测';
  const tl=DATA.logs.find(l=>l.date===today());
  document.getElementById('todayKcal').textContent=(tl&&tl.calories?tl.calories:0)+' kcal';
  document.getElementById('targetKcal').textContent=ad.target?ad.target+' kcal':'--';
  document.getElementById('streakText').textContent=`连续 ${streak()} 天`;
  renderChart(); renderCal(); renderLogList();
  if(!document.getElementById('tab-week').classList.contains('hidden')) renderWeek();
}

function renderLogList(){
  const l=DATA.logs.slice().sort((a,b)=>b.date.localeCompare(a.date));
  const el=document.getElementById('logList');
  if(!l.length){ el.innerHTML='<div class="empty">还没有记录</div>'; return; }
  el.innerHTML=l.map(x=>`<div class="log-item">
    <div><div>${x.date}</div><div class="log-sub">${x.calories?x.calories+' kcal':''}${x.protein?' · 蛋白 '+Math.round(x.protein)+'g':''}</div></div>
    <div style="display:flex;align-items:center;gap:10px">
      <span style="font-weight:500">${x.weight!=null?x.weight.toFixed(1)+' kg':'—'}</span>
      <span class="log-del" onclick="delLog('${x.date}')">删除</span></div></div>`).join('');
}

function saveLog(){
  const date=document.getElementById('logDate').value||today();
  const w=parseFloat(document.getElementById('logWeight').value);
  const c=parseInt(document.getElementById('logCal').value);
  const pp=parseFloat(document.getElementById('logProtein').value);
  const cb=parseFloat(document.getElementById('logCarb').value);
  const ft=parseFloat(document.getElementById('logFat').value);
  if(isNaN(w)&&isNaN(c)&&isNaN(pp)){ toast('至少填一项'); return; }
  let l=DATA.logs.find(x=>x.date===date);
  if(!l){ l={date}; DATA.logs.push(l); }
  if(!isNaN(w))l.weight=w; if(!isNaN(c))l.calories=c;
  if(!isNaN(pp))l.protein=pp; if(!isNaN(cb))l.carbs=cb; if(!isNaN(ft))l.fat=ft;
  save(DATA); checkBadges(); render();
  ['logWeight','logCal','logProtein','logCarb','logFat'].forEach(i=>document.getElementById(i).value='');
  toast('已保存 · 连续 '+streak()+' 天');
}
function delLog(d){ if(!confirm('删除 '+d+'？'))return; DATA.logs=DATA.logs.filter(x=>x.date!==d); save(DATA); render(); toast('已删除'); }
function saveProfile(){
  const p=DATA.profile;
  p.start_weight=parseFloat(document.getElementById('setStart').value)||p.start_weight;
  p.goal_weight=parseFloat(document.getElementById('setGoal').value)||p.goal_weight;
  p.height_cm=parseFloat(document.getElementById('setHeight').value)||p.height_cm;
  p.age=parseInt(document.getElementById('setAge').value)||p.age;
  p.sex=document.getElementById('setSex').value;
  p.target_date=document.getElementById('setTarget').value||p.target_date;
  save(DATA); render(); toast('资料已保存');
}
function exportData(){
  const b=new Blob([JSON.stringify(DATA,null,2)],{type:'application/json'});
  const a=document.createElement('a'); a.href=URL.createObjectURL(b);
  a.download='fitness-backup-'+today()+'.json'; a.click(); toast('已导出');
}
function importData(e){
  const f=e.target.files[0]; if(!f)return;
  const r=new FileReader();
  r.onload=ev=>{ try{ DATA=JSON.parse(ev.target.result); if(!DATA.badges)DATA.badges=[]; if(!DATA.favorites)DATA.favorites=[];
    save(DATA); fillSet(); render(); toast('导入成功'); }catch(x){ toast('文件格式错误'); } };
  r.readAsText(f);
}
function clearData(){ if(!confirm('清空所有记录？建议先导出备份。'))return;
  DATA={profile:DATA.profile,logs:[],badges:[],favorites:[]}; save(DATA); render(); toast('已清空'); }
function fillSet(){
  const p=DATA.profile;
  document.getElementById('setStart').value=p.start_weight??'';
  document.getElementById('setGoal').value=p.goal_weight??'';
  document.getElementById('setHeight').value=p.height_cm??'';
  document.getElementById('setAge').value=p.age??'';
  document.getElementById('setSex').value=p.sex??'male';
  document.getElementById('setTarget').value=p.target_date??'';
}
document.getElementById('logDate').value=today();
fillSet(); render(); checkBadges();
</script>
</body>
</html>
