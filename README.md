# Словник гетеронімів української мови

[English version](./README.en.md)

Словник містить слова, що пишуться однаково, але мають різну вимову
(гетероніми). Іноді це відбувається, коли слова мають різне значення:

* а́тлас - збірник карт
* атла́с - тканина

Але більшість гетеронімів це слова, які мають різний наголос в залежності
від форми слова (відмінку, множини, часу тощо). Наприклад:

* блохи́ - родовий відмінок в однині ("немає ані блохи́")
* бло́хи - множина називного відмінку ("повсюди були бло́хи")


## Формат

Кожна група гетеронімів подається на окремому рядку. Кожен рядок має
формат

```
headword [TAB]  heteronym1,heteronym2
```

`headword` це слово без наголосу, як воно зазвичай подається на письмі.
`heteronym1`, `heteronym2` це слова, які мають різну вимову (їх може бути
більше, ніж два). Наголос в цих словах позначається Unicode символом
[`COMBINING ACUTE ACCENT`](https://unicode-table.com/en/0301/), що ставиться
після наголошеної голосної.

Приклад коду на Python, який парсить цей формат:

```python

dictionary = {}
with open("heteronyms.tsv") as f:
    for line in f:
        line = line.rstrip("\n")
        headword, heteronyms = line.split("\t")
        dictionary[headword] = heteronyms.split(",")

print(dictionary["пташки"])
# Out: ['пташки́', 'пта́шки']
```


## Джерело

Словник сформував [Олексій Сивоконь](https://github.com/asivokon) на
основі ["Словників України"](https://lcorp.ulif.org.ua/dictua/) Українського
мовно-інформаційного фонду НАН України.
