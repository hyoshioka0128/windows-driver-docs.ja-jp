---
title: プリンター インターフェイス DLL によって定義されている関数
description: プリンター インターフェイス DLL によって定義されている関数
ms.assetid: 8b0ae796-67cf-4619-a0a7-6cb6aab8c2e4
keywords:
- プリンター インターフェイス DLL の WDK、関数
- WDK プリンター インターフェイス DLL の関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d0cf1e1d8df03086ea6c605b09d5344f9455b66
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363998"
---
# <a name="functions-defined-by-printer-interface-dlls"></a>プリンター インターフェイス DLL によって定義されている関数





プリンターのインターフェイスの Dll は、次の表に示す関数をエクスポートします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DllEntryPoint</strong></p></td>
<td><p>初期 DLL エントリ ポイント、通常 DLLMain (Microsoft Windows SDK のドキュメントで説明) と呼ばれます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvconvertdevmode" data-raw-source="[&lt;strong&gt;DrvConvertDevMode&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvconvertdevmode)"><strong>DrvConvertDevMode</strong></a></p></td>
<td><p>指定した変換<a href="https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)"> <strong>DEVMODEW</strong> </a> 1 つのバージョンから別の構造体。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities" data-raw-source="[&lt;strong&gt;DrvDeviceCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)"><strong>DrvDeviceCapabilities</strong></a></p></td>
<td><p>要求されたプリンターの機能に関する情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicepropertysheets" data-raw-source="[&lt;strong&gt;DrvDevicePropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicepropertysheets)"><strong>DrvDevicePropertySheets</strong></a></p></td>
<td><p>呼び出し<a href="common-property-sheet-user-interface.md" data-raw-source="[CPSUI](common-property-sheet-user-interface.md)">CPSUI</a>プリンターのプロパティを説明するプロパティ シートのページを作成します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentevent" data-raw-source="[&lt;strong&gt;DrvDocumentEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentevent)"><strong>DrvDocumentEvent</strong></a></p></td>
<td><p>(省略可能)プリンターのインターフェイスに関連付けられたドキュメントを印刷するイベントが処理されることを指定する DLL を使用できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdriverevent" data-raw-source="[&lt;strong&gt;DrvDriverEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdriverevent)"><strong>DrvDriverEvent</strong></a></p></td>
<td><p>(省略可能)プリンターのインターフェイス特定のドライバー固有のイベントが発生した、スプーラーからの通知に応答する DLL を使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets" data-raw-source="[&lt;strong&gt;DrvDocumentPropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)"><strong>DrvDocumentPropertySheets</strong></a></p></td>
<td><p>印刷ドキュメントのプロパティを説明するプロパティ シートのページを作成する CPSUI を呼び出します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvprinterevent" data-raw-source="[&lt;strong&gt;DrvPrinterEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvprinterevent)"><strong>DrvPrinterEvent</strong></a></p></td>
<td><p>プリンターのインターフェイス特定のプリンター固有のイベントが発生した、スプーラーからの通知に応答する DLL を使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvquerycolorprofile" data-raw-source="[&lt;strong&gt;DrvQueryColorProfile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvquerycolorprofile)"><strong>DrvQueryColorProfile</strong></a></p></td>
<td><p>(省略可能)プリンター インターフェイス ICC の色の管理に使用するプロファイルを指定する DLL を使用できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvqueryjobattributes" data-raw-source="[&lt;strong&gt;DrvQueryJobAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvqueryjobattributes)"><strong>DrvQueryJobAttributes</strong></a></p></td>
<td><p>(省略可能)プリンター インターフェイス物理ページ ("n-up"印刷) に複数のドキュメント ページを印刷すると、このような機能のサポートを指定する DLL はの各ページで、複数のコピーを印刷、およびページを照合します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-devqueryprintex" data-raw-source="[&lt;strong&gt;DevQueryPrintEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-devqueryprintex)"><strong>DevQueryPrintEx</strong></a></p></td>
<td><p>プリンターの現在の構成を使用して、印刷ジョブを印刷できるかどうかを決定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvspldevicecaps" data-raw-source="[&lt;strong&gt;DrvSplDeviceCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvspldevicecaps)"><strong>DrvSplDeviceCaps</strong></a></p></td>
<td><p>要求されたプリンターの機能に関する情報を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvupgradeprinter" data-raw-source="[&lt;strong&gt;DrvUpgradePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvupgradeprinter)"><strong>DrvUpgradePrinter</strong></a></p></td>
<td><p>(省略可能)新しいバージョンのドライバーがシステムに追加されたときに、プリンターのレジストリ設定を更新します。</p></td>
</tr>
</tbody>
</table>

 

 

 




