---
title: asd
description: Asd の拡張機能には、指定したアドレスで始まるデータ キャッシュからのエラー分析のエントリの指定した数が表示されます。
ms.assetid: fb0eeedd-d50b-4385-b35f-4ac46fb97ce0
keywords:
- データ キャッシュから失敗の分析のエントリを表示します。
- Windows デバッグ asd
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- asd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 672a6cb35443fff4c4ec0c201bb38b0e1ae19313
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558364"
---
# <a name="asd"></a>! asd


**! Asd**拡張機能は、指定したアドレスで始まるデータ キャッシュからのエラー分析のエントリの指定した数を表示します。

```dbgcmd
    !asd Address DataUsed
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示する最初のエラー分析のエントリのアドレスを指定します。

<span id="_______DataUsed______"></span><span id="_______dataused______"></span><span id="_______DATAUSED______"></span> *DataUsed*   
表示するトークンの数を決定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

使用することができます、 [ **! dumpfa** ](-dumpfa.md)をデバッグする拡張機能、 [ **! 分析**](-analyze.md)拡張機能。

<a name="remarks"></a>注釈
-------

**! Asd**拡張機能のみのデバッグ中に便利ですが、 [ **! 分析**](-analyze.md)拡張機能。

 

 





