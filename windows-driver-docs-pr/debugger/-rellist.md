---
title: rellist
description: Rellist 拡張機能では、プラグ アンド プレイの関係の一覧が表示されます。
ms.assetid: ecbf7e35-91c0-4ff4-82a4-53a935920915
keywords:
- Windows デバッグ rellist
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rellist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d632bc61ff186381cbc5e61f2c527014cc43c845
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338920"
---
# <a name="rellist"></a>!rellist


**! Rellist**拡張機能には、プラグ アンド プレイ関係一覧が表示されます。

```dbgcmd
!rellist Address [Flags] 
```

## <a name="span-idddkrellistdbgspanspan-idddkrellistdbgspanparameters"></a><span id="ddk__rellist_dbg"></span><span id="DDK__RELLIST_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
関係のリストのアドレスを指定します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示に含める追加の情報を指定します。 次のビット (既定値は 0) の任意の組み合わせこのことができます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
表示に含める、CM\_リソース\_一覧。 使用できる場合、表示にはからもブート リソースの一覧が含まれます。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
リソース要件の一覧に表示 (IO\_リソース\_リスト)。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
翻訳された CM を含める表示\_リソース\_一覧。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドのアプリケーション。 これらの構造の一覧については、Windows Driver Kit (WDK) ドキュメントを参照してください。

 

 





