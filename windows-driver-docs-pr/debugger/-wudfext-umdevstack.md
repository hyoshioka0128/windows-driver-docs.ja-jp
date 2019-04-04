---
title: wudfext.umdevstack
description: Wudfext.umdevstack 拡張機能では、ホスト プロセスでデバイス スタックに関する詳細情報が表示されます。
ms.assetid: 3cce0e30-ea04-4587-9208-b6a7d51fd44a
keywords:
- デバッグ wudfext.umdevstack Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umdevstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d0b715e70d69a55e28dc47160ca9a1d3ea7e1262
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557321"
---
# <a name="wudfextumdevstack"></a>!wudfext.umdevstack


**! Wudfext.umdevstack**拡張機能は、ホスト プロセスでデバイス スタックに関する詳細情報を表示します。

```dbgcmd
!wudfext.umdevstack DevstackAddress [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DevstackAddress______"></span><span id="_______devstackaddress______"></span><span id="_______DEVSTACKADDRESS______"></span> *DevstackAddress*   
に関する情報を表示するデバイスのスタックのアドレスを指定します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、0x01 です。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>Bit 0 (0x01)  
詳細については、デバイス スタックを表示します。

<span id="Bit_8__0x80_"></span><span id="bit_8__0x80_"></span><span id="BIT_8__0X80_"></span>8 ビット (0x80)  
内部のフレームワークについての情報を表示します。

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

 

### <a name="span-idadditionalinformation1spanspan-idadditionalinformation1spanadditional-information"></a><span id="additional_information1"></span><span id="ADDITIONAL_INFORMATION1"></span>追加情報

詳細については、[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

例を次に、 **! wudfext.umdevstack**表示。

```dbgcmd
kd> !umdevstack 0x0034e4e0
Device Stack: 0x0034e4e0  Pdo Name: \Device\00000057
 Number of UM drivers: 0x1
  Driver 00:
    Driver Config Registry Path: WUDFEchoDriver
    UMDriver Image Path: C:\Windows\system32\DRIVERS\UMDF\WUDFEchoDriver.dll
    Fx Driver: IWDFDriver 0xf2db8
    Fx Device: IWDFDevice 0xf2f80
        IDriverEntry: WUDFEchoDriver!CMyDriver 0x000f2c70
```

 

 





