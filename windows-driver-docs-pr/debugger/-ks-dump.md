---
title: ks.dump
description: Ks.dump 拡張機能では、指定したオブジェクトが表示されます。
ms.assetid: 7878c79f-9de6-4fd2-9641-c636212429eb
keywords:
- デバッグ ks.dump Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 81b6db8685a6b6841febcbec68379362a2eab817
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336660"
---
# <a name="ksdump"></a>!ks.dump


**! Ks.dump**拡張機能には、指定したオブジェクトが表示されます。

```dbgcmd
!ks.dump Object [Level] [Flags]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
AVStream 構造体、AVStream クラス オブジェクト、または PortCls オブジェクトへのポインターを指定します。 IRP またはファイル オブジェクトへのポインターを指定することもできます。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
(省略可能)。 0 ~ 7 で表示する詳細のレベルを指定の値を大きく表示徐々 に詳細なスケールします。 使用可能なすべての詳細を表示するには、7 の値を指定します。 発行することによってレベルの詳細を確認できます、 **! ks.dump**引数なしでコマンド。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
任意。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
すべてのキューに置かれた Irp を表示します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
保留中のすべての Irp を表示します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
%Sort% ストールしたグラフを分析します。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
暗証番号 (pin) のすべての状態を示してください。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)します。

<a name="remarks"></a>コメント
-------

**! Ks.dump**コマンドは、pin、フィルター、ファクトリ、デバイス、パイプ、およびストリーム ポインターを含む、ほとんどの AVStream オブジェクトを認識します。 このコマンドは、ストリーム オブジェクト、フィルター インスタンス、デバイスの拡張機能、およびされる Srb など、一部のストリーム クラス構造を認識します。

例を次に、 **! ks.dump**フィルターの表示。

```dbgcmd
kd> !dump 829493c4
Filter object 829493c4 [CKsFilter = 82949350]
    Descriptor     f7a233c8:
    Context        829dce28
```

例を次に、 **! ks.dump**ピンの表示。

```dbgcmd
kd> !dump 8160DDE0 7
Pin object 8160DDE0 [CKsPin = 8160DD50]
    DeviceState    KSSTATE_RUN
    ClientState    KSSTATE_RUN
    ResetState     KSRESET_END
    CKsPin object 8160DD50 [KSPIN = 8160DDE0]
        State                    KSSTATE_RUN
        Processing Mutex         8160DFD0 is not held
        And Gate &               8160DF88
        And Gate Count           1
```

次の表では、この表示のいくつかの重要な部分が含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>パラメーター</strong></p></td>
<td align="left"><p><strong>意味</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>DeviceState</p></td>
<td align="left"><p>ピンの状態が入力を要求します。 ClientState から別にある場合、ミニドライバーは、[次へ] を移行する状態です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ClientState</p></td>
<td align="left"><p>状態、ミニドライバーは実際にです。 これには、パイプの状態が反映されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ResetState</p></td>
<td align="left"><p>フラッシュを途中で、オブジェクトであるかどうかを示します。</p>
<p>KSRESET_BEGIN では、フラッシュを示します。</p>
<p>KSRESET_END はフラッシュがないことを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>状態</p></td>
<td align="left"><p>非 AVStream フィルターに暗証番号 (pin) のトランスポートの内部状態。</p></td>
</tr>
</tbody>
</table>

 

例を次に、 **! ks.dump**ストリーム クラス ドライバーの表示。

```dbgcmd
kd> !dump 81a0a170 7
Device Extension 81a0a228:
    Device Object          81a0a170 [\Driver\TESTCAP]
    Next Device Object     81bd56d8 [\Driver\PnpManager]
    Physical Device Object 81bd56d8 [\Driver\PnpManager]
    REGISTRY FLAGS:
        Page out driver when closed
        No suspend if running
    MINIDRIVER Data:
        Device Extension       81a0a44c
        Interrupt Routine      00000000
        Synchronize Routine    STREAM!StreamClassSynchronizeExecution
        Receive Device SRB     testcap!AdapterReceivePacket
        Cancel Packet          testcap!AdapterCancelPacket
        Timeout Packet         testcap!AdapterTimeoutPacket
        Size (d / r / s / f)   1a0(416), 14(20), 978(2424), 0(0)
        Sync Mode              Driver Synchronizes
    Filter Type 0:
        Symbolic Links:
            Information Paged Out
        Instances:
            816b7bd8
```

サイズが表示されていることに注意してください、16 進数の両方をクリックし、10 進数の相当のかっこ内で。 この表示でサイズの省略形は、次の表に一覧表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Size</strong></p></td>
<td align="left"><p><strong>説明</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>d</p></td>
<td align="left"><p>デバイス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>r</p></td>
<td align="left"><p>要求</p></td>
</tr>
<tr class="even">
<td align="left"><p>s</p></td>
<td align="left"><p>[ストリーミング]</p></td>
</tr>
<tr class="odd">
<td align="left"><p>f</p></td>
<td align="left"><p>フィルター処理します。 フィルターのサイズが 0 の場合、フィルターは、1 つのインスタンスです。 0 より大きい場合は、複数インスタンスです。</p></td>
</tr>
</tbody>
</table>

 

 

 





