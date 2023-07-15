# awk-arabic
Arabic Texts task by AWK

هذه الصفحة لكتابة بعض الملاحظات والإرشادات عن استعمال لغة برمجة AWK في مهام اللغة العربية
## أفكار لاستعمالات أوك

* حذف الحركات
* تغيير الفاصل في ملف csv
* تقسيم النص إلى كلمات
* حساب تكرار الكلمات
* حذف الكلمات المستبعدة



### حذف الحركات
أوك لا يدعم اليونيكود لذا علينا تحويل الحركات إلى utf8

سكريبت حذف الحركات بواسطة أوك:
```awk
echo "أُحِبُّ وَطَنِي" | awk '{ gsub(/\xd9\x8b|\xd9\x8c|\xd9\x8d|\xd9\x8e|\xd9\x8f|\xd9\x90|\xd9\x91|\xd9\x92|\xd9\xb0/, ""); print }'
```
للحصول على سلسلة الحركات بشكل بايتات استعنّا بسكريبت بيثون
```python
repru = []
for c in u"\u064b\u064c\u064d\u064e\u064f\u0650\u0651\u0652\u0670":
	code_point = ord(c)  # Unicode code point
	utf8_bytes = chr(code_point).encode('utf-8')
	utf8_representation = ''.join([f'\\x{byte:02x}' for byte in utf8_bytes])
	repru.append(utf8_representation)
print('|'.join(repru))
```
الناتج يكون:
```
\xd9\x8b|\xd9\x8c|\xd9\x8d|\xd9\x8e|\xd9\x8f|\xd9\x90|\xd9\x91|\xd9\x92|\xd9\xb0
```

### convert multiline record  to csv

FS = field separator
RS = record separator
OFS = output field separator
```awk
BEGIN { FS="\n"; RS=""; OFS="\t"}

{print $1,$2,$9}
END {}
```

## مراجع
30 Examples for Awk Command in Text Processing
https://likegeeks.com/awk-command/
