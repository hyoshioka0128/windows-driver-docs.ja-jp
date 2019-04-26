---
title: ks.pciks
description: Ks.pciks 拡張機能には、PCI バスに接続されているデバイスをストリーミングするカーネル用の機能のデバイスが一覧表示します。 必要に応じて、それらの機能のデバイスのアクティブな streams についての情報を表示できます。
ms.assetid: 525eb1eb-4b96-46da-90ae-d3c5f8d7511a
keywords:
- デバッグ ks.pciks Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.pciks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5c202a4c9985225e8c43ec5dfd36a566bb15e129
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336230"
---
# <a name="kspciks"></a>!ks.pciks


**! Ks.pciks**拡張機能には、PCI バスに接続されているデバイスをストリーミングするカーネル用の機能のデバイスが一覧表示されます。 必要に応じて、それらの機能のデバイスのアクティブな streams についての情報を表示できます。

```dbgcmd
!ks.pciks [Flags] [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
任意。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
現在実行中のすべてのストリームを一覧表示します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
非 PCI デバイスを検索するグラフを再帰処理します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
プロキシ インスタンスの一覧を表示します。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
現在キューに置かれた Irp を表示します。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
すべてのストリームに関する情報を表示します。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>Bit 5 (0x20)  
アクティブな stream の形式を表示します。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
省略可能、およびデータを表示するフラグの組み合わせに対してのみ適用できます。 レベルは、の場合と同じ[ **! ks.dump**](-ks-dump.md)します。

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

このコマンドは、ACPI フィルター ドライバーが読み込まれる場合や、ドライバーの検証が有効になっているし、ドライバー名をページ アウトの場合、実行に時間をかかる場合があります。

次の例に示します、 **! ks.pciks**表示。

```dbgcmd
kd> !pciks
1 Kernel Streaming FDOs found:
    Functional Device 82a17690 [\Driver\smwdm]
```

 

 





