---
title: キーボードからのシステム クラッシュの強制実行
description: キーボードからのシステム クラッシュの強制実行
ms.assetid: 0c3ec6f3-d233-46e4-b599-1a0f89318ed2
keywords:
- ブートプロセスが原因でキーボードからシステムがクラッシュする
- CTRL + スクロールロック
- システムのクラッシュ、キーボードからのクラッシュ
- バグチェック、キーボードからの発生
- キーボード-システムクラッシュの原因
- USB キーボードとシステムクラッシュ
- PS/2 キーボードとシステムクラッシュ
- キーボードからのシステムクラッシュの強制
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: a57f1daaee2bb7d435ae42931fa1e4cb1dca0254
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534367"
---
# <a name="forcing-a-system-crash-from-the-keyboard"></a>キーボードからのシステム クラッシュの強制実行

## <span id="ddk_forcing_a_system_crash_from_the_keyboard_dbg"></span><span id="DDK_FORCING_A_SYSTEM_CRASH_FROM_THE_KEYBOARD_DBG"></span>

次の種類のキーボードでは、システムのクラッシュが直接発生する場合があります。

<span id="________PS_2_keyboards_connected_on_i8042prt_ports_______"></span><span id="________ps_2_keyboards_connected_on_i8042prt_ports_______"></span><span id="________PS_2_KEYBOARDS_CONNECTED_ON_I8042PRT_PORTS_______"></span>**I8042prt ポートで接続されている PS/2 キーボード**

この機能は、Windows 2000 以降のバージョンの Windows オペレーティングシステムで使用できます。

<span id="________USB_keyboards_______"></span><span id="________usb_keyboards_______"></span><span id="________USB_KEYBOARDS_______"></span>**USB キーボード**

この機能は、Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。

<span id="hyper_v_keyboards_______"></span>**Hyper-v キーボード**

この機能は、Windows 10 バージョン1903以降のバージョンの Windows オペレーティングシステムで使用できます。

<span id="Configuration"></span> **構成**

キーボードを使用してシステムのクラッシュを有効にするには、次の設定を構成します。

1. クラッシュダンプファイルを書き込む場合は、そのようなダンプファイルを有効にし、パスとファイル名を選択して、ダンプファイルのサイズを選択する必要があります。 詳細については、「[カーネルモードダンプファイルの有効化](enabling-a-kernel-mode-dump-file.md)」を参照してください。

2. PS/2 キーボードを使用する場合は、レジストリでキーボードによるクラッシュを有効にする必要があります。 レジストリキー **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Services \\ i8042prt \\ Parameters**に**CrashOnCtrlScroll**という名前の値を作成し、それを REG \_ DWORD 値0x01 に設定します。

3. USB キーボードを使用する場合は、レジストリでキーボードによるクラッシュを有効にする必要があります。 レジストリキー **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Services \\ kbdhid \\ パラメーター**に、 **CrashOnCtrlScroll**という名前の値を作成し、それを REG \_ DWORD 値0x01 に設定します。

4. Hyper-v キーボードを使用する場合は、レジストリでキーボードによるクラッシュを有効にする必要があります。 レジストリキー **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\hyperkbd\parameters**に**CrashOnCtrlScroll**という名前の値を作成し、それを0x01 の REG_DWORD 値に設定します。

これらの設定を有効にするには、システムを再起動する必要があります。

この操作が完了したら、キーボードのクラッシュを開始するには、次のホットキーシーケンスを使用します。右の CTRL キーを押しながら、スクロールキーを2回押します。

その後、システムは**Kebugcheck**を呼び出し、[**バグチェック 0xe2**](bug-check-0xe2--manually-initiated-crash.md) (手動で開始されたクラッシュ) を発行し \_ \_ ます。 クラッシュダンプが無効になっていない限り、この時点でクラッシュダンプファイルが書き込まれます。

カーネルデバッガーがクラッシュしたマシンにアタッチされている場合、クラッシュダンプファイルが書き込まれた後、マシンはカーネルデバッガーに中断します。

