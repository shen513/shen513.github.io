#include "SPI.h"
#include "MFRC522.h"

#define SS_PIN 10 //晶片選擇腳位
#define RST_PIN 9 //設定重置腳位


MFRC522 rfid(SS_PIN, RST_PIN); //建立MFRC522物件

void setup() {
  Serial.begin(9600);
  SPI.begin();
  rfid.PCD_Init();
}
byte cardID[] = {0xA0, 0x79, 0x7A, 0xA2};//固定rfid卡號 
void loop() {
  //
  if (!rfid.PICC_IsNewCardPresent() || !rfid.PICC_ReadCardSerial())
    return;
    
  byte *id = rfid.uid.uidByte;   // 取得卡片的UID
  byte idSize = rfid.uid.size;   // 取得UID的長度

  //設定驗證指標為 true
  bool validate = true;
  //判斷卡片的id是否與cardID一致
  for (int i = 0; i < idSize; i++)
  {
    // 如果其中一個id不符合cardID中對應的id
    if (cardID[i] != id[i])
    {
      //設定驗證指標為 false
      validate = false;
      //跳出迴圈
      break;
    }
  }

  //如果卡片通過驗證
  if (validate)
  {
    Serial.println("open");
  }
  //卡片沒通過驗證
  else
  {
    Serial.println("lock") ;
  }

  rfid.PICC_HaltA();
  rfid.PCD_StopCrypto1();
}
