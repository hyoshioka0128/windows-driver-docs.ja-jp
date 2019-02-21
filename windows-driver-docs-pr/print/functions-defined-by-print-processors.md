---
title: プリント プロセッサによって定義されている関数
description: プリント プロセッサによって定義されている関数
ms.assetid: ada376f0-515e-4995-b612-4da9523b6fcf
keywords:
- プリント プロセッサ WDK、関数
- WDK の関数を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17c27218af95da7714b9e9d99ce18ab0a97d3f13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536588"
---
# <a name="functions-defined-by-print-processors"></a>プリント プロセッサによって定義されている関数





プリント プロセッサは、次の表に示す関数をエクスポートする必要があります。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545976" data-raw-source="[&lt;strong&gt;ClosePrintProcessor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545976)"><strong>ClosePrintProcessor</strong></a></p></td>
<td><p>プリント プロセッサを閉じます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546352" data-raw-source="[&lt;strong&gt;ControlPrintProcessor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546352)"><strong>ControlPrintProcessor</strong></a></p></td>
<td><p>ドキュメントの印刷に制御を提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548757" data-raw-source="[&lt;strong&gt;EnumPrintProcessorDatatypes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548757)"><strong>EnumPrintProcessorDatatypes</strong></a></p></td>
<td><p>プリント プロセッサによってサポートされるデータ型を列挙します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550522" data-raw-source="[&lt;strong&gt;GetPrintProcessorCapabilities&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550522)"><strong>GetPrintProcessorCapabilities</strong></a></p></td>
<td><p>返します。 指定した入力データの種類のプロセッサの処理能力を印刷します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559604" data-raw-source="[&lt;strong&gt;OpenPrintProcessor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559604)"><strong>OpenPrintProcessor</strong></a></p></td>
<td><p>印刷のプリント プロセッサを開きます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560724" data-raw-source="[&lt;strong&gt;PrintDocumentOnPrintProcessor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560724)"><strong>PrintDocumentOnPrintProcessor</strong></a></p></td>
<td><p>プリント プロセッサには、ドキュメントを印刷します。</p></td>
</tr>
</tbody>
</table>

 

 

 