この機能の使用方法の詳細については、「Windows の機能」を参照してください。[キーボードを使用して、メモリダンプファイルを生成する](https://support.microsoft.com/help/244139/windows-feature-lets-you-generate-a-memory-dump-file-by-using-the-keyb)ことができます。

### <a name="span-iddefining_alternate_keyboard_shortcuts_to_force_a_system_crash_from_thespanspan-iddefining_alternate_keyboard_shortcuts_to_force_a_system_crash_from_thespandefining-alternate-keyboard-shortcuts-to-force-a-system-crash-from-the-keyboard"></a><span id="defining_alternate_keyboard_shortcuts_to_force_a_system_crash_from_the"></span><span id="DEFINING_ALTERNATE_KEYBOARD_SHORTCUTS_TO_FORCE_A_SYSTEM_CRASH_FROM_THE"></span>キーボードからのシステムクラッシュを強制する代替キーボードショートカットの定義

次のレジストリサブキーの下で、メモリダンプファイルを生成するためのさまざまなキーボードショートカットシーケンスの値を構成できます。

- PS/2 キーボードの場合:

    **HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Services \\ i8042prt \\ クラッシュ**

- USB キーボードの場合:

    **HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Services \\ kbdhid \\ クラッシュ**

- Hyper-v キーボードの場合:

    **HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\hyperkbd\crashdump**

これらのサブキーの下に、次のレジストリ REG DWORD 値を作成する必要があり \_ ます。

<span id="Dump1Keys"></span><span id="dump1keys"></span><span id="DUMP1KEYS"></span>**Dump1Keys**  
**Dump1Keys**レジストリ値は、使用する最初のホットキーのビットマップです。 たとえば、ホットキーシーケンスを開始するために右端の CTRL キーを使用するのではなく、最初のホットキーを左端の SHIFT キーに設定できます。

次の表では、最初のホットキーの値について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">キーボードショートカットシーケンスで使用される最初のキー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>右の SHIFT キー</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>右端の CTRL キー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>右端の ALT キー</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>左端の SHIFT キー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>左端の CTRL キー</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x40</p></td>
<td align="left"><p>左端の ALT キー</p></td>
</tr>
</tbody>
</table>

**メモ**   **Dump1Keys**には、キーボードショートカットシーケンスで使用される最初のキーとして1つ以上のキーを有効にする値を割り当てることができます。 たとえば、 **Dump1Keys**の値を0x11 に設定すると、キーボードショートカットシーケンスの最初のキーとして、右端と左端の両方の SHIFT キーが定義されます。

<span id="Dump2Key"></span><span id="dump2key"></span><span id="DUMP2KEY"></span>**Dump2Key**  
**Dump2Key**レジストリ値は、対象のコンピューターのキーボードレイアウト用の scancode テーブルのインデックスです。 ドライバーの実際のテーブルを次に示します。

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

**メモ**   インデックス 124 (sysreq) は特殊なケースです。これは、84キーのキーボードのスキャンコードが異なるためです。

USB または PS/2 キーボードからシステムクラッシュを強制する代替キーボードショートカットを定義する場合は、 **CrashOnCtrlScroll**レジストリ値を0に設定するか、レジストリから削除する必要があります。

### <a name="span-idlimitationsspanspan-idlimitationsspanlimitations"></a><span id="limitations"></span><span id="LIMITATIONS"></span>制限事項

キーボードショートカットシーケンスが機能しないようにシステムをフリーズさせることができます。 ただし、これはめったに発生しません。 キーボードショートカットシーケンスを使用してクラッシュを開始することは、CTRL + ALT + DELETE が機能しない多くのインスタンスでも機能します。

コンピューターが高い割り込み要求レベル (IRQL) で応答を停止した場合、キーボードからのシステムクラッシュの強制は機能しません。 この制限は、メモリダンププロセスの実行を許可する Kbdhid .sys ドライバーが、i8042prt ドライバーよりも低い IRQL で動作するために発生します。
