---
title: プラグ アンド プレイ ドライバーをデバッグするための拡張機能
description: プラグ アンド プレイ ドライバーをデバッグするための拡張機能
ms.assetid: 0b60c4ce-5c2d-4cce-a1e6-8275186aa147
keywords:
- プラグ アンド プレイ (PnP) 拡張機能
- 拡張機能、プラグ アンド プレイ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48a1d0aa5d3a93d3517875cf9f7d446b78a84741
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347716"
---
# <a name="extensions-for-debugging-plug-and-play-drivers"></a>プラグ アンド プレイ ドライバーをデバッグするための拡張機能


プラグ アンド プレイ ドライバーをデバッグするときに役立つ次のデバッガー拡張機能。

[**! 監視**](-arbiter.md)  
現在のシステム リソース仲裁を表示します。 監視は、リソースについては、要求を調停およびそのバスに接続されているデバイスの間でリソースの競合を解決しようとしています。 バス ドライバーによって公開されるコードです。

[**!cmreslist**](-cmreslist.md)  
表示、CM\_リソース\_指定したデバイス オブジェクトのリスト。

CM のリソース リストのアドレスが必要です。

以下に例を示します。

```dbgcmd
kd> !cmreslist 0xe12576e8

CmResourceList at 0xe12576e8  Version 0.0  Interface 0x1  Bus #0
  Entry 0 - Port (0x1) Device Exclusive (0x1)
    Flags (0x01) - PORT_MEMORY PORT_IO
    Range starts at 0x3f8 for 0x8 bytes
  Entry 1 - Interrupt (0x2) Shared (0x3)
    Flags (0x01) - LATCHED
    Level 0x4, Vector 0x4, Affinity 0xffffffff
```

これには、I/O 範囲 3f8-3ff と IRQ 4 CM このリソースの一覧でデバイスを使用しているが表示されます。

[**! dc**](-dcs.md)  
この拡張機能は廃止されています--によってその機能が含まれているされて[ **! pci**](-pci.md)します。 参照してください、。 このセクションで後述する pci 100 例。

[**!devext**](-devext.md)  
バスに固有のデバイスのさまざまなデバイスの拡張機能の情報が表示されます。

[**! devnode**](-devnode.md)  
デバイス ツリー内のノードに関する情報を表示します。

[デバイス] ノード 0 (ゼロ) は、デバイス ツリーのルートです。

以下に例を示します。

```dbgcmd
0: kd> !devnode 0xfffffa8003634af0
DevNode 0xfffffa8003634af0 for PDO 0xfffffa8003658590
  Parent 0xfffffa8003604010   Sibling 0xfffffa80036508e0   Child 0000000000
  InstancePath is "ROOT\SYSTEM\0000"
  ServiceName is "swenum"
  State = DeviceNodeStarted (0x308)
  Previous State = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[09] = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[08] = DeviceNodeEnumeratePending (0x30c)
  StateHistory[07] = DeviceNodeStarted (0x308)
  StateHistory[06] = DeviceNodeStartPostWork (0x307)
  StateHistory[05] = DeviceNodeStartCompletion (0x306)
  StateHistory[04] = DeviceNodeStartPending (0x305)
  ...
  Flags (0x6c000131)  DNF_MADEUP, DNF_ENUMERATED, 
                      DNF_IDS_QUERIED, DNF_NO_RESOURCE_REQUIRED, 
                      DNF_NO_LOWER_DEVICE_FILTERS, DNF_NO_LOWER_CLASS_FILTERS, 
                      DNF_NO_UPPER_DEVICE_FILTERS, DNF_NO_UPPER_CLASS_FILTERS
  UserFlags (0x00000008)  DNUF_NOT_DISABLEABLE
  DisableableDepends = 1 (including self)
```

[**!devobj**](-devobj.md)  
デバイスに関する詳細な情報が表示されます\_オブジェクト。

以下に例を示します。

```dbgcmd
kd> !devobj 0xff0d4af0

Device object (ff0d4af0) is for:
 00252d \Driver\PnpManager DriverObject ff0d9030
Current Irp 00000000 RefCount 0 Type 00000004 Flags 00001040AttachedDev ff0b59e0

DevExt ff0d4ba8 DevNode ff0d4a08
Device queue is not busy.
```

[**! ドライバー**](-drivers.md)  
[ **! ドライバー** ](-drivers.md)コマンドがサポートされていません。 使用してください、 [ **lm t n** ](lm--list-loaded-modules-.md)コマンドを代わりにします。

[**!drvobj**](-drvobj.md)  
ドライバーに関する詳細な情報が表示されます\_オブジェクト。

指定したドライバーによって作成されたすべてのデバイス オブジェクトを一覧表示します。

以下に例を示します。

```dbgcmd
kd> !drvobj serial

Driver object (ff0ba630) is for:
 \Driver\Serial
Driver Extension List: (id , addr)

Device Object list:
ffba3040  ff0b4040  ff0b59e0  ff0b5040
```

