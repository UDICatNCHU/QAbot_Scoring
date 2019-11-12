## QA機器人評分系統說明

- 新增之`questions_example.json`為提供測試之20題範例，其他題目皆以此邏輯出題。
- 網站已上線提供測試，共20題，一題5分滿分100分，正式demo當天會提供200題，一題0.5分。
- 請注意自己程式輸出之答案，**格式須符合規定，系統才能正確計算分數，demo當天亦如此。**
- **規定之JSON格式 : e.g. 第一題答案A，第二題答案B，第三題答案C，則最後答案之JSON格式應為 ["A", "B", "C"]**
- 答案範例 : ["A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A"]

---

- 評分網站: <http://140.120.13.243:8123/scoring/>

#### JSON讀取說明
- 例如題目之格式為：
```json
 {"Question":"中華民國第14任總統，民主進步黨第16屆黨主席，同時也是台灣歷史上首位女性元首，她是:" 
  , "A":"蔡正元"
  , "B":"蔡英文"
  , "C":"洪慈庸" },

  {"Question":"明末清初著名軍事將領，曾因「引清兵入關」而被世人斥責為漢奸，他的名字叫做:" 
  , "A":"吳一桂"
  , "B":"吳二桂"
  , "C":"吳三桂" }
```
- 首先使用python的open函式讀檔，python3的open函式可選擇編碼方式，由於python3的字串預設編碼都是unicode，而JSON的預設編碼是UTF-8，所以open時要告訴python這個字串是UTF-8編碼才能做後續的字串處理，程式碼如下:
```python
import json

with open('questions.json', 'r', encoding='UTF-8') as f:
	JsonList = json.load(f)
```

- 選擇**第一題的題目**的方法如下:
```python
print(JsonList[0]['Question'])
```
- 列印結果:
```
中華民國第14任總統，民主進步黨第16屆黨主席，同時也是台灣歷史上首位女性元首，她是:
```

#### 繳交答案網站使用說明
- 第一格填入學號，第二格填入你程式跑出的答案
- **答案請使用規定之JSON格式，例如: 第一題答案A，第二題答案B，第三題答案C，JSON格式應為 ["A", "B", "C"]**

#### 可用資源
1. 中文wiki百科的json檔： https://drive.google.com/open?id=0ByoB_9NkZ9rRa3VUY25TeXRtdnM
2. 繁體中文wiki的json檔，且content經過斷詞https://drive.google.com/file/d/0ByoB_9NkZ9rRZWFRa1FiWlZYTDA/view?usp=sharing  
3. ptt社群網站爬蟲：https://github.com/RogerTsai917/PTT-Crawler
4. ijson: https://github.com/isagalaev/ijson
   使用ijson搜尋工具，ijson主要是使用在json過大而不能夠全部loading進記憶體時，採用stream的方式讀取json檔。
	python3 ijsonSearch.py 查詢的json檔名 查詢的目標類型 查詢目標名稱
