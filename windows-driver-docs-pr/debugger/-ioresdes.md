---
title: ioresdes
description: Ioresdes 拡張機能では、指定したアドレスに IO_RESOURCE_DESCRIPTOR 構造が表示されます。
ms.assetid: a57dd414-16d6-4515-9eee-dac91398906b
keywords:
- Windows デバッグ ioresdes
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ioresdes
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fe4f2bff66961e0fe2c713c394e483e4efead11
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553059"
---
# <a name="ioresdes"></a>! ioresdes


**! Ioresdes**拡張機能の表示、IO\_リソース\_指定したアドレス記述子構造体。

```dbgcmd
!ioresdes Address 
```

## <a name="span-idddkioresdesdbgspanspan-idddkioresdesdbgspanparameters"></a><span id="ddk__ioresdes_dbg"></span><span id="DDK__IORESDES_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
IO の 16 進数のアドレスを指定します\_リソース\_記述子構造体。

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

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドのアプリケーション。 については、IO\_リソース\_記述子構造体を Windows Driver Kit (WDK) ドキュメントを参照してください。

 

 





