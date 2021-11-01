# studyGPIO
## GPIOの概要
GPIOはGeneral Purpose Input/Outputの略で、汎用I/Oポートとも呼ばれる。以下の特徴がある。
- ユーザー側から制御可能
- 入出力に使える
- 有効/無効の切り替え可能
- 入力割り込み機能
## Ultra96-V2のハードウェア仕様
### Ultra96-V2の入出力配置
Ultra96-V2の入出力は以下のように配置されている。ユーザー用ブッシュボタンにUser Push Button(SW1)が用意されている。また、様々なLEDが用意されている。   
![Ultra96-V2 I/O image](ultra96v2.png)

### Ultra96-V2のハードウェアユーザガイド
[HW User Guide](Ultra96-V2-HW-User-Guide-v1_3.pdf)より以下がわかる。
#### プッシュボタンスイッチ
ユーザーが利用可能なプッシュボタンは以下の通り。
- PS MIO Bank 500(1.8V, MIOs 0 to 25)
	- MIO23 Push Button(SW1)
		- MPSoC Pin Number: AB5
		- MPSoC Site Name: PS_MIO23_500
		- Ultra96-V2 Net name: MIO23_GPIO_PB
#### LED
ユーザーが利用可能なLEDは以下の通り。
- Four user-controllable LEDs connected to PS_MIO[17..20]
	- PS LEDs
		- MPSoC Pin Number: AB4
		- Bank: 500
		- MPSoC Site Name: PS_MIO20_500
		- Ultra96-V2 Net name: MIO20_PS_LED0
		- MPSoC VCCO: +VCC_PSAUX = 1.8V
		- Color: Green
	- PS LEDs
		- MPSoC Pin Number: AA4
		- Bank: 500
		- MPSoC Site Name: PS_MIO19_500
		- Ultra96-V2 Net name: MIO19_PS_LED1
		- MPSoC VCCO: +VCC_PSAUX = 1.8V
		- Color: Green
	- PS LEDs
		- MPSoC Pin Number: Y5
		- Bank: 500
		- MPSoC Site Name: PS_MIO18_500
		- Ultra96-V2 Net name: MIO18_PS_LED2
		- MPSoC VCCO: +VCC_PSAUX = 1.8V
		- Color: Green
	- PS LEDs
		- MPSoC Pin Number: AA3
		- Bank: 500
		- MPSoC Site Name: PS_MIO17_500
		- Ultra96-V2 Net name: MIO17_PS_LED3
		- MPSoC VCCO: +VCC_PSAUX = 1.8V
		- Color: Green
- User-controllable Radio status connected to PL Pin B9/A9
	- Radio LEDs
		- MPSoC Pin Number: A9
		- Bank: 26
		- MPSoC Site Name: IO_L9N_AD3N_26
		- Ultra96-V2 Net name: RADIO_LED0
		- MPSoC VCCO: +VCC_AUX = 1.8V
		- Color: Yellow
	- Radio LEDs
	- Radio LEDs
		- MPSoC Pin Number: B9
		- Bank: 26
		- MPSoC Site Name: IO_L9P_AD3P_26
		- Ultra96-V2 Net name: RADIO_LED1
		- MPSoC VCCO: +VCC_AUX = 1.8V
		- Color: Blue
		
#### Bluetooth   
The ATWILC300-MR110CA Bluetooth interface connects through a UART interface. Since the Bluetooth UART interface requires hardware flow-control (RTS/CTS), which is only available through the PL, the UART RX/TX signals are connected to PS UART0 (MIO2, MIO3) and the RTS/CTS signals are connected to the PL High-Density (HD) bank. A blue LED is connected to Bank 26 programmable logic and can be used to indicate that Bluetooth is enabled when configured properly.
- Bluetooth
	- MPSoC Pin Number: B5
	- Bank: 26
	- MPSoC Site Name: IO_L11N_AD1N_26
	- Ultra96-V2 Net Name: BT_HCI_CTS
	- MPSoC VCCO: +VCC_AUX = 1.8V
- Bluetooth
	- MPSoC Pin Number: B7
	- Bank: 26
	- MPSoC Site Name: IO_L12P_AD0P_26
	- Ultra96-V2 Net Name: BT_HCI_RTS
	- MPSoC VCCO: +VCC_AUX = 1.8V
