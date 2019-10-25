---
title: プリンター インターフェイス DLL によって定義されている関数
description: プリンター インターフェイス DLL によって定義されている関数
ms.assetid: 8b0ae796-67cf-4619-a0a7-6cb6aab8c2e4
keywords:
- printer interface DLL WDK、functions
- functions WDK printer interface DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96617e358c0e116efb6287cba51e12c6dea848ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845297"
---
# <a name="functions-defined-by-printer-interface-dlls"></a>プリンター インターフェイス DLL によって定義されている関数





プリンタインターフェイス Dll は、次の表に示す関数をエクスポートします。

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
<td><p>初期 DLL エントリポイント。通常は DLLMain と呼ばれます (Microsoft Windows SDK のドキュメントを参照)。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvconvertdevmode" data-raw-source="[&lt;strong&gt;DrvConvertDevMode&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvconvertdevmode)"><strong>DrvConvertDevMode</strong></a></p></td>
<td><p>指定した<a href="https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)"><strong>Devmodew</strong></a>構造体をあるバージョンから別のバージョンに変換します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities" data-raw-source="[&lt;strong&gt;DrvDeviceCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)"><strong>DrvDeviceCapabilities</strong></a></p></td>
<td><p>プリンターの機能に関する要求された情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets" data-raw-source="[&lt;strong&gt;DrvDevicePropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets)"><strong>DrvDevicePropertySheets</strong></a></p></td>
<td><p><a href="common-property-sheet-user-interface.md" data-raw-source="[CPSUI](common-property-sheet-user-interface.md)">CPSUI</a>を呼び出して、プリンターのプロパティを説明するプロパティシートページを作成します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent" data-raw-source="[&lt;strong&gt;DrvDocumentEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent)"><strong>DrvDocumentEvent</strong></a></p></td>
<td><p>Optionalプリンターインターフェイス DLL が、処理するドキュメントの印刷に関連付けられているイベントを指定できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdriverevent" data-raw-source="[&lt;strong&gt;DrvDriverEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdriverevent)"><strong>DrvDriverEvent</strong></a></p></td>
<td><p>Optional特定のドライバー固有のイベントが発生したスプーラからの通知にプリンターインターフェイス DLL が応答できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets" data-raw-source="[&lt;strong&gt;DrvDocumentPropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)"><strong>DrvDocumentPropertySheets</strong></a></p></td>
<td><p>CPSUI を呼び出して、印刷ドキュメントのプロパティを説明するプロパティシートページを作成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent" data-raw-source="[&lt;strong&gt;DrvPrinterEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)"><strong>DrvPrinterEvent</strong></a></p></td>
<td><p>プリンターインターフェイス DLL が、特定のプリンター固有のイベントが発生したスプーラからの通知に応答できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvquerycolorprofile" data-raw-source="[&lt;strong&gt;DrvQueryColorProfile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvquerycolorprofile)"><strong>DrvQueryColorProfile</strong></a></p></td>
<td><p>Optionalプリンターインターフェイス DLL が、カラーの管理に使用する ICC プロファイルを指定できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes" data-raw-source="[&lt;strong&gt;DrvQueryJobAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes)"><strong>DrvQueryJobAttributes</strong></a></p></td>
<td><p>Optionalプリンターインターフェイス DLL が、物理的なページでの複数のドキュメントページの印刷 ("N-up" 印刷)、各ページの複数コピーの印刷、および照合ページなどの機能のサポートを指定できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-devqueryprintex" data-raw-source="[&lt;strong&gt;DevQueryPrintEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-devqueryprintex)"><strong>DevQueryPrintEx</strong></a></p></td>
<td><p>プリンターの現在の構成を使用して印刷ジョブを印刷できるかどうかを決定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvspldevicecaps" data-raw-source="[&lt;strong&gt;DrvSplDeviceCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvspldevicecaps)"><strong>DrvSplDeviceCaps</strong></a></p></td>
<td><p>プリンターの機能に関する要求された情報を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvupgradeprinter" data-raw-source="[&lt;strong&gt;DrvUpgradePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvupgradeprinter)"><strong>DrvUpgradePrinter</strong></a></p></td>
<td><p>Optional新しいバージョンのドライバーがシステムに追加されたときに、プリンターのレジストリ設定を更新します。</p></td>
</tr>
</tbody>
</table>

 

 

 




