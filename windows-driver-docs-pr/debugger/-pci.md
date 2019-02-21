---
title: pci
description: Pci の拡張機能では、周辺機器のコンポーネントの相互接続 (PCI) バスとするバスに接続されているすべてのデバイスの現在の状態が表示されます。
ms.assetid: 37b767db-18c9-4fd3-8910-4be03f41e764
keywords:
- PCI バス
- PCI デバイス
- PCI 構成領域
- Windows デバッグ pci
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pci
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1ee88676db2e019d7c96c26d14d800cf646b1e73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537512"
---
# <a name="pci"></a>! pci


**! Pci**拡張機能には、周辺機器のコンポーネントの相互接続 (PCI) バスとするバスに接続されているすべてのデバイスの現在の状態が表示されます。

```dbgcmd
!pci [Flags [Segment] [Bus [Device [Function [MinAddress MaxAddress]]]]]
```

## <a name="span-idddkpcidbgspanspan-idddkpcidbgspanparameters"></a><span id="ddk__pci_dbg"></span><span id="DDK__PCI_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
出力のレベルを指定します。 次のビットの任意の組み合わせを指定できます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
詳細の表示をによりします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
表示の bus 0 (ゼロ) を指定した範囲内ですべてのバスを含める*Bus*します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
未フォーマットの形式の情報が追加ディスプレイをによりします。 場合*MinAddress*、 *MaxAddress*、またはフラグ ビット 0x8 が設定されて、このビットはも自動的に設定します。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
DWORD の未加工の形式の情報が追加ディスプレイをによりします。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
無効なデバイスの番号が表示をによりします。 場合*デバイス*指定すると、このフラグは無視されます。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>Bit 5 (0x20)  
無効な関数番号を記載するためにディスプレイをによりします。

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>ビット 6 (0x40)  
機能するためにディスプレイをによりします。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>ビット 7 (0x80)  
Intel 8086 デバイスに固有の情報が追加ディスプレイをによりします。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>ビット 8 (0x100)  
PCI の構成領域が表示をによりします。

<span id="Bit_9__0x200_"></span><span id="bit_9__0x200_"></span><span id="BIT_9__0X200_"></span>ビット 9 (0x200)  
セグメントの情報が追加ディスプレイをによりします。 このビットが含まれている場合、*セグメント*パラメーターを含める必要があります。

<span id="Bit_10__0x400_"></span><span id="bit_10__0x400_"></span><span id="BIT_10__0X400_"></span>ビット 10 (0x400)  
セグメントは 0 から指定されたセグメントの範囲に有効なすべてのセグメントを含める表示をによりします。 このビットが含まれている場合、*セグメント*パラメーターを含める必要があります。

<span id="_______Segment______"></span><span id="_______segment______"></span><span id="_______SEGMENT______"></span> *セグメント*   
表示されるセグメントの数を指定します。 0 から 0 xffff までの数値の範囲を分割します。 場合*セグメント*は省略すると、プライマリのセグメント (セグメント 0) に関する情報が表示されます。 場合*フラグ*ビット 10 (0x400) が含まれています*セグメント*表示される最上位の有効なセグメントを指定します。

<span id="_______Bus______"></span><span id="_______bus______"></span><span id="_______BUS______"></span> *バス*   
表示するバスを指定します。 *バス*0 xff までの範囲のことができます。 省略した場合は、プライマリ バス (バス 0) に関する情報が表示されます。 場合*フラグ*ビット 1 (0x2) が含まれています*Bus*表示バス番号の最大値を指定します。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span> *デバイス*   
デバイスのデバイスのスロット番号を指定します。 これを省略すると、すべてのデバイスに関する情報が出力されます。

<span id="_______Function______"></span><span id="_______function______"></span><span id="_______FUNCTION______"></span> *関数*   
デバイスのスロットの関数の数を指定します。 これを省略すると、すべてのデバイス機能に関するすべての情報が出力されます。

