---
응답: true
기도 시작 날짜: 2024-07-23
tags:
  - "#기도제목"
범주: 1. 나
---
###### 상위 파일: [[🧭신앙#기도제목|기도 제목]]


# 기도한 노트
```dataviewjs
const fileName = dv.current()["file"]["link"];

dv.execute(
`TABLE WITHOUT ID
	file.link AS "제목"
	, date AS "기도 날짜"
FROM
	${fileName}
AND "20. 📅Calendar/201. 🙏기도 노트"
SORT date DESC`
)
```