#### 40 Pin Low Speed Expansion Connector (J5)
Ultra96-V2 provides a 96Boards compatible Low Speed Expansion Connector. A Molex
87381-4063 (or compatible) 40 pin low profile female 2mm receptacle (20x2) 4.5mm height
is specified.
Table 24 shows the pinout of the Low Speed Expansion Header (Ultra96-V2 column) and
the differences from the 96Boards specification (96Boards column). Except for I2C0 and
I2C1, all dedicated interfaces specified by 96Boards can be replaced with GPIO or any
other IP supported by Zynq UltraScale+.
- HD PL IO Bank 26 (1.8V)
	- HD_GPIO0
		- MPSoC Pin Number: D7
		- MPSoC Site Name: IO_L5P_HDGC_AD7P_26
		- Pin: 3
	- HD_GPIO1
		- MPSoC Pin Number: F8
		- MPSoC Site Name: IO_L4P_AD8P_26
		- Pin: 5
	- HD_GPIO2
		- MPSoC Pin Number: F7
		- MPSoC Site Name: IO_L4N_AD8N_26
		- Pin: 7
	- HD_GPIO3
		- MPSoC Pin Number: G7
		- MPSoC Site Name: IO_L2P_AD10P_26
		- Pin: 9
	- HD_GPIO4
		- MPSoC Pin Number: F6
		- MPSoC Site Name: IO_L2N_AD10N_26
		- Pin: 11
	- HD_GPIO5
		- MPSoC Pin Number: G5
		- MPSoC Site Name: IO_L1N_AD11N_26
		- Pin: 13
	- HD_GPIO6
		- MPSoC Pin Number: A6
		- MPSoC Site Name: IO_L12N_AD0N_26
		- Pin: 29
	- HD_GPIO7
		- MPSoC Pin Number: A7
		- MPSoC Site Name: IO_L10N_AD2N_26
		- Pin: 31
	- HD_GPIO8
		- MPSoC Pin Number: G6
		- MPSoC Site Name: IO_L1P_AD11P_26
		- Pin: 33
	- HD_GPIO9
		- MPSoC Pin Number: E6
		- MPSoC Site Name: IO_L3P_AD9P_26
		- Pin: 16
	- HD_GPIO10
		- MPSoC Pin Number: E5
		- MPSoC Site Name: IO_L3N_AD9N_26
		- Pin: 18
	- HD_GPIO11
		- MPSoC Pin Number: D6
		- MPSoC Site Name: IO_L5N_HDGC_AD7N_26
		- Pin: 20
	- HD_GPIO12
		- MPSoC Pin Number: D5
		- MPSoC Site Name: IO_L7P_HDGC_AD5P_26
		- Pin: 22
	- HD_GPIO13
		- MPSoC Pin Number: C7
		- MPSoC Site Name: IO_L8N_HDGC_AD4N_26
		- Pin: 30
	- HD_GPIO14
		- MPSoC Pin Number: B6
		- MPSoC Site Name: IO_L11P_AD1P_26
		- Pin: 32
	- HD_GPIO15
		- MPSoC Pin Number: C5
		- MPSoC Site Name: IO_L7N_HDGC_AD5N_26
		- Pin: 34
		
## GPIOの使用方法
### PS側GPIOの使用方法
Vivadoでの接続作業は特に必要ない。制御方法は以下を参照。
- https://qiita.com/Ryuz/items/2a2603c2ce01fc054cf0
- https://www.trenz.jp/tutorial/zb-gpio.html


### PL側GPIOの使用方法
VivadoでAXI GPIOを経由してExternal Pinと接続する。制御方法はAXI GPIOの使い方を記載した以下のページを参照。
- https://japan.xilinx.com/content/dam/xilinx/support/documentation/ip_documentation/axi_gpio/v2_0/pg144-axi-gpio.pdf
- https://github.com/Xilinx/embeddedsw/tree/master/XilinxProcessorIPLib/drivers/gpio/examples
- https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18841846/AXI+GPIO
- https://qiita.com/s_nkg/items/800e0559332495605056
- https://taltalp.hatenablog.jp/entry/2017/11/06/204748
- https://dora.bk.tsukuba.ac.jp/~takeuchi/?%E9%9B%BB%E6%B0%97%E5%9B%9E%E8%B7%AF%2Fzynq%2FPetalinux2018.3%E3%81%A7axi_gpio

	
## Ultra96-V2の参考資料
- [Ultra96-V2 image](ultra96v2.png)
- [HW User Guide](Ultra96-V2-HW-User-Guide-v1_3.pdf)
- [Scemantic](Ultra96-V2_Rev1_Schematic.pdf)
- [constraints of AVNET reference file](Ultra96_V2_constraints_190430.xdc)
