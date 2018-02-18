+++
title = "ไพธอนมาตรฐาน"
date =  2018-02-17T23:29:54+07:00
weight = 1
+++

## การนำเข้าข้อมูลจากไฟล์ csv

การนำเข้าข้อมูลจากไฟล์ csv สามารถทำได้โดยใช้ library `csv` ในไพธอน ผลลัพธ์จากการอ่านมีได้หลายแบบ

### อ่านข้อมูลทีละบรรทัดเป็น `list`
ตัวอย่างด้านล่างแสดงการอ่านไฟล์ `scores.csv` ทีละบรรทัดออกมาเป็นรายการ (`list`) และพิมพ์ออกมา

{{< highlight python >}}
import csv

csvfile = open('scores.csv')
reader = csv.reader(csvfile)
for row in reader:
    print(row)

csvfile.close()
{{< /highlight >}}

ผลลัพธ์
```
['name', 'score']
['สมชาย', '50']
['สมหญิง', '45']
['สมศักดิ์', '80']
['ประวิทย์', '78']
['ประมาณ', '56']
```

### อ่านข้อมูลทีละบรรทัดเป็น `dict`

{{< highlight python >}}
import csv

csvfile = open('scores.csv')
reader = csv.DictReader(csvfile)
for row in reader:
    print(row)

csvfile.close()
{{< /highlight >}}

ผลลัพธ์
```
{'name': 'สมชาย', 'score': '50'}
{'name': 'สมหญิง', 'score': '45'}
{'name': 'สมศักดิ์', 'score': '80'}
{'name': 'ประวิทย์', 'score': '78'}
{'name': 'ประมาณ', 'score': '56'}
```

### อ่านข้อมูลทั้งหมดจากนั้นคืนรายการที่เป็น `dict`

ด้านล่างเป็นฟังก์ชัน `read_csv_data` ที่คืนค่าเป็น `list` ของ `dict` ที่สามารถนำไปใช้ต่อได้เลย และตัวอย่างการใช้งาน

{{< highlight python >}}
import csv

def read_csv_data(filename):
    results = []
    csvfile = open(filename)
    reader = csv.DictReader(csvfile)
    for row in reader:
        results.append(row)
    csvfile.close()

    return results

# ตัวอย่างการเรียกใช้ฟังก์ชัน
data = read_csv_data('scores.csv')
for d in data:
    print(d['name'], d['score'])
{{< /highlight >}}

ผลลัพธ์
```
สมชาย 50
สมหญิง 45
สมศักดิ์ 80
ประวิทย์ 78
ประมาณ 56
```
