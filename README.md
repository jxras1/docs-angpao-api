TrueMoney Voucher API

# Endpoint Base URL :
https://rikumi.qzz.io/api/truemoney/angpao


# ข้อมูลเพิ่มเติม
 API นี้รองรับทั้ง GET และ POST requests

 ต้องระบุ voucher hash และเบอร์โทรศัพท์ 10 หลัก

API นี้รองรับการร้องขอผ่านทั้ง HTTP GET และ POST methods พร้อมรูปแบบข้อมูลทั้ง JSON และ form-data


# Authentication
API นี้ไม่ต้องการการ authentication ในขณะนี้ คุณสามารถเริ่มใช้งานได้ทันทีโดยเรียกใช้ endpoint พร้อมพารามิเตอร์ที่จำเป็น

Endpoint
https://rikumi.qzz.io/api/truemoney/angpao
POST
หรือใช้ผ่าน GET request โดยส่งพารามิเตอร์ผ่าน query string


# Parameter:
voucher	String	Yes	Voucher hash (เฉพาะส่วนหลัง v= ใน URL) เช่น จากลิงก์เต็ม https://gift.truemoney.com/campaign/?v=019b54d1844e7c99a68f3d394b249e3845X ส่งเฉพาะ 019b54d1844e7c99a68f3d394b249e3845X หรือลิงค์แบบเต็มได้หมด 
phone	String	Yes	เบอร์มือถือ 10 หลัก (ต้องมี 0 นำหน้า) เช่น 0981234567

curl -X POST "https://rikumi.qzz.io/api/truemoney/angpao" \
  -H "Content-Type: application/json" \
  -d '{
    "voucher": "019b54d1844e7c99a68f3d394b249e3845X",
    "phone": "0981234567"
  }'

หรือใช้ GET request:

curl "https://rikumi.qzz.io/api/truemoney/angpao?voucher=019b54d1844e7c99a68f3d394b249e3845X&phone=0981234567"

Response
Success Response
{
  "status": {
    "message": "success",
    "code": "SUCCESS"
  },
  "data": {
    "voucher": {
      "voucher_id": "996332695962297663",
      "amount_baht": "10.00",
      "redeemed_amount_baht": "10.00",
      "member": 1,
      "status": "active",
      "link": "019b54d1844e7c99a68f3d394b249e3845X",
      "detail": "",
      "expire_date": 1757081437789,
      "type": "F",
      "redeemed": 1,
      "available": 0
    },
    "owner_profile": {
      "full_name": "จิรัสย์ ***"
    },
    "redeemer_profile": {
      "mobile_number": "0981234567"
    },
    "my_ticket": {
      "mobile": "**",
      "update_date": 1755871875554,
      "amount_baht": "10.00",
      "full_name": "เอพีไอ ***",
      "profile_pic": null
    },
    "tickets": [
      {
        "mobile": "**",
        "update_date": 1755871873355,
        "amount_baht": "10.00",
        "full_name": "เอพีไอ ***",
        "profile_pic": "https://profile-images-cdn.truemoney.com/**.jpg"
      }
    ]
  }
}

Error Response
{
  "status": "fail",
  "message": "Voucher hash is required"
}


# Error Codes: 
Voucher hash is required	ไม่ได้ส่งพารามิเตอร์ voucher	ตรวจสอบให้แน่ใจว่าได้ส่งพารามิเตอร์ voucher

Phone number is required	ไม่ได้ส่งพารามิเตอร์ phone	ตรวจสอบให้แน่ใจว่าได้ส่งพารามิเตอร์ phone

Invalid voucher hash	voucher hash ไม่ถูกต้อง	ตรวจสอบว่า voucher hash ถูกต้องและครบถ้วน

Invalid phone number	หมายเลขโทรศัพท์ไม่ถูกต้อง	ตรวจสอบว่าเป็นหมายเลขโทรศัพท์ 10 หลักและขึ้นต้นด้วย 0

{ "status": { "message": "Voucher ticket is out of stock.", "code": "VOUCHER_OUT_OF_STOCK" },	ซองนี้ถูกใช้ไปแล้ว	ใช้ซองอื่นที่ยังไม่ถูกใช้



# ตัวอย่างการใช้งาน:
# cURL :
curl -X POST "https://rikumi.qzz.io/api/truemoney/angpao" \
  -H "Content-Type: application/json" \
  -d '{
    "voucher": "019b54d1844e7c99a68f3d394b249e3845X",
    "phone": "0981234567"
  }'
  
# หรือใช้ GET request:    
curl "https://rikumi.qzz.io/api/truemoney/angpao?voucher=019b54d1844e7c99a68f3d394b249e3845X&phone=0981234567"
  

# python :
import requests

url = "https://rikumi.qzz.io/api/truemoney/angpao"
payload = {
    "voucher": "019b54d1844e7c99a68f3d394b249e3845X",
    "phone": "0981234567"
}

# Send as JSON
response = requests.post(url, json=payload)
print(response.status_code)
print(response.json())

# Or as form data
# response = requests.post(url, data=payload)


# JavaScript :
// Using fetch API
const url = 'https://rikumi.qzz.io/api/truemoney/angpao';
const data = {
  voucher: '019b54d1844e7c99a68f3d394b249e3845X',
  phone: '0981234567'
};

// As JSON
fetch(url, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));

// As form data
const formData = new FormData();
formData.append('voucher', data.voucher);
formData.append('phone', data.phone);

fetch(url, {
  method: 'POST',
  body: formData
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));