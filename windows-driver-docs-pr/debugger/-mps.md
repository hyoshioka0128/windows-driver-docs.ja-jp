---
title: 管理パック
description: Mp の拡張機能には、ターゲット コンピューターの BIOS 情報 Intel マルチプロセッサ仕様 (MP) が表示されます。
ms.assetid: b6ee2eac-ef3c-403a-83ca-fe45506a8c4e
keywords:
- mp Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- mps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56ebf64bd0fbe009f043be7f9d7f0aeb5386330e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537859"
---
# <a name="mps"></a>! mp


**! Mp**拡張機能には、ターゲット コンピューターの BIOS 情報 Intel マルチプロセッサ仕様 (MP) が表示されます。

```dbgcmd
!mps [Address] 
```

## <a name="span-idddkmpsdbgspanspan-idddkmpsdbgspanparameters"></a><span id="ddk__mps_dbg"></span><span id="DDK__MPS_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
BIOS では、MP テーブルの 16 進数のアドレスを指定します。 これを省略した場合は、情報が、HAL から取得されます。 HAL シンボルが必要になります。

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

 

この拡張機能のコマンドは、x86 ベースの移行先のコンピューターでのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

BIOS のデバッグの詳細については、[BIOS コードのデバッグ](debugging-bios-code.md)を参照してください。 MP の詳細については、適切なバージョンの Intel マルチプロセッサ仕様を参照してください。

 

 





