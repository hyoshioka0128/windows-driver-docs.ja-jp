---
title: キーボードからのシステム クラッシュの強制実行
description: キーボードからのシステム クラッシュの強制実行
ms.assetid: 0c3ec6f3-d233-46e4-b599-1a0f89318ed2
keywords:
- 起動プロセス、キーボードからシステムのクラッシュの原因
- CTRL + SCROLL LOCK
- キーボードの原因と、システムのクラッシュ
- キーボードからのバグ チェック
- キーボードによるシステムのクラッシュ
- USB キーボードとシステムのクラッシュ
- Ps/2 キーボードとシステムのクラッシュ
- キーボードから強制的にシステムのクラッシュ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 728380861030e3add4703505836eeb7ecbd807be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371700"
---
# <a name="forcing-a-system-crash-from-the-keyboard"></a>キーボードからのシステム クラッシュの強制実行


## <span id="ddk_forcing_a_system_crash_from_the_keyboard_dbg"></span><span id="DDK_FORCING_A_SYSTEM_CRASH_FROM_THE_KEYBOARD_DBG"></span>


次のキーボードのほとんどは、直接システム クラッシュを引き起こすことができます。

<span id="________PS_2_keyboards_connected_on_i8042prt_ports_______"></span><span id="________ps_2_keyboards_connected_on_i8042prt_ports_______"></span><span id="________PS_2_KEYBOARDS_CONNECTED_ON_I8042PRT_PORTS_______"></span> I8042prt ポートで ps/2 キーボードが接続されています。   
この機能は、Windows 2000 およびそれ以降のバージョンの Windows オペレーティング システムで使用できます。

<span id="________USB_keyboards_______"></span><span id="________usb_keyboards_______"></span><span id="________USB_KEYBOARDS_______"></span> USB キーボード   
この機能はあります。

