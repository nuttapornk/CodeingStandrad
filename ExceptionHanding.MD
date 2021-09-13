# Exception Handing

1.	การทำ Try-Catch เมื่อเกิด Exception(ข้อยกเว้น) และไม่ทำอะไรเลย เป็นสิ่งที่ไม่สมควรทำโดยอย่างยิ่ง หากซ่อนException เราจะไม่มีทางทราบเลยว่า Exception นั้นคืออะไร ไม่ทราบถึงปัญหา ควรหลีกเลี่ยง Exception ทั้งหมด โดยการเพิ่มเงื่อไขการตรวจสอบในกระบวรการพัฒนาโปรแกรม ไม่ว่าในกรณีใด ไม่อนุญาตให้มี Exception และไม่ทําอะไรเลย ในกรณีที่เลวร้ายที่สุดควรบันทึก Exception และดําเนินการต่อไป
2.	ในกรณีที่เกิดException ให้แสดงข้อความที่เหมาะสมเป็นมิตรแก่ผู้ใช้งาน แต่ให้บันทึก Exception จริง พร้อมรายละเอียดทั้งหมด วันเวลาที่เกิด ฟังก์ชันหรือชื่อ Class เป็นต้น
3.	Try-catch เฉพาะ Exception ที่เฉพาะเจาะจงเท่านั้น ยกเว้น Exception ทั้วไป

```c#
//Good: 
void ReadFromFile(string fileName)
{
  try
  {
    // read from file.
  }
  catch (FileIOException ex)
  {
    // log error.
    // re-throw exception depending on your case.
    throw;
  }
}
//Not Good: 
void ReadFromFile(string fileName)
{
  try
  {
    // read from file.
  }
  catch (Exception ex)	
  {
    // Catching general exception is bad... we will never know whether 
    // it was a file error or some other error.		
    // Here you are hiding an exception. 
    // In this case no one will ever know that an exception happened.	
    return "";		
  }
}
```
4.	ไม่จำเป็นต้อง Try-Catch ทั้งหมดในฟังก์ชัน เปิดทิ้งไว้แล้วปล่อยให้แอปพลิเคชันล่ม จะช่วยให้เราพบข้อผิดพลาดในขั้นตอนการพัฒนาระบบ 
5.	เมื่อจะโยน Exception ต่อ ให้ใช้คำสั่ง “throw” โดยไม่ต้องระบุ Exception เดิม วิธีการนี้จะทำให้ลำดับการทำงานเดิมอยู่ครบทั้งหมด (call stack preserved)

```c#
//Good:
catch
{
  // do whatever you want to handle the exception 
  throw;	
}

//Not Good:
catch (Exception ex)
{
  // do whatever you want to handle the exception 
  throw ex;
}
```
