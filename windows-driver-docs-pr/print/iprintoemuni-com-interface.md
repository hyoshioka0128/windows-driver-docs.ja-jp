---
title: IPrintOemUni COM インターフェイス
description: IPrintOemUni COM インターフェイス
ms.assetid: b120def0-f270-49c6-b12f-10c220801f51
keywords:
- IPrintOemUni
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3f4cff5ef4ce487f4fe3ce40d4d9e78cad25d05
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841767"
---
# <a name="iprintoemuni-com-interface"></a>IPrintOemUni COM インターフェイス





`IPrintOemUni` COM インターフェイスは、Unidrv 用の[プリンターグラフィックス DLL](printer-graphics-dll.md)がレンダリングプラグインと通信する手段です。 `IPrintOemUni` インターフェイスは、各レンダリングプラグインによって実装されます。

次の表に、`IPrintOemUni` インターフェイスによって提供されるすべてのメソッドとその説明を示します。 レンダリングプラグインでは、表示されているすべてのメソッドを定義する必要があります。 メソッドが不要な場合は、単に E\_NOTIMPL を返すことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback" data-raw-source="[&lt;strong&gt;IPrintOemUni::CommandCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback)"><strong>IPrintOemUni:: CommandCallback</strong></a></p></td>
<td><p>レンダリングプラグインが動的に生成されたプリンターコマンドを提供できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-compression" data-raw-source="[&lt;strong&gt;IPrintOemUni::Compression&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-compression)"><strong>IPrintOemUni:: Compression</strong></a></p></td>
<td><p>レンダリングプラグインがカスタマイズされたビットマップ圧縮方法を提供できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-devmode" data-raw-source="[&lt;strong&gt;IPrintOemUni::DevMode&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-devmode)"><strong>IPrintOemUni::D evMode</strong></a></p></td>
<td><p>レンダリングプラグインのプライベート DEVMODE メンバーに対して操作を実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-disabledriver" data-raw-source="[&lt;strong&gt;IPrintOemUni::DisableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-disabledriver)"><strong>IPrintOemUni::D isableDriver</strong></a></p></td>
<td><p>レンダリングプラグインの<strong>Iprintoemuni:: EnableDriver</strong>メソッドによって割り当てられたリソースを解放します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-disablepdev" data-raw-source="[&lt;strong&gt;IPrintOemUni::DisablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-disablepdev)"><strong>IPrintOemUni::D isablePDEV</strong></a></p></td>
<td><p>レンダリングプラグインが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)"><strong>Iprintoemuni:: EnablePDEV</strong></a>メソッドによって割り当てられたプライベート pdev 構造を削除できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadcharglyph" data-raw-source="[&lt;strong&gt;IPrintOemUni::DownloadCharGlyph&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadcharglyph)"><strong>IPrintOemUni::D ownloadCharGlyph</strong></a></p></td>
<td><p>レンダリングプラグインが、指定されたソフトフォントの文字グリフをプリンターにダウンロードできるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadfontheader" data-raw-source="[&lt;strong&gt;IPrintOemUni::DownloadFontHeader&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadfontheader)"><strong>IPrintOemUni::D ownloadFontHeader</strong></a></p></td>
<td><p>レンダリングプラグインがプリンターにフォントのヘッダー情報をダウンロードできるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-driverdms" data-raw-source="[&lt;strong&gt;IPrintOemUni::DriverDMS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-driverdms)"><strong>IPrintOemUni::D riverDMS</strong></a></p></td>
<td><p>レンダリングプラグインで、デバイスによって管理される描画サーフェイスを使用することを示すことができます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enabledriver" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)"><strong>IPrintOemUni:: EnableDriver</strong></a></p></td>
<td><p>レンダリングプラグインがいくつかのグラフィックス DDI 関数をフックできるようにします。 このメソッドと<strong>Iprintoemuni::D isableDriver</strong>はペアと見なす必要があることに注意してください。実装されている場合は、もう一方も実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)"><strong>IPrintOemUni:: EnablePDEV</strong></a></p></td>
<td><p>レンダリングプラグインで独自の PDEV 構造体を作成できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics" data-raw-source="[&lt;strong&gt;IPrintOemUni::FilterGraphics&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)"><strong>IPrintOemUni:: FilterGraphics</strong></a></p></td>
<td><p>レンダリングプラグインがスキャンラインデータを変更してスプーラに送信できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getimplementedmethod" data-raw-source="[&lt;strong&gt;IPrintOemUni::GetImplementedMethod&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getimplementedmethod)"><strong>IPrintOemUni:: GetImplementedMethod</strong></a></p></td>
<td><p>(実装が必要です)。レンダリングプラグインによって実装された <code>IPrintOemUni</code> インターフェイスメソッドを判別できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getinfo" data-raw-source="[&lt;strong&gt;IPrintOemUni::GetInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getinfo)"><strong>IPrintOemUni:: GetInfo</strong></a></p></td>
<td><p>(実装が必要です)。レンダリングプラグインの識別情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern" data-raw-source="[&lt;strong&gt;IPrintOemUni::HalftonePattern&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)"><strong>IPrintOemUni:: HalftonePattern</strong></a></p></td>
<td><p>ハーフトーン操作で使用する前に、レンダリングプラグインがハーフトーンパターンを作成または変更できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)"><strong>IPrintOemUni:: ImageProcessing</strong></a></p></td>
<td><p>色の書式設定またはハーフトーンを実行するために、レンダリングプラグインがイメージビットマップデータを変更できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-memoryusage" data-raw-source="[&lt;strong&gt;IPrintOemUni::MemoryUsage&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-memoryusage)"><strong>IPrintOemUni:: MemoryUsage</strong></a></p></td>
<td><p>レンダリングプラグインが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)"><strong>Iprintoemuni:: ImageProcessing</strong></a>メソッドで使用するために必要なメモリの量を指定できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-outputcharstr" data-raw-source="[&lt;strong&gt;IPrintOemUni::OutputCharStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-outputcharstr)"><strong>IPrintOemUni:: OutputCharStr</strong></a></p></td>
<td><p>レンダリングプラグインでフォントグリフの印刷を制御できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-publishdriverinterface" data-raw-source="[&lt;strong&gt;IPrintOemUni::PublishDriverInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-publishdriverinterface)"><strong>IPrintOemUni::P ublishDriverInterface</strong></a></p></td>
<td><p>(実装が必要です)。Unidrv ドライバーの<a href="iprintoemdriveruni-com-interface.md" data-raw-source="[IPrintOemDriverUni COM interface](iprintoemdriveruni-com-interface.md)">Iprintoemdriveruni COM インターフェイス</a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni" data-raw-source="[IPrintCoreHelperUni interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)">iprintcoreの peruni インターフェイス</a>へのポインターを提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-resetpdev" data-raw-source="[&lt;strong&gt;IPrintOemUni::ResetPDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-resetpdev)"><strong>IPrintOemUni:: ResetPDEV</strong></a></p></td>
<td><p>レンダリングプラグインが PDEV 構造をリセットできるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-sendfontcmd" data-raw-source="[&lt;strong&gt;IPrintOemUni::SendFontCmd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-sendfontcmd)"><strong>IPrintOemUni:: SendFontCmd</strong></a></p></td>
<td><p>レンダリングプラグインがプリンターのフォント選択コマンドを変更し、プリンターに送信できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap" data-raw-source="[&lt;strong&gt;IPrintOemUni::TextOutAsBitmap&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap)"><strong>IPrintOemUni:: TextOutAsBitmap</strong></a></p></td>
<td><p>レンダリングプラグインを使用して、テキスト文字列のビットマップイメージを作成できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-ttdownloadmethod" data-raw-source="[&lt;strong&gt;IPrintOemUni::TTDownloadMethod&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-ttdownloadmethod)"><strong>IPrintOemUni:: TTDownloadMethod</strong></a></p></td>
<td><p>指定された TrueType フォントに対して Unidrv が使用する形式を表示プラグインで示すことができるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-ttygetinfo" data-raw-source="[&lt;strong&gt;IPrintOemUni::TTYGetInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-ttygetinfo)"><strong>IPrintOemUni:: TTYGetInfo</strong></a></p></td>
<td><p>レンダリングプラグインが、テキストのみのプリンターに関連する情報で Unidrv を提供できるようにします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 




