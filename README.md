Wi-SUN-playground
=================
ESP32 晶片本身不原生支援 Wi-SUN（Wireless Smart Ubiquitous Network，一種基於 IEEE 802.15.4g 的 Sub-GHz IPv6 網狀網路標準）。若要讓 ESP32 搭配 Wi-SUN 使用，通常需要透過外部專用的 Wi-SUN 無線模組或晶片來橋接。 [1, 2, 3] 
## 常見的整合方式與架構

   1. 搭配外部 Sub-GHz / Wi-SUN 專用晶片
   * 常見晶片/模組來源：Silicon Labs EFR32 (例如 EFR32FG25)、德州儀器 (TI) CC1352P7，或是奎芯/其餘廠商的 Wi-SUN 模組（例如 Quectel KCM0A5S）。
      * 連接方式：ESP32 通常透過 UART 或 SPI 與這些 Sub-GHz 無線協同處理器（RCP）或模組通訊。
      * 角色分工：
      * ESP32：作為主控端（Host），負責高層應用邏輯、Wi-Fi/藍牙回傳（Gateway 橋接），或是螢幕顯示與資料處理（例如使用 M5AtomS3 搭配 Wi-SUN 模組做智慧電表監控）。
         * 外部 Wi-SUN 晶片：負責處理底層沉重的 Sub-GHz 實體層（PHY）、媒體存取控制層（MAC）以及 IPv6 Mesh 網狀協定堆疊。 [1, 2, 3, 4, 5, 6] 
      2. 開發與軟體限制
   * 完整的 Wi-SUN FAN (Field Area Network) 協定堆疊記憶體與運算需求較高，官方或主流廠商多針對 Silicon Labs（搭配 Simplicity Studio 5）或 Linux 平台（如 Raspberry Pi）提供完整 SDK。
      * ESP32 要與外部 Wi-SUN 裝置通訊時，通常需要自己撰寫 AT 指令解析或序列埠（UART/SPI）封包轉送協定，TI 與 Silicon Labs 官方論壇多數回饋皆表示無現成的 SPI 隨插即用 Host 範例，需自行開發驅動與協議橋接。 [1, 3, 4, 6] 
   
如果你正打算進行相關開發，可以告訴我：

* 你希望 ESP32 扮演什麼角色（例如：Wi-SUN 終端節點、還是 Wi-SUN 轉 Wi-Fi 網關 Gateway）？
* 目前手頭上有選定哪一款 Wi-SUN 模組或晶片嗎？

我可以幫你進一步評估硬體介面與架構的可行性。

[1] [https://e2e.ti.com](https://e2e.ti.com/support/wireless-connectivity/sub-1-ghz-group/sub-1-ghz/f/sub-1-ghz-forum/1603834/cc1352p7-spi-communication-between-cc1352p7-1-wi-sun-and-esp32-data-not-transmitting-properly-over-wi-sun)
[2] [https://www.cnx-software.com](https://www.cnx-software.com/2025/06/11/quectel-kcm0a5s-wi-sun-fan-module-targets-large-iot-deployments-for-smart-cities-and-smart-agriculture/)
[3] [https://docs.silabs.com](https://docs.silabs.com/wisun/latest/wisun-getting-started-development/)
[4] [https://community.silabs.com](https://community.silabs.com/s/question/0D5Vm00000HlYXjKAN/integration-of-efr32mg-module-with-esp32-for-wisun-to-wifi-gateway?language=en_US)
[5] [https://www.hackster.io](https://www.hackster.io/rin_ofumi/power-monitor-using-wi-sun-with-m5atoms3-04576a)
[6] [https://docs.silabs.com](https://docs.silabs.com/wisun/2.8.0/wisun-network-configuration/)
