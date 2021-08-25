#include <Wire.h> 

/* Địa chỉ của DS1307 */
const byte DS1307 = 0x68;
/* Số byte dữ liệu sẽ đọc từ DS1307 */
const byte NumberOfFields = 7;
 
/* khai báo các biến thời gian */
int second, minute, hour, day, wday, month, year;
   byte sc = second;
   byte mn = minute;
   byte hr = hour;
void setup()
{
  pinMode(9, OUTPUT);//relay điều khiển chuông
 

  Wire.begin();
  /* cài đặt thời gian cho module */
    //setTime(11, 53, 00, 7, 15, 6,19); // 12:30:45 CN 08-02-2015
  Serial.begin(9600);
}
 
void loop()
{
 
  readDS1307(); /* Đọc dữ liệu của DS1307 */
   
  /* Hiển thị thời gian ra Serial monitor */
  digitalClockDisplay();
  delay(1000);
  
  if((second>0&&minute==45&&hour==6)){ //Chuông vào tiết 1
   digitalWrite(9,HIGH);  
  }
  if(second>0&&minute==30&&hour==7){ //Chuông vào tiết 2
    digitalWrite(9,HIGH);
  }
 if((second>0&&minute==15&&hour==8)){ //Chuông vào tiết 3
   digitalWrite(9,HIGH);  
  }
  if(second>0&&minute==0&&hour==9){ //Chuông vào tiết 4
    digitalWrite(9,HIGH);
  }if((second>0&&minute==45&&hour==9)){ //Chuông vào tiết 5
   digitalWrite(9,HIGH);  
  }
  if(second>0&&minute==15&&hour==10){ ////Chuông vào tiết 6
    digitalWrite(9,HIGH);
  }if((second>0&&minute==0&&hour==11)){ //Chuông vào tiết 7
   digitalWrite(9,HIGH);  
  }
  if(second>0&&minute==45&&hour==11){//Chuông vào tiết 8
    digitalWrite(9,HIGH);
  }
 
}
void readDS1307()
{
        Wire.beginTransmission(DS1307);
        Wire.write((byte)0x00);
        Wire.endTransmission();
        Wire.requestFrom(DS1307, NumberOfFields);
        
        second = bcd2dec(Wire.read() & 0x7f);
      
        minute = bcd2dec(Wire.read() );
      
        hour   = bcd2dec(Wire.read() & 0x3f); // chế độ 24h.
      
        wday   = bcd2dec(Wire.read() );
        day    = bcd2dec(Wire.read() );
        month  = bcd2dec(Wire.read() );
        year   = bcd2dec(Wire.read() );
        year += 2000;    
}
/* Chuyển từ format BCD (Binary-Coded Decimal) sang Decimal */
int bcd2dec(byte num)
{
        return ((num/16 * 10) + (num % 16));
}
/* Chuyển từ Decimal sang BCD */
int dec2bcd(byte num)
{
        return ((num/10 * 16) + (num % 10));
}
 
void digitalClockDisplay(){
    // digital clock display of the time
    Serial.print(hour);
    printDigits(minute);
    printDigits(second);
    Serial.print(" ");
    Serial.print(day);
    Serial.print(" ");
    Serial.print(month);
    Serial.print(" ");
    Serial.print(year); 
    Serial.println(); 
}
 
void printDigits(int digits){
    // các thành phần thời gian được ngăn cách bằng dấu :
    Serial.print(":");
        
    if(digits < 10)
        Serial.print('0');
    Serial.print(digits);
}
 
/* cài đặt thời gian cho DS1307 */
void setTime(byte hr, byte min, byte sec, byte wd, byte d, byte mth, byte yr)
{
        Wire.beginTransmission(DS1307);
        Wire.write(byte(0x00)); // đặt lại pointer
        Wire.write(dec2bcd(sec));
        Wire.write(dec2bcd(min));
        Wire.write(dec2bcd(hr));
        Wire.write(dec2bcd(wd)); // day of week: Sunday = 1, Saturday = 7
        Wire.write(dec2bcd(d)); 
        Wire.write(dec2bcd(mth));
        Wire.write(dec2bcd(yr));
        Wire.endTransmission();
}