-   Windows Server 2003 Service Pack 1 場合に使用可能な修正プログラム[KB 244139](https://go.microsoft.com/fwlink/p/?linkid=106065)がインストールされています。

-   Windows Server 2003 (Service Pack 2 またはそれ以降)。

-   Windows Vista Service Pack 1 場合に使用可能な修正プログラム[KB 971284](https://go.microsoft.com/fwlink/p/?LinkId=241349)がインストールされています。

-   Windows Vista Service Pack 2。

-   Windows Server 2008 Service Pack 1 場合に使用可能な修正プログラム[KB 971284](https://go.microsoft.com/fwlink/p/?LinkId=241349)がインストールされています。
-   Windows Server 2008 (Service Pack 2 またはそれ以降)。
-   Windows 7 およびそれ以降のバージョンの Windows オペレーティング システム。

**注**  この機能は Windows XP では使用できません。

 

キーボードできますシステム クラッシュが発生する前に、次の 3 つの設定を確認する必要があります。

1.  このようなダンプ ファイルを有効にする必要があります、書き込まれるクラッシュ ダンプ ファイルを希望する場合、パスとファイル名を選択し、ダンプ ファイルのサイズを選択します。 詳細については、次を参照してください。[カーネル モードのダンプ ファイルを有効にする](enabling-a-kernel-mode-dump-file.md)します。

2.  Ps/2 キーボードでは、レジストリにキーボードによるクラッシュを有効にする必要があります。 レジストリ キーに**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス\\i8042prt\\パラメーター**、という名前の値を作成**します**、21 と等しい設定\_DWORD 値 0x01 になります。

3.  USB キーボードでレジストリにキーボードによるクラッシュを有効にする必要があります。 レジストリ キーに**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス\\kbdhid\\パラメーター、** を作成します。という名前の値**します**、21 と等しい設定\_DWORD 値 0x01 になります。

これらの設定を有効にするためにシステムを再起動する必要があります。

これが完了した後は、次のホットキーを使用して、キーボードのクラッシュを開始できます。右端の CTRL キーを押しながら、SCROLLLOCK キーを 2 回押します。

システムを呼び出して**KeBugCheck**と問題[**バグ チェック 0 xe2** ](bug-check-0xe2--manually-initiated-crash.md) (手動で\_INITIATED\_クラッシュ)。 クラッシュ ダンプを無効になっている場合を除き、この時点で、クラッシュ ダンプ ファイルが書き込まれます。

カーネル デバッガーがクラッシュしたマシンに接続されている場合は、クラッシュ ダンプ ファイルが書き込まれた後、カーネル デバッガーに、マシンが中断されます。

この機能の使用に関する詳細については、この記事を参照してください[キーボード (KB 244139) を使用して、メモリ ダンプ ファイルを生成](https://go.microsoft.com/fwlink/p/?linkid=106065)します。

### <a name="span-iddefiningalternatekeyboardshortcutstoforceasystemcrashfromthespanspan-iddefiningalternatekeyboardshortcutstoforceasystemcrashfromthespandefining-alternate-keyboard-shortcuts-to-force-a-system-crash-from-the-keyboard"></a><span id="defining_alternate_keyboard_shortcuts_to_force_a_system_crash_from_the"></span><span id="DEFINING_ALTERNATE_KEYBOARD_SHORTCUTS_TO_FORCE_A_SYSTEM_CRASH_FROM_THE"></span>キーボードからシステムのクラッシュを強制的に代替のキーボード ショートカットを定義します。

メモリ ダンプ ファイルを生成するさまざまなキーボード ショートカットのシーケンスの次のレジストリ サブキーの下に値を構成できます。

-   Ps/2 キーボードの場合。

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\i8042prt\\crashdump**

-   USB キーボードの場合。

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\kbdhid\\crashdump**

REG の次のレジストリを作成する必要があります\_これらのサブキーの下に DWORD 値。

<span id="Dump1Keys"></span><span id="dump1keys"></span><span id="DUMP1KEYS"></span>**Dump1Keys**  
**Dump1Keys**レジストリ値が使用する最初のホット キーのビット マップします。 たとえば、ホット キー シーケンスを開始する最も右にある、CTRL キーを使用する代わりに、最初のホット キーを一番左の SHIFT キーを設定できます。

最初のホット キーの値は、次の表で説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">キーボード ショートカットのシーケンスで使用される最初のキー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>一番右の SHIFT キー</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>右端の CTRL キー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>一番右 ALT キー</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>一番左の SHIFT キー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>一番左 CTRL キー</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x40</p></td>
<td align="left"><p>一番左 ALT キー</p></td>
</tr>
</tbody>
</table>

 

**注**  割り当てることができます**Dump1Keys**キーボード ショートカットのシーケンスで使用される最初のキーとして 1 つまたは複数のキーを有効にする値。 たとえば、割り当てる**Dump1Keys**キーボード ショートカットのシーケンスの最初のキーとしての右端と左端の両方の SHIFT キーを定義するパターンの値。

 

<span id="Dump2Key"></span><span id="dump2key"></span><span id="DUMP2KEY"></span>**Dump2Key**  
**Dump2Key**レジストリ値は、ターゲット コンピューターのキーボード レイアウト scancode テーブルにインデックス。 ドライバーでは、実際のテーブルを次に示します。

```cpp
const UCHAR keyToScanTbl[134] = { 
        0x00,0x29,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,
        0x0A,0x0B,0x0C,0x0D,0x7D,0x0E,0x0F,0x10,0x11,0x12,
        0x13,0x14,0x15,0x16,0x17,0x18,0x19,0x1A,0x1B,0x00,
        0x3A,0x1E,0x1F,0x20,0x21,0x22,0x23,0x24,0x25,0x26,
        0x27,0x28,0x2B,0x1C,0x2A,0x00,0x2C,0x2D,0x2E,0x2F,
        0x30,0x31,0x32,0x33,0x34,0x35,0x73,0x36,0x1D,0x00,
        0x38,0x39,0xB8,0x00,0x9D,0x00,0x00,0x00,0x00,0x00,
        0x00,0x00,0x00,0x00,0x00,0xD2,0xD3,0x00,0x00,0xCB,
        0xC7,0xCF,0x00,0xC8,0xD0,0xC9,0xD1,0x00,0x00,0xCD,
        0x45,0x47,0x4B,0x4F,0x00,0xB5,0x48,0x4C,0x50,0x52,
        0x37,0x49,0x4D,0x51,0x53,0x4A,0x4E,0x00,0x9C,0x00,
        0x01,0x00,0x3B,0x3C,0x3D,0x3E,0x3F,0x40,0x41,0x42,
        0x43,0x44,0x57,0x58,0x00,0x46,0x00,0x00,0x00,0x00,
        0x00,0x7B,0x79,0x70 };
```

**注**   84 キーボードに別のスキャン コードがあるために、インデックス 124 (sysreq) は特殊なケースです。

 

設定する必要があります、USB、ps/2 キーボードからシステムのクラッシュを強制的に代替のキーボード ショートカットを定義する場合、**します**レジストリ値を 0 またはレジストリから削除します。

### <a name="span-idlimitationsspanspan-idlimitationsspanlimitations"></a><span id="limitations"></span><span id="LIMITATIONS"></span>制限事項

システム固定キーボード ショートカットのシーケンスは、このような方法で作業することができます。 ただし、非常にまれな場合があります。 キーボード ショートカットのシーケンスを使用して、クラッシュを開始するは、CTRL + ALT + DEL が機能しないという多数のインスタンスであっても機能します。

キーボードから強制的にシステムがクラッシュしても、コンピューターが高い割り込み要求レベル (IRQL) で応答を停止した場合は機能しません。 この制限は、メモリ ダンプ プロセスの実行をできる Kbdhid.sys ドライバーが i8042prt.sys のドライバーよりも低いかどうかで動作するために存在します。

 

 