[**! ecb、!、ecd! ecw**](-ecb---ecd---ecw.md)  
(x86 を対象コンピューターの場合のみ)PCI の構成領域には、値のシーケンスを書き込みます。

[**ib、インフォメーション ワーカーは、id**](-ib---id---iw.md)  
I/O ポートからデータを読み取ります。

これら 3 つのコマンドは、特定の I/O の範囲がデバッグされているドライバー以外のデバイスが要求したかどうかを決定するのに役立ちます。 ポートで 0 xff のバイト値では、ポートが使用されていないことを示します。

[**!ioreslist**](-ioreslist.md)  
指定した IO の表示\_リソース\_要件\_一覧。

[**! irp**](-irp.md)  
IRP についての情報を表示します。

[**! irpfind**](-irpfind.md)  
については、ターゲット システムに現在割り当てられているすべての Irp またはそれらの Irp フィールドが指定した検索条件に一致に関する情報が表示されます。

[**!pci**](-pci.md)  
(x86 を対象コンピューターの場合のみ)PCI バスとそれらに接続されているすべてのデバイスの現在の状態を表示します。 PCI の構成領域を表示することもできます。

次の例では、プライマリ バス上のデバイスが表示されます。

```dbgcmd
kd> !pci
PCI Bus 0
00:0  8086:1237.02  Cmd[0106:.mb..s]  Sts[2280:.....]  Device  Host bridge
0d:0  8086:7000.01  Cmd[0007:imb...]  Sts[0280:.....]  Device  ISA bridge
0d:1  8086:7010.00  Cmd[0005:i.b...]  Sts[0280:.....]  Device  IDE controller
0e:0  1011:0021.01  Cmd[0107:imb..s]  Sts[0280:.....]  PciBridge 0->1-1  PCI-PCI
 bridge
10:0  5333:8811.43  Cmd[0023:im.v..]  Sts[0200:.....]  Device  VGA compatible controller



The following example displays the devices for the secondary bus, with verbose output:

kd> !pci 1 1

PCI Bus 1
08:0  10b7:5900.00  Cmd[0107:imb..s]  Sts[0200:.....]  Device  Ethernet
      cf8:80014000  IntPin:1  IntLine:f  Rom:fa000000  cis:0  cap:0
      IO[0]:fce1

09:0  9004:8178.00  Cmd[0117:imb..s]  Sts[0280:.....]  Device  SCSI controller
      cf8:80014800  IntPin:1  IntLine:f  Rom:fa000000  cis:0  cap:0
      IO[0]:f801       MEM[1]:f9fff000

0b:0  9004:5800.10  Cmd[0116:.mb..s]  Sts[0200:.....]  Device  SubID:9004:8940
1394 host controller
      cf8:80015800  IntPin:1  IntLine:e  Rom:fa000000  cis:0  cap:0
      MEM[0]:f9ffec00
```

次の例では、SCSI コント ローラー (バス デバイス 9、関数 0、1) の PCI 構成領域が表示されます。

```dbgcmd
kd> !pci 100 1 9 0 
00: 9004    ;VendorID=9004
02: 8178    ;DeviceID=8178
04: 0117    ;Command=SERREnable,MemWriteEnable,BusInitiate,MemSpaceEnable,IOSpac
eEnable
06: 0280    ;Status=FB2BCapable,DEVSELTiming:1
08: 00      ;RevisionID=00
09: 00      ;ProgIF=00 (SCSI bus controller)
0a: 00      ;SubClass=00
0b: 01      ;BaseClass=01 (Mass storage controller)
0c: 08      ;CacheLineSize=Burst8DW
0d: 20      ;LatencyTimer=20
0e: 00      ;HeaderType=00
0f: 00      ;BIST=00
10: 0000f801;BAR0=0000f801
14: f9fff000;BAR1=f9fff000
18: 00000000;BAR2=00000000
1c: 00000000;BAR3=00000000
20: 00000000;BAR4=00000000
24: 00000000;BAR5=00000000
28: 00000000;CBCISPtr=00000000
2c: 0000    ;SubSysVenID=0000
2e: 0000    ;SubSysID=0000
30: fa000000;ROMBAR=fa000000
34: 00000000;Reserved=00000000
38: 00000000;Reserved=00000000
3c: 0f      ;IntLine=0f
3d: 01      ;IntPin=01
3e: 08      ;MinGnt=08
3f: 08      ;MaxLat=08
40: 00001580,00001580,00000000,00000000,00000000,00000000,00000000,00000000
60: 00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000000
80: 00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000000
a0: 00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000000
c0: 00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000000
e0: 00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000000
```

[**!pcitree**](-pcitree.md)  
子の PCI バスと CardBus バス、ほかに接続されているデバイスなど、PCI デバイス オブジェクトに関する情報を表示します。

[**!pnpevent**](-pnpevent.md)  
PnP デバイスのイベント キューが表示されます。

[**!rellist**](-rellist.md)  
PnP 関係一覧と、関連する CM 表示\_リソース\_一覧と IO\_リソース\_リストの構造体。

 

 