<span id="_______MinAddress______"></span><span id="_______minaddress______"></span><span id="_______MINADDRESS______"></span> *MinAddress*   
最初の生バイトまたは Dword で表示するのには元のアドレスを指定します。 これは、は、0 から 0 xff までの間でなければなりません。

<span id="_______MaxAddress______"></span><span id="_______maxaddress______"></span><span id="_______MAXADDRESS______"></span> *MaxAddress*   
実際のバイト数または Dword で表示されるの元の最後のアドレスを指定します。 0 ~ 0 xff の場合、このことがありより小さくない*MinAddress*します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kext.dll Kdextx86.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>



この拡張機能のコマンドは、x86 ベースの移行先のコンピューターでのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドおよびその他の例のアプリケーション。 PCI バスについては、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

PCI の構成領域を編集する使用[ **。 ecb**](-ecb---ecd---ecw.md)、 **! ecd**、または **! ecw**します。

次の例では、すべてのバスと自分のデバイスの一覧が表示されます。 このコマンドには、実行に長い時間がかかります。 デバッガーがターゲット システムには、PCI バスをスキャン中に、画面の下部にある移動カウンターが表示されます。

```dbgcmd
kd> !pci 2 ff
PCI Bus 0
00:0  8086:1237.02  Cmd[0106:.mb..s]  Sts[2280:.....]  Device  Host bridge
0d:0  8086:7000.01  Cmd[0007:imb...]  Sts[0280:.....]  Device  ISA bridge
0d:1  8086:7010.00  Cmd[0005:i.b...]  Sts[0280:.....]  Device  IDE controller
0e:0  1011:0021.02  Cmd[0107:imb..s]  Sts[0280:.....]  PciBridge 0->1-1  PCI-PCI bridge
10:0  102b:0519.01  Cmd[0083:im....]  Sts[0280:.....]  Device  VGA compatible controller
PCI Bus 1
08:0  10b7:9050.00  Cmd[0107:imb..s]  Sts[0200:.....]  Device  Ethernet
09:0  9004:8178.00  Cmd[0117:imb..s]  Sts[0280:.....]  Device  SCSI controller
```

この例では、プライマリ バス上のデバイスの詳細情報を表示します。 各行の先頭に 2 桁の数字は、デバイスの数。後に 1 桁の数字は、関数の数を示します。

```dbgcmd
kd> !pci 1 0
PCI Bus 0
00:0  8086:1237.02  Cmd[0106:.mb..s]  Sts[2280:.....]  Device  Host bridge
      cf8:80000000  IntPin:0  IntLine:0  Rom:0  cis:0  cap:0

0d:0  8086:7000.01  Cmd[0007:imb...]  Sts[0280:.....]  Device  ISA bridge
      cf8:80006800  IntPin:0  IntLine:0  Rom:0  cis:0  cap:0

0d:1  8086:7010.00  Cmd[0005:i.b...]  Sts[0280:.....]  Device  IDE controller
      cf8:80006900  IntPin:0  IntLine:0  Rom:0  cis:0  cap:0
      IO[4]:fff1       

0e:0  1011:0021.02  Cmd[0107:imb..s]  Sts[0280:.....]  PciBridge 0->1-1  PCI-PCI bridge
      cf8:80007000  IntPin:0  IntLine:0  Rom:0  cap:0  2sts:2280  BCtrl:6 ISA
      IO:f000-ffff  Mem:fc000000-fdffffff  PMem:fff00000-fffff

10:0  102b:0519.01  Cmd[0083:im....]  Sts[0280:.....]  Device  VGA compatible controller
      cf8:80008000  IntPin:1  IntLine:9  Rom:80000000  cis:0  cap:0
      MEM[0]:fe800000  MPF[1]:fe000008  
```

この例では、さらに詳しい情報に関する bus 0 (ゼロ)、デバイス 0x0D、関数 0x1、0x00 と 0x3F 間のアドレスから生の DWORD を含みます。

