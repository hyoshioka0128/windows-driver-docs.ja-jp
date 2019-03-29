---
title: プリンター インターフェイス DLL によって定義されている関数
description: プリンター インターフェイス DLL によって定義されている関数
ms.assetid: 8b0ae796-67cf-4619-a0a7-6cb6aab8c2e4
keywords:
- プリンター インターフェイス DLL の WDK、関数
- WDK プリンター インターフェイス DLL の関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9daf71e6c2529c1eecc6a3b0fc6c7b193155ab98
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464300"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548532" data-raw-source="[&lt;strong&gt;DrvConvertDevMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548532)"><strong>DrvConvertDevMode</strong></a></p></td>
<td><p>指定した変換<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a> 1 つのバージョンから別の構造体。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548539" data-raw-source="[&lt;strong&gt;DrvDeviceCapabilities&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548539)"><strong>DrvDeviceCapabilities</strong></a></p></td>
<td><p>要求されたプリンターの機能に関する情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548542" data-raw-source="[&lt;strong&gt;DrvDevicePropertySheets&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548542)"><strong>DrvDevicePropertySheets</strong></a></p></td>
<td><p>呼び出し<a href="common-property-sheet-user-interface.md" data-raw-source="[CPSUI](common-property-sheet-user-interface.md)">CPSUI</a>プリンターのプロパティを説明するプロパティ シートのページを作成します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548544" data-raw-source="[&lt;strong&gt;DrvDocumentEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548544)"><strong>DrvDocumentEvent</strong></a></p></td>
<td><p>(省略可能)プリンターのインターフェイスに関連付けられたドキュメントを印刷するイベントが処理されることを指定する DLL を使用できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548551" data-raw-source="[&lt;strong&gt;DrvDriverEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548551)"><strong>DrvDriverEvent</strong></a></p></td>
<td><p>(省略可能)プリンターのインターフェイス特定のドライバー固有のイベントが発生した、スプーラーからの通知に応答する DLL を使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548548" data-raw-source="[&lt;strong&gt;DrvDocumentPropertySheets&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548548)"><strong>DrvDocumentPropertySheets</strong></a></p></td>
<td><p>印刷ドキュメントのプロパティを説明するプロパティ シートのページを作成する CPSUI を呼び出します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548564" data-raw-source="[&lt;strong&gt;DrvPrinterEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548564)"><strong>DrvPrinterEvent</strong></a></p></td>
<td><p>プリンターのインターフェイス特定のプリンター固有のイベントが発生した、スプーラーからの通知に応答する DLL を使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548573" data-raw-source="[&lt;strong&gt;DrvQueryColorProfile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548573)"><strong>DrvQueryColorProfile</strong></a></p></td>
<td><p>(省略可能)プリンター インターフェイス ICC の色の管理に使用するプロファイルを指定する DLL を使用できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548581" data-raw-source="[&lt;strong&gt;DrvQueryJobAttributes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548581)"><strong>DrvQueryJobAttributes</strong></a></p></td>
<td><p>(省略可能)プリンター インターフェイス物理ページ ("n-up"印刷) に複数のドキュメント ページを印刷すると、このような機能のサポートを指定する DLL はの各ページで、複数のコピーを印刷、およびページを照合します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547576" data-raw-source="[&lt;strong&gt;DevQueryPrintEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547576)"><strong>DevQueryPrintEx</strong></a></p></td>
<td><p>プリンターの現在の構成を使用して、印刷ジョブを印刷できるかどうかを決定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548600" data-raw-source="[&lt;strong&gt;DrvSplDeviceCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548600)"><strong>DrvSplDeviceCaps</strong></a></p></td>
<td><p>要求されたプリンターの機能に関する情報を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548648" data-raw-source="[&lt;strong&gt;DrvUpgradePrinter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548648)"><strong>DrvUpgradePrinter</strong></a></p></td>
<td><p>(省略可能)新しいバージョンのドライバーがシステムに追加されたときに、プリンターのレジストリ設定を更新します。</p></td>
</tr>
</tbody>
</table>

 

 

 




