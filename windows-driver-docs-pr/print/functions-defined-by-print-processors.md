---
title: 印刷プロセッサによって定義されている関数
description: 印刷プロセッサによって定義されている関数
ms.assetid: ada376f0-515e-4995-b612-4da9523b6fcf
keywords:
- プリントプロセッサ WDK、functions
- functions WDK print
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 682fb80a93afb9001f65af5c5dd80544fedf5e42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842404"
---
# <a name="functions-defined-by-print-processors"></a>印刷プロセッサによって定義されている関数





プリントプロセッサは、次の表に示す関数をエクスポートする必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeprintprocessor" data-raw-source="[&lt;strong&gt;ClosePrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeprintprocessor)"><strong>ClosePrintProcessor</strong></a></p></td>
<td><p>印刷プロセッサを閉じます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-controlprintprocessor" data-raw-source="[&lt;strong&gt;ControlPrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-controlprintprocessor)"><strong>ControlPrintProcessor</strong></a></p></td>
<td><p>ドキュメントの印刷を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/nf-winspool-enumprintprocessordatatypesa" data-raw-source="[&lt;strong&gt;EnumPrintProcessorDatatypes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/nf-winspool-enumprintprocessordatatypesa)"><strong>EnumPrintProcessorDatatypes 型</strong></a></p></td>
<td><p>プリントプロセッサによってサポートされるデータ型を列挙します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-getprintprocessorcapabilities" data-raw-source="[&lt;strong&gt;GetPrintProcessorCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-getprintprocessorcapabilities)"><strong>GetPrintProcessorCapabilities</strong></a></p></td>
<td><p>指定された入力データ型の印刷プロセッサ機能を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openprintprocessor" data-raw-source="[&lt;strong&gt;OpenPrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openprintprocessor)"><strong>OpenPrintProcessor</strong></a></p></td>
<td><p>印刷用の印刷プロセッサを開きます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor" data-raw-source="[&lt;strong&gt;PrintDocumentOnPrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor)"><strong>PrintDocumentOnPrintProcessor</strong></a></p></td>
<td><p>印刷プロセッサにドキュメントを出力します。</p></td>
</tr>
</tbody>
</table>

 

 

 