```dbgcmd
kd> !pci f 0 d 1 0 3f
PCI Bus 0
0d:1  8086:7010.00  Cmd[0005:i.b...]  Sts[0280:.....]  Device  IDE controller
      cf8:80006900  IntPin:0  IntLine:0  Rom:0  cis:0  cap:0
      IO[4]:fff1       
      00000000:  70108086 02800005 01018000 00002000
      00000010:  00000000 00000000 00000000 00000000
      00000020:  0000fff1 00000000 00000000 00000000
      00000030:  00000000 00000000 00000000 00000000
```

この例では、セグメントは 1、0、デバイス 1 のバスの構成領域が表示されます。

```dbgcmd
0: kd> !pci 301 1 0 1

PCI Configuration Space (Segment:0001 Bus:00 Device:01 Function:00)
Common Header:
    00: VendorID       14e4 Broadcom Corporation
    02: DeviceID       16c7
    04: Command        0146 MemSpaceEn BusInitiate PERREn SERREn
    06: Status         02b0 CapList 66MHzCapable FB2BCapable DEVSELTiming:1
.
.
.
    5a: MsgCtrl        64BitCapable MultipleMsgEnable:0 (0x1) MultipleMsgCapable:3 (0x8)
    5c: MsgAddr        2d4bff00
    60: MsgAddrHi      1ae09097
    64: MsData         9891
```

すべてのデバイスとバスの有効なセグメントを表示するには、コマンドを発行 **! pci 602 ffff ff**:

```dbgcmd
0: kd> !pci 602 ffff ff
Scanning the following PCI segments: 0 0x1
PCI Segment 0 Bus 0
01:0  14e4:16c7.10  Cmd[0146:.mb.ps]  Sts[02b0:c6...]  Ethernet Controller  SubID:103c:1321
02:0  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
02:1  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
03:0  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
03:1  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
PCI Segment 0 Bus 0x38
01:0  14e4:1644.12  Cmd[0146:.mb.ps]  Sts[02b0:c6...]  Ethernet Controller  SubID:10b7:1000
PCI Segment 0 Bus 0x54
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0x54->0x55-0x55
PCI Segment 0 Bus 0x70
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0x70->0x71-0x71
PCI Segment 0 Bus 0xa9
01:0  8086:b154.00  Cmd[0147:imb.ps]  Sts[0ab0:c6.A.]  Intel PCI-PCI Bridge 0xa9->0xaa-0xaa
PCI Segment 0 Bus 0xaa
04:0  1033:0035.41  Cmd[0146:.mb.ps]  Sts[0210:c....]  NEC USB Controller  SubID:103c:1293
04:1  1033:0035.41  Cmd[0146:.mb.ps]  Sts[0210:c....]  NEC USB Controller  SubID:103c:aa55
04:2  1033:00e0.02  Cmd[0146:.mb.ps]  Sts[0210:c....]  NEC USB2 Controller  SubID:103c:aa55
05:0  1002:5159.00  Cmd[0187:imb..s]  Sts[0290:c....]  ATI VGA Compatible Controller  SubID:103c:1292
PCI Segment 0 Bus 0xc6
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0xc6->0xc7-0xc7
PCI Segment 0 Bus 0xe3
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0xe3->0xe4-0xe4
PCI Segment 0x1 Bus 0
01:0  14e4:16c7.10  Cmd[0146:.mb.ps]  Sts[02b0:c6...]  Ethernet Controller  SubID:103c:1321
02:0  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
02:1  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
03:0  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
03:1  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
PCI Segment 0x1 Bus 0x54
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0x54->0x55-0x55
PCI Segment 0x1 Bus 0x55
00:0  8086:10b9.06  Cmd[0147:imb.ps]  Sts[0010:c....]  Intel Ethernet Controller  SubID:8086:1083
PCI Segment 0x1 Bus 0x70
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0x70->0x71-0x71
PCI Segment 0x1 Bus 0xc6
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0xc6->0xc7-0xc7
PCI Segment 0x1 Bus 0xe3
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0xe3->0xe4-0xe4
```









