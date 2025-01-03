---
운동 시작 날짜: 2024-07-18
운동_부위: 복근
---
###### 상위 파일: [[🧭건강#운동 종류]]


# 운동한 날
```dataviewjs
const fileName = dv.current()["file"]["link"];

dv.execute(
`TABLE WITHOUT ID
	file.link AS "제목"
	, date AS "운동 날짜"
FROM
	${fileName}
AND "20. 📅Calendar/203. 💪운동 노트"
SORT date DESC`
)
```

