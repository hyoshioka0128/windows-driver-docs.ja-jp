---
title: gbl
description: Gbl 拡張機能では、ターゲットコンピューターの ACPI BIOS ルートシステムの説明 (RSDT) テーブルからヘッダー情報が表示されます。
ms.assetid: 1fc59112-27c4-465c-b460-8d6b0e83a39b
keywords:
- ACPI (高度な構成と電源インターフェイス)、RSDT ヘッダー情報
- グローバルロック
- gbl Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gbl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 75e3117be785d48ee8d474077649a9238bd60418
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025246"
---
# <a name="gbl"></a>!gbl


**! Gbl**拡張機能は、ターゲットコンピューターの ACPI BIOS ルートシステムの説明 (rsdt) テーブルからヘッダー情報を表示します。

```dbgcmd
!gbl [-v]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
な. テーブルに関する詳細情報を表示します。

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
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ACPI および ACPI テーブルの詳細については、「[その他の Acpi デバッグ拡張機能](other-acpi-debugging-extensions.md)」および「 [acpi 仕様](https://go.microsoft.com/fwlink/p/?linkid=57185)」 Web サイトを参照してください。 また、Microsoft Windows SDK のドキュメント、Windows Driver Kit (WDK) のドキュメント、および Mark Russinovich と David ソロモンによる*Microsoft windows の内部構造*も参照してください。

 

 





