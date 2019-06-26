---
title: プリンター グラフィックス DLL によって定義されている関数
description: プリンター グラフィックス DLL によって定義されている関数
ms.assetid: b0c9ce45-76c4-4058-af3f-7b9d230bcf94
keywords:
- プリンター グラフィックス DLL WDK、関数
- WDK プリンター グラフィックス DLL の関数
- グラフィックスのプリンター DLL WDK 関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 868eb414a0b48802aa0bce31d7ede17fdec3087f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364017"
---
# <a name="functions-defined-by-printer-graphics-dlls"></a>プリンター グラフィックス DLL によって定義されている関数





すべてのグラフィック ドライバーのようなプリンター グラフィックス Dll は、次の図に DDI 関数を定義する責任を負います。 次の[ **DrvEnableDriver**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)、初期のドライバー エントリ ポイントで、残りの関数は、アルファベット順に一覧表示されます。 GDI を呼び出すため**DrvEnableDriver**名前では、その名前が太字で表示されます。 GDI の呼び出し関数ポインターの配列を使用してすべてのディスプレイ ドライバー機能**DrvEnableDriver**を返します。

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
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver" data-raw-source="[&lt;strong&gt;DrvEnableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)"><strong>DrvEnableDriver</strong></a></p></td>
<td><p>自体を初期化し、サポートされているグラフィック DDI 関数へのポインターを返すドライバーできます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev" data-raw-source="[&lt;strong&gt;DrvCompletePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)"><strong>DrvCompletePDEV</strong></a></p></td>
<td><p>デバイス インスタンスへの GDI ハンドルをドライバーを提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver" data-raw-source="[&lt;strong&gt;DrvDisableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)"><strong>DrvDisableDriver</strong></a></p></td>
<td><p>(省略可能)ドライバーがアンロードされる前にクリーンアップ操作を実行できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev" data-raw-source="[&lt;strong&gt;DrvDisablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)"><strong>DrvDisablePDEV</strong></a></p></td>
<td><p>デバイス インスタンスに固有の情報を削除するドライバーを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface" data-raw-source="[&lt;strong&gt;DrvDisableSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)"><strong>DrvDisableSurface</strong></a></p></td>
<td><p>描画サーフェイスを削除するドライバーを使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev" data-raw-source="[&lt;strong&gt;DrvEnablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)"><strong>DrvEnablePDEV</strong></a></p></td>
<td><p>物理デバイスの特性を持つ GDI を提供して、デバイス インスタンスに固有の情報を初期化するために、ドライバーを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)"><strong>DrvEnableSurface</strong></a></p></td>
<td><p>描画サーフェイスを作成するドライバーを使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydevicesupport" data-raw-source="[&lt;strong&gt;DrvQueryDeviceSupport&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydevicesupport)"><strong>DrvQueryDeviceSupport</strong></a></p></td>
<td><p>(省略可能)要求されたデバイスに固有の情報を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo)"><strong>DrvQueryDriverInfo</strong></a></p></td>
<td><p>(省略可能)要求されたドライバー固有の情報を返します。</p></td>
</tr>
</tbody>
</table>

 

プリンター グラフィックス Dll も次の印刷固有グラフィックス DDI 関数は、印刷ジョブの表示中に特定の時点で呼び出されるを定義する責任を負います。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>呼び出されたときに</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenddoc" data-raw-source="[&lt;strong&gt;DrvEndDoc&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenddoc)"><strong>DrvEndDoc</strong></a></p></td>
<td><p>GDI が完了すると、レンダリング用のドライバーにドキュメントを送信します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband" data-raw-source="[&lt;strong&gt;DrvNextBand&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)"><strong>DrvNextBand</strong></a></p></td>
<td><p>(省略可能)GDI は、物理ページのバンドの描画が完了したら、そのため、ドライバーはプリンターにバンドを送信できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo" data-raw-source="[&lt;em&gt;DrvQueryPerBandInfo&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo)"><em>DrvQueryPerBandInfo</em></a></p></td>
<td><p>(省略可能)GDI では、物理ページのバンドの描画を開始、前にそのため、ドライバーはバンドに固有の情報を GDI を指定できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsendpage" data-raw-source="[&lt;em&gt;DrvSendPage&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsendpage)"><em>DrvSendPage</em></a></p></td>
<td><p>GDI は、物理ページの描画が完了したら、そのため、ドライバーはプリンターにページを送信できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding" data-raw-source="[&lt;strong&gt;DrvStartBanding&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding)"><strong>DrvStartBanding</strong></a></p></td>
<td><p>(省略可能)GDI が物理ページのバンドをレンダリング用のドライバーに送信を開始する準備ができて場合です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartdoc" data-raw-source="[&lt;strong&gt;DrvStartDoc&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartdoc)"><strong>DrvStartDoc</strong></a></p></td>
<td><p>GDI がドキュメントをレンダリング用のドライバーに送信を開始する準備ができて場合です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartpage" data-raw-source="[&lt;strong&gt;DrvStartPage&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartpage)"><strong>DrvStartPage</strong></a></p></td>
<td><p>GDI がドキュメントのページをレンダリング用のドライバーに送信を開始する準備ができて場合です。</p></td>
</tr>
</tbody>
</table>

 

通常は、プリンター グラフィックス DLL も定義どのような追加のグラフィックス DDI 関数では、印刷ジョブの表示を実現するために必要です。 定義された関数の種類と数に依存します。

-   かどうか、ドライバーは、GDI が管理またはデバイス管理の描画サーフェス (または両方) の使用をサポートします。 詳細については、次を参照してください。[画面型](https://docs.microsoft.com/windows-hardware/drivers/display/surface-types)します。

-   描画操作で処理できる GDI ドライバー自体によって実行されているのではなく拡張です。 詳細については、次を参照してください。[グラフィックス DDI を使用して](https://docs.microsoft.com/windows-hardware/drivers/display/using-the-graphics-ddi)します。

プリンター グラフィックスによって定義されているすべての関数の Dll は、GDI のカーネル モードのグラフィックス レンダリング エンジン (GRE) によって呼び出されます。

[ **DrvEnableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)と[ **DrvQueryDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo)関数は、グラフィックス DLL によってエクスポートされます。 サポートされている他のすべてのグラフィックス DDI 関数のアドレスは、によって返されるテーブルに、 **DrvEnableDriver**関数。

 

 




