# SpaceShip Game

#### TH Lang

> สำหรับรูปภาพต่างๆที่ใช้ในการสร้างสามารถโหลดได้ใน assest เลยนะครับ ผมเตรียมไว้ให้แล้ว :D

วิธีการสร้าง
1. สร้าง **Canvas** ชื่อว่า **Canvas1** เป็นพื้นที่สำหรับเล่นเกม
2. กำหนด **Properties** ของ **Canvas1** ได้แก่ **Width** เป็น **Fill parent** และ **Height** เป็น **300 pixel** กำหนด **BackgroundColor เป็น None**
3. สร้าง **ImageSprite** ตั้งชื่อว่า **Rocket** เป็นฐานยิงจรวด
4. อัพโหลดภาพฐานยิงจรวดกำหนดค่า **Picture** ใน **Properties** ของ **Rocket** เป็นรูปฐานยิงจรวดที่เราอัพโหลด และ ลากไปไว้ด้านล่างข้างใน **Canvas1** เพื่อที่จะได้เป็นฐานยิงจรวด
5. สร้าง **ImageSprite** ตั้งชื่อว่า **Flying** เป็นยานบินที่เราต้องการจะยิง
6. อัพโหลดภาพยานบินกำหนดค่า **Picture** ใน **Properties** ของ **Flying** เป็นรูปยานบินที่เราอัพโหลด และ ลากไปไว้ด้านบนข้างใน **Canvas1** เพื่อที่จะได้เป็นยานบินที่เราต้องการจะยิง
7. สร้าง **BallSprite** ตั้งชื่อว่า **Bullet** เปลี่ยน **PaintColor** เป็น**สีเขียว** ตั้งค่า **Radius** เป็น **5** เป็นกระสุนจรวดไว้สำหรับยิง
8. สร้าง **Clock** ตั้งชื่อว่า **RandPosFlying** กำหนด **TimeInterval** เป็น **3000** ไว้สำหรับกำหนดเวลาการสุ่มตำแหน่งของยานบิน
9. สร้าง **HorizontalArrangement** ไว้ข้างล่างถัดจาก **Canvas1** กำหนด **Width** เป็น **Fill Parent** และ **BackgroundColor** เป็น **None**
10. สร้าง **Label** ชื่อว่า **Label1** เปลี่ยน **Text** เป็น **Score : **
11. สร้าง **Label** ตั้งชื่อว่า **LabelScore** เปลี่ยน **Text** เป็น **0**
12. สร้าง **Button** ตั้งชื่อว่า **Reset** เปลี่ยน **Text** เป็น **Reset**
13. นำ **Label1** **LabelScore** และ **Reset** ไปไว้ใน **HorizontalArrangement** ที่สร้างไว้
14. เริ่มการกำหนดการทำงานของโปรแกรมโดยไปที่หน้า **Blocks**
15. สร้างบล็อก **Rocket.Dragged** สำหรับทำให้ฐานยิงเคลื่อนที่ได้ โดยใช้คำสั่ง **set Rocket.X to** และนำ **get currentX** มาต่อเข้าด้วยกัน
![Rocket.Dragged](https://www.img.in.th/images/d815e0aaee3d2d7aa02e5be7915768bb.png "Rocket.Dragged")
16. การกำหนดการยิงกระสุนจากฐานยิง **เมื่อยานบินโดนยิงจะทำให้ยานบินหายไปและเพิ่มคะแนน 1 คะแนน** ให้เริ่มจากคำสั่ง **Screen1.initialize** เมื่อ**เปิดโปรแกรม**จะให้**กระสุนมีค่า**เป็น **invisible** หรือมองไม่เห็นก่อน
![Screen1.initialize](https://www.img.in.th/images/f52aec309505636f2059279dee4ad908.png "Screen1.initialize")
17. **กำหนดให้กระสุนย้ายมายังตำแหน่งของฐานยิงและเริ่มทำการยิง** เมื่อแตะตัวยาน แต่ถ้าสั่ง **Bullet.Moveto** อย่างเดียว จะทำให้กระสุนยิงไปไม่ถึงขอบจอได้ถ้าหากแตะที่ฐานยิงรัวๆ จึงต้องใช้ **if** มาใช้ในการตรวจสอบว่า**กระสุน**ยังมี**สถานะการมอง**เห็นเป็น **true** อยู่หรือไม่ ถ้าไม่มีจึงจะ **Moveto** มาที่ฐานและทำการยิงได้
![Rocket.Touched](https://www.img.in.th/images/5aea92237575b45d476b4db4bfc24917.png "Rocket.Touched")
> อธิบายโค้ดนิดนึง คือตัว Bullet.Speed เนียคือการกำหนดความเร็วของกระสุน ส่วน Bullet.Heading คือ ทิศทางของกระสุน โดย 90 คือ 90 องศา

18. เมื่อยานบินโดนยิง ให้กระสุนมีสถานะเป็น **invisible** โดยใช้ **when Flying.CollidedWith** เพื่อตรวจสอบว่ายานบินได้โดยวัตถุอื่นชน หรือก็คือ โดนยิงนั้นเอง และ เพิ่มคะแนน **1** คะแนน โดยนำ **LabelScore** มา **+1** และ **set LabelScore.Text to** เพื่ออัพเดทคะแนน และทำการ **Moveto** มาที่ฐานและทำการยิงอีกครั้ง
![Flying.CollidedWith](https://www.img.in.th/images/14af768e60eab6c2acedf0af8a2f8793.png "Flying.CollidedWith")
19. กำหนดการทำงานให้ปุ่ม **Reset** เมื่อกดปุ่ม คะแนนจะกลับไปเป็น **0** โดยการ **when Reset.Click** ให้ **set LabelScore.Text to** เป็น **0**
![Reset.Click](https://www.img.in.th/images/3543de99ce53041fe8bd918dc5c91d35.png "Reset.Click")
20. สามารถกำหนดเวลาการเคลื่อนไหวของยานบินให้เคลื่อนที่ตลอดเวลาได้โดยการใช้ **Clock** ที่ชื่อว่า **RandPosFlying** ที่สร้างไว้ โดยนำบล็อก **when RandPosFlying.Timer** ให้ **set Flying.X to** เป็น **random integer from 0 to Canvas1.Width - Flying.Width**
![RandPosFlying](https://www.img.in.th/images/e708a172f53ee8fa49cb35d0a99e8354.png "RandPosFlying")
21. เมื่อกระสุนโดนขอบจอให้ **set Bullet.Visible to**   **false** และทำการ **Moveto** มาที่ฐานและทำการยิงอีกครั้ง
![Bullet.Visible](https://www.img.in.th/images/eacc8bd77514b36d2bad6616230f150a.png "Bullet.Visible")
22. ไปที่หน้า **Designer** ที่ **Properties** ของ **Screen1** และอัพโหลดรูปภาพฉากพื้นหลังทำการกำหนด **BackgroundImage** เป็นรูปภาพฉากพื้นหลัง
> เพิ่มเติมสำหรับคนที่ต้องการกระสุนสมจริงขึ้นด้วยการนำกระสุนมาติดกับบอล

23. สร้าง ImageSprite ตั้งชื่อว่า ImgBullet อัพโหลดรูปกระสุนและกำหนด Picture เป็นรูปกระสุน 
24. สร้าง Clock ตั้งชื่อว่า TicBullet กำหนด TimeInterval เป็น 20
24. ไปที่หน้า Blocks สร้างบล็อกชื่อ TicBullet.Timer และให้ภาพกระสุน(ImgBullet) MoveTo ตาม Bullet ไป
![TicBullet](https://www.img.in.th/images/350d0688b5ee558f50dd6c3192aadc7d.png "TicBullet")

### หากจุดใดผมพิมพ์ผิดหรือวิธีการผิดตรงไหนสามารถเปิด issues หรือ แจ้งผมได้เลยนะครับ ขอบคุณครับ

#### Create By ForestCrazy
