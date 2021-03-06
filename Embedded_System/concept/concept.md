##Concepts List		[Back](./../Embedded_System.md)

- 處理器選型依賴因素:
	- 系統核心功能模塊需求
	- 系統外部需求
- ARM三大系列的特點:
	- Cortex-A: 高性能應用處理
		- High-Performance Applications Processing for **Mobile** and **Enterprise Markets**.
		- provide a range of solutions for devices undertaking **complex compute tasks**.
	- Cortex-R: 實時處理
		- offer high-performance computing solutions for embedded system.
		- meeting challenging real-time constraints.
	- Cortex-M: 可向上兼容處理
		- for MCU which is sensitive to the **cost** and **consumption of power**.
- 指令系統
	- 存儲方式:
		- 馮諾依曼結構: 又名為普林斯頓結構
			- 指令存儲器和數據存儲器**合併**在一起的存儲結構, 兩個的地址位數一樣.
			- CPU使用單條總線取指令或數據
		- 哈佛結構
			- 指令存儲器和數據存儲器**分開**存放的存儲結構.
			- CPU使用兩條單獨的總線並行訪問兩個存儲器.
- 超長指令字處理器(VLIW)
	- 結合編譯器找到可以並行執行的指令捆綁在一個VLIW包下并行执行, 而包與包間是順序執行的.
	- VLIW只對包內的指令進行相關性檢查
	- 適合於**信號處理**和**多媒體應用**
- 數據存儲順序
	- little-endian(小端): 低地址放低位
	- big-endian(大端): 低地址放高位
- Neon協處理器
	- **SIMD**(單指令多數據) 引擎, 可用於加速**多媒體**和**信號數據**的處理, 協助CPU的運算.
	- 協處理器設計的目的是為了減輕主處理器的計算負擔

- Peripherals(外設)
	- PLL(Phase Locked Loop, 鎖相環): 指電路中鎖定相位的環路
	- EDMA(Enhanced Direct Memory Access, 增強型直接內存訪問): 用於DSP中的快速數據交換, 獨立於CPU的後臺數據傳輸處理
- Bus(總線)
	- I^2C(Inter-Intergrated Circuit, 內部集成電路): 雙向兩線型串行總線
		- SDA: 串行數據線
		- SCL: 串行時鐘線
	- GPIO(General Purpose Input/Output, 通用目的輸入/輸出): 總線擴展器
	- EMIF(External Memory Interface, 外部存儲接口): 用於實現DSP與不同存儲器間的鏈接
	- UART(Universal Asynchronous Receiver/Transmitter, 通用異步接受/發送器): 用於串行通信與並行通信間數據傳輸
	- SPI(Serial Peripheral Interface, 串行外設接口): 是一種高速的, 全雙工的, 同步的通信總線
- 板子调试步骤：
	- 編譯: 生成目標文件(.o)
	- 鏈接: 生成可執行文件(.elf)
	- 調試: 通過JTAG接口來進行調試
		- JTAG兩大模塊:
			- 測試芯片的電氣特性: 芯片是否可用
			- Debug: 測試可執行文件是否可用
		- JTAG四個接口:
			- TMS: 用於測試模式選擇
			- TCK: 用於測試時鐘輸入
			- TDI: 用於測試數據輸入
			- TDO: 用於測試數據輸出

<a href="#" style="left:200px;"><img src="./../../pic/gotop.png"></a>
=====
<a href="http://aleen42.github.io/" target="_blank" ><img src="./../../pic/tail.gif"></a>
