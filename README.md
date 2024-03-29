# 2022_Robocon_circuit
**2022年ロボコンの回路**<br>
マスターブランチは保護されているので，各ブランチで必ずプルリクエストを送ってください．<br>

他にも[自作MD](https://github.com/Issaimaru/MoterDriver_v1)と[自作電源基板](https://github.com/Issaimaru/PowerSupply_v1)とか[モババ電源分岐させるやつ](https://github.com/Issaimaru/USB_JST-XH_CONVERTER)とかいろいろ使ったけど不具合多く見つかって成仏しそうになった<br>

回路図とピン配置をここに明記しておきます．<br>

- 上部機構
  - 回路図
    ![上部機構](https://user-images.githubusercontent.com/80198387/185569705-36741227-0238-4329-8269-7aa137394152.png)
    
    > **Warning**<br>
    > 回路図が一部変わっています．詳しくはIssaimaruまで...
  
  - ピン配置
  
    | ピン番号 | 機能 | 備考 |
    | :---: | :---: | :--: |
    | PB_8/D15 | I2C_SCL | MoterDriver-Controller v3との通信用(I2C)|
    | PB_9/D14 | I2C_SDA | 同様 |
    | PA_15 | UART_TX | 足回りのmbedとの通信用 |
    | PB_7 | UART_RX | 同様 |
    | PB_4/D5 | PWM1 | 上下機構のモータの制御用 |
    | PB_5/D4 | DIR1 | 同様 |
    | PB_10/D6 | PWM2 | 装填機構のモータの制御用 |
    | PB_3/D3 | DIR2 | 同様 |
    | PA_8/D7 | PWM3 | 射出機構のモータ制御用 |
    | PA_10/D2 | DIR3 | 同様 |
    | PA_1/A1 | LED1 | MDCとの通信確認用LED |
    | PA_4/A2 | LED2 | 足回りのmbedとの通信確認用LED |
    | PA_0/A0 | LED3 | 上下機構の速度確認用LED(PWMに対応) |
    | PB_0/A3 | LED4 | 上下機構の上昇確認用LED |
    | PC_1/A4 | LED5 | 上下機構の下降確認用LED |
    | PC_0/A6 | LED6 | 射出確認用LED |
    
- 足回り
  - 回路図
    ![足回り](https://user-images.githubusercontent.com/80198387/185569554-7d095d9b-2277-4369-bf48-2375935484d7.png)

    > **Warning**<br>
    > 回路図が一部変わっています．詳しくはIssaimaruまで...
    
  - ピン配置

    | ピン番号 | 機能 | 備考 |
    | :---: | :---: | :--: |
    | PB_8/D15 | I2C_SCL | MoterDriver-Controller v3との通信用(I2C)|
    | PB_9/D14 | I2C_SDA | 同様 |
    | PA_15 | TWE_TX | TWELITEとの通信用 |
    | PB_7 | TWE_RX | 同様 |
    | PA_12 | MCU_RX | 上部機構側mbedとの通信用 |
    | PA_11 | MCU_TX | 同様 |
    | PB_4/D5 | PWM1 | 三輪メカナムの正面側モータ制御用 |
    | PB_5/D4 | DIR1 | 同様 |
    | PB_10/D6 | PWM2 | 三輪メカナムの左側面側モータの制御用 |
    | PB_3/D3 | DIR2 | 同様 |
    | PA_8/D7 | PWM3 | 三輪メカナムの右側面側モータの制御用 |
    | PA_10/D2 | DIR3 | 同様 |
    | PA_0/A0 | LED1 | MDCとの通信確認用LED |
    | PA_1/A1 | LED2 | 上部機構側mbedとの通信確認用LED |
    | PA_4/A2 | LED3 | TWELITEとの通信確認用LED |
    
- 暴走対策機能付き非常停止スイッチ
  - 回路図
    ![暴走対策機能付き非常停止スイッチ](https://user-images.githubusercontent.com/80198387/187575599-e7619aea-3dc1-4c90-a574-2f65bee7aef9.png)

  - 接続方法<br>
    - INPUT1，INPUT2はPowerUnit BseriesのMILコネクタ部のうちのVCCとGNDに無理やりはんだ付けして配線を伸ばして2ピンのJST-XHで接続してください．
    - SW_INは非常停止スイッチと接続してください．
    - CTRLはPowerUnit BseriesのCTRLと接続してください．
    - SWITCHはPowerUnit BseriesのSWITCHと接続してください．
    
 - 上部機構用エンコーダー
  - 回路図
    ![上部機構用エンコーダー](https://user-images.githubusercontent.com/80198387/193417058-c3f58b3c-a31a-4396-a744-c2936ded76ef.png)

  - ピン配置
    | ピン番号 | 機能 | 備考 |
    | :---: | :---: | :--: |
    | PB_7/D4 | I2C_SDA | メインマイコンとの通信用 |
    | PB_6/D5 | I2C_SCL | 同様 |
    | PF_0/D7 | ENC1_A | ロリコン1のA相 |
    | PF_1/D8 | ENC1_B | ロリコン1のB相 |
    | PA_8/D9 | ENC1_X | ロリコン1のX相 |
    | PA_11/D10 | ENC2_A | ロリコン2のA相 |
    | PB_5/D11 | ENC2_B | ロリコン2のB相 |
    | PB_4/D12 | ENC2_X | ロリコン2のX相 |
    | PB_1/D6 | PHOTO_OUT | フォトインタラプタの入力(HI->物体有/LOW->物体無) |
    | PA_6/A5 | RED | テープLEDの赤色点灯用ピン |
    | PA_4/A3 | GREEN | テープLEDの緑色点灯用ピン |
    | PA_3/A2 | BLUE | テープLEDの青色点灯用ピン |
    
  - 足回り用ロリコン
    - 回路図<br>
      ![足回り用ロリコン](https://user-images.githubusercontent.com/80198387/194679919-a4d8bbbc-785c-45b8-91b9-a1de73a46089.png)<br>

    - ピン配置<br>
      | ピン番号 | 機能 | 備考 |
      | :---: | :---: | :--: |
      | PB_7/D4 | I2C_SDA | メインマイコンとの通信用 |
      | PB_6/D5 | I2C_SCL | 同様 |
      | PA_12/D2 | ENC1_A | ロリコン1のA相 |
      | PB_0/D3 | ENC1_B | ロリコン1のB相 |
      | PF_0/D7 | ENC2_A | ロリコン2のA相 |
      | PB_1/D6 | ENC2_B | ロリコン2のB相 |
      | PF_1/D8 | ENC3_A | ロリコン3のA相 |
      | PA_8/D9 | ENC3_B | ロリコン3のB相 |
      | PB_5/D11 | ENC4_A | ロリコン4のA相 |
      | PA_11/D10 | ENC4_B | ロリコン4のB相 |
      
  - 国技館射出
    - 回路図<br>
      ![国技館射出](https://user-images.githubusercontent.com/80198387/199213701-0def5a7b-3f51-46c5-b0ae-15a8d4d2cb61.png)<br>
      
    - ピン配置<br>
      | ピン番号 | 機能 | 備考 |
      | :---: | :---: | :--: |
      | PC_12 | UART1_TX | 足回りとの通信用 |
      | PD_2 | UART1_RX | 同様 |
      | 🌠PF_7 | UART2_TX | マトリクスLEDとの通信用 |
      | 🌠PF_6 | UART2_RX | 同様 |
      | 🌠PA_10 | PWM1 | モータ駆動用PWM出力ピン |
      | 🌠PB_3 | PWM2 | 同様 |
      | 🌠PB_5 | PWM3 | 同様 |
      | 🌠PB_4 | PWM4 | 同様 |
      | 🌠PA_3 | PWM5 | 同様 |
      | 🌠PA_2 | PWM6 | 同様 |
      | 🌠PC_7 | DIR1 | モータ回転方向信号出力ピン |
      | 🌠PA_9 | DIR2 | 同様 |
      | 🌠PA_8 | DIR3 | 同様 |
      | 🌠PB_10 | DIR4 | 同様 |
      | 🌠PA_7 | DIR5 | 同様 |
      | 🌠PB_6 | DIR6 | 同様 |
      | PD_5 | ENC1_B | ロリコン1のB相 |
      | PD_6 | ENC1_A | ロリコン1のA相 |
      | PD_7 | ENC2_B | ロリコン2のB相 |
      | PE_3 | ENC2_A | ロリコン2のA相 |
      | PF_1 | ENC3_B | ロリコン3のB相 |
      | PF_0 | ENC3_A | ロリコン3のA相 |
      | PD_1 | ENC4_B | ロリコン4のB相 |
      | PD_0 | ENC4_A | ロリコン4のA相 |
      | PG_0 | ENC5_B | ロリコン5のB相 |
      | PE_1 | ENC5_A | ロリコン5のA相 |
      | PG_9 | ENC6_B | ロリコン6のB相 |
      | PG_12 | ENC6_A | ロリコン6のA相 |
      | PD_14 | RED | テープLED 赤色 |
      | PD_15 | GREEN | テープLED 緑色 |
      | PE_9 | BLUE | テープLED 青色 |
      | PF_11 | LED1 | 確認用LED(任意) |
      | PE_0 | LED2 | 同様 |
      | PG_8 | LED3 | 同様 |
      | PG_5 | LED4 | 同様 |
      | PG_6 | LED5 | 同様 |

  - 国技館足回り
    - 回路図<br>
      ![国技館足回り](https://user-images.githubusercontent.com/80198387/199422710-bb65ea0e-a7b4-44d6-8f0d-4337bfc3b219.png)<br>
      
    - ピン配置<br>
      | ピン番号 | 機能 | 備考 |
      | :---: | :---: | :--: |
      | PA_15 | UART1_TX | IM920sLとの通信用 |
      | PB_7 | UART1_RX | 同様 |
      | PA_11 | UART2_TX | 射出マイコンとの通信用 |
      | PA_12 | UART2_RX | 同様 |
      | D6/PB_10 | PWM1 | モータ駆動用PWM出力ピン |
      | D7/PA_8 | PWM2 | 同様 |
      | D8/PA_9 | PWM3 | 同様 |
      | D9/PC_7 | PWM4 | 同様 |
      | Pc_4 | DIR1 | モータ回転方向信号出力ピン |
      | PB_12 | DIR2 | 同様 |
      | PC_5 | DIR3 | 同様 |
      | PC_6 | DIR4 | 同様 |
      | PA_13 | ENC1_B | ロリコン1のB相 |
      | PA_14 | ENC1_A | ロリコン1のA相 |
      | PC_14 | ENC2_B | ロリコン2のB相 |
      | PC_15 | ENC2_A | ロリコン2のA相 |
      | PH_0 | ENC3_B | ロリコン3のB相 |
      | PH_1 | ENC3_A | ロリコン3のA相 |
      | PC_2 | ENC4_B | ロリコン4のB相 |
      | PC_3 | ENC4_A | ロリコン4のA相 |
      | A1/PA_1 | SLEEP | IM920sLのSLEEPピン |
      | A2/PA_4 | RESET | IM920sLのRESETピン |
      | A3/PB_0 | STATUS | IM920sLのSTATUSピン |
      | A4/PC_1 | XMIT | IM920sLのXMITピン |
      | A6/PC_0 | BUSY | IM920sLのBUSYピン |
      | PB_2 | LED1 | 確認用LED |
      | PB_1 | LED2 | 同様 |
      | PB_15 | LED3 | 同様 |
      | PB_14 | LED4 | 同様 |
      | PB_13 | LED5 | 同様 |
      
  - 国技館コントローラ
    - 回路図<br>
      ![国技館コントローラ](https://user-images.githubusercontent.com/80198387/200781753-c2ce0916-b5e8-4044-99a5-a1f258bbd0fb.png)
      
    - ピン配置<br>
      | ピン番号 | 機能 | 備考 |
      | :---: | :---: | :--: |
      | PC_10 | CK1_UP | 左十字キー↑ |
      | PC_12 | CK1_LEFT | 左十字キー← |
      | PD_2 | CK1_RIGHT | 左十字キー→ |
      | PC_11 | CK1_DOWN | 左十字キー↓ |
      | D3/PB_3 | CK2_UP | 右十字キー↑ |
      | D5/PB_4 | CK2_LEFT | 右十字キー← |
      | D4/PB_5 | CK2_RIGHT | 右十字キー→ |
      | D2/PA_10 | CK2_DOWN | 右十字キー↓ |
      | PB_14 | BL1 | 左トリガーL1 |
      | PB_13 | BL2 | 左トリガーL2 |
      | PB_1 | BR1 | 右トリガーR1 |
      | PB_15 | BR2 | 右トリガーR2 |
      | A0/PA_0 | L/R1 | 左アナログスティックx軸 |
      | A1/PA_1 | U/D1 | 左アナログスティックy軸 |
      | A2/PA_4 | L/R2 | 右アナログスティックx軸 |
      | A3/PB_0 | U/D2 | 右アナログスティックy軸 |
      | PA_13 | EME_SW | 非常停止スイッチ入力(HIGH:開 LOW:閉) |
      | PA_15 | TX | IM920sL通信用 |
      | PB_7 | RX | 同様 |
      | PH_1 | XMIT | IM920sLのドキュメント参照 |
      | PC_2 | SLEEP | 同様 |
      | PC_3 | STATUS | 同様 |
      | A6/PC_0 | BUSY | 同様 |
      | A4/PC_1 | RESET | 同様 |
      | D14/PB_9 | LED1 | 確認用LED |
      | D15/PB_8 | LED2 | 同様 |
      | PC_9 | LED3 | 同様 | 
      | PC_8 | LED4 | 同様 |
      | PC_6 | LED5 | 同様 |
      
    

      
  
