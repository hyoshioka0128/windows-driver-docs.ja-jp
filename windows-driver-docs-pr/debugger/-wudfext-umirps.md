---
title: wudfext.umirps
description: Wudfext.umirps 拡張機能では、ホスト プロセスで保留中の I/O 要求パケット (Irp UM) のユーザー モードの一覧が表示されます。
ms.assetid: bba78784-f4f5-432c-ad5e-837770de79d9
keywords:
- デバッグ wudfext.umirps Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umirps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 472d5d58584662ba19e9d2940c0f8e67da8ccc9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347926"
---
# <a name="wudfextumirps"></a>!wudfext.umirps


**! Wudfext.umirps**拡張機能は、ホスト プロセスで保留中の I/O 要求パケット (Irp UM) のユーザー モードの一覧を表示します。

```dbgcmd
!wudfext.umirps NumberOfIrps Flags
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______NumberOfIrps______"></span><span id="_______numberofirps______"></span><span id="_______NUMBEROFIRPS______"></span> *NumberOfIrps*   
(省略可能)。 に関する情報を表示するための Irp UM 保留中の数を指定します。 場合*NumberOfIrps*にアスタリスク (\*)、または省略すると、すべての UM すべて UM Irp が表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、0x01 です。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>Bit 0 (0x01)  
保留中の Irp の詳細を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

表示される Irp UM 保留中の一覧は、ドライバーが紹介されていますか、またはドライバーに提示するを待機しています。

既定では、 **! wudfext.umirps**すべて UM Irp を示しています。 ただし、使用することができます、 *NumberOfIrps*この表示を制限するパラメーター。

例を次に、 **! wudfext.umirps**表示。

```dbgcmd
kd> !umirps 0xa 
Number of pending IRPS: 0xc8
####  CWudfIrp          Type        UniqueId          KernelIrp
----  ----------------  ----------  ----------------  ---------
0000            3dd280        READ                dc  856f02f0
0001            3dd380       WRITE                dd  85b869e0
0002            3dd480        READ                de  85377850
0003            3dd580        READ                df  93bba4e8
0004            3dd680       WRITE                e0  84cb9d70
0005            3dd780        READ                e1  85bec150
0006            3dd880       WRITE                e2  86651db0
0007            3dd980        READ                e3  85c22818
0008            3dda80        READ                e4  9961d150
0009            3ddb80       WRITE                e5  85c15148
```

対応するカーネル モード IRP を調べるには、 [ **! wudfext.wudfdownkmirp** ](-wudfext-wudfdownkmirp.md)拡張機能。 内の値を使用する代わりに、 **UniqueId**と**KernelIrp** UMDF IRP (または IRP UM) を対応するカーネル IRP に一致する列。 内の値を渡すことができます、 **CWudfIrp**列を[ **! wudfext.umirp** ](-wudfext-umirp.md)拡張機能フレームワークを判断する**IWDFRequest**デバイス スタックの各層にアクセスできるオブジェクト。

 

 





