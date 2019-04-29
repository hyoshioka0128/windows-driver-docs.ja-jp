---
title: IPrintOemUni COM インターフェイス
description: IPrintOemUni COM インターフェイス
ms.assetid: b120def0-f270-49c6-b12f-10c220801f51
keywords:
- IPrintOemUni
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c0ee8a3113ca2e0360a61fe091c08f532f16932
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384213"
---
# <a name="iprintoemuni-com-interface"></a>IPrintOemUni COM インターフェイス





`IPrintOemUni`の COM インターフェイスは、の方法で、[プリンター グラフィックス DLL](printer-graphics-dll.md) Unidrv がプラグインのレンダリングと通信するのです。 `IPrintOemUni`インターフェイスは、各レンダリング プラグインによって実装されます。

次の表とによって提供されるメソッドのすべてについて説明します、`IPrintOemUni`インターフェイス。 プラグインをレンダリングと、一覧内のすべてのメソッドを定義する必要があります。 かどうか、メソッドは必要ありません、単に返すことができます E\_NOTIMPL します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554216" data-raw-source="[&lt;strong&gt;IPrintOemUni::CommandCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554216)"><strong>IPrintOemUni::CommandCallback</strong></a></p></td>
<td><p>生成されるプリンターのコマンドを動的に提供するプラグインを表示できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554224" data-raw-source="[&lt;strong&gt;IPrintOemUni::Compression&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554224)"><strong>IPrintOemUni::Compression</strong></a></p></td>
<td><p>レンダリングをカスタマイズしたビットマップの圧縮方法を提供するプラグインに使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554230" data-raw-source="[&lt;strong&gt;IPrintOemUni::DevMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554230)"><strong>IPrintOemUni::DevMode</strong></a></p></td>
<td><p>プライベートなレンダリング プラグインの DEVMODE メンバーに対して操作を実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554232" data-raw-source="[&lt;strong&gt;IPrintOemUni::DisableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554232)"><strong>IPrintOemUni::DisableDriver</strong></a></p></td>
<td><p>レンダリング プラグインでは、によって割り当てられたリソースを解放<strong>IPrintOemUni::EnableDriver</strong>メソッド。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554238" data-raw-source="[&lt;strong&gt;IPrintOemUni::DisablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554238)"><strong>IPrintOemUni::DisablePDEV</strong></a></p></td>
<td><p>レンダリングで割り当てられたプライベート PDEV 構造を削除するプラグインは、その<a href="https://msdn.microsoft.com/library/windows/hardware/ff554249" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554249)"> <strong>IPrintOemUni::EnablePDEV</strong> </a>メソッド。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554241" data-raw-source="[&lt;strong&gt;IPrintOemUni::DownloadCharGlyph&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554241)"><strong>IPrintOemUni::DownloadCharGlyph</strong></a></p></td>
<td><p>レンダリングは、プラグインの指定した論理的なフォントの文字のグリフをプリンターにダウンロードできます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554242" data-raw-source="[&lt;strong&gt;IPrintOemUni::DownloadFontHeader&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554242)"><strong>IPrintOemUni::DownloadFontHeader</strong></a></p></td>
<td><p>レンダリングをプリンターにフォントのヘッダー情報をダウンロードするプラグインに使用できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554245" data-raw-source="[&lt;strong&gt;IPrintOemUni::DriverDMS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554245)"><strong>IPrintOemUni::DriverDMS</strong></a></p></td>
<td><p>レンダリングをプラグインをデバイス管理の描画サーフェイスを使用することを示すために使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554248" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554248)"><strong>IPrintOemUni::EnableDriver</strong></a></p></td>
<td><p>レンダリングは、一部のグラフィックス DDI 関数をフックするプラグインできます。 注意このメソッドと<strong>IPrintOemUni::DisableDriver</strong>見なす必要がありますのペアとして 1 つが実装されている場合、もう一方も実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554249" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554249)"><strong>IPrintOemUni::EnablePDEV</strong></a></p></td>
<td><p>レンダリングを独自の PDEV 構造を作成するプラグインに使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554252" data-raw-source="[&lt;strong&gt;IPrintOemUni::FilterGraphics&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554252)"><strong>IPrintOemUni::FilterGraphics</strong></a></p></td>
<td><p>レンダリングは、プラグインのスキャン ラインのデータを変更して、スプーラーに送信できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554253" data-raw-source="[&lt;strong&gt;IPrintOemUni::GetImplementedMethod&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554253)"><strong>IPrintOemUni::GetImplementedMethod</strong></a></p></td>
<td><p>(必要な実装です。)により判断するために Unidrv<code>IPrintOemUni</code>プラグインを表示してインターフェイス メソッドが実装されました。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554256" data-raw-source="[&lt;strong&gt;IPrintOemUni::GetInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554256)"><strong>IPrintOemUni::GetInfo</strong></a></p></td>
<td><p>(必要な実装です。)レンダリング プラグインの識別情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554258" data-raw-source="[&lt;strong&gt;IPrintOemUni::HalftonePattern&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554258)"><strong>IPrintOemUni::HalftonePattern</strong></a></p></td>
<td><p>レンダリングは、プラグインを作成またはハーフトーン操作で使用される前に、ハーフトーン パターンを変更できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554261" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554261)"><strong>IPrintOemUni::ImageProcessing</strong></a></p></td>
<td><p>レンダリングは、プラグインの色の書式設定、またはハーフトーンを実行するために、ビットマップ データをイメージを変更できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554264" data-raw-source="[&lt;strong&gt;IPrintOemUni::MemoryUsage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554264)"><strong>IPrintOemUni::MemoryUsage</strong></a></p></td>
<td><p>レンダリングで使用するために必要なメモリの量を指定するプラグインは、その<a href="https://msdn.microsoft.com/library/windows/hardware/ff554261" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554261)"> <strong>IPrintOemUni::ImageProcessing</strong> </a>メソッド。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554267" data-raw-source="[&lt;strong&gt;IPrintOemUni::OutputCharStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554267)"><strong>IPrintOemUni::OutputCharStr</strong></a></p></td>
<td><p>レンダリングは、プラグインのグリフのフォントの印刷を制御できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554269" data-raw-source="[&lt;strong&gt;IPrintOemUni::PublishDriverInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554269)"><strong>IPrintOemUni::PublishDriverInterface</strong></a></p></td>
<td><p>(必要な実装です。)Unidrv ドライバーへのポインターを提供<a href="iprintoemdriveruni-com-interface.md" data-raw-source="[IPrintOemDriverUni COM interface](iprintoemdriveruni-com-interface.md)">IPrintOemDriverUni COM インターフェイス</a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff552940" data-raw-source="[IPrintCoreHelperUni interface](https://msdn.microsoft.com/library/windows/hardware/ff552940)">IPrintCoreHelperUni インターフェイス</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554270" data-raw-source="[&lt;strong&gt;IPrintOemUni::ResetPDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554270)"><strong>IPrintOemUni::ResetPDEV</strong></a></p></td>
<td><p>レンダリングは、その PDEV 構造をリセットするプラグインできます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554274" data-raw-source="[&lt;strong&gt;IPrintOemUni::SendFontCmd&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554274)"><strong>IPrintOemUni::SendFontCmd</strong></a></p></td>
<td><p>レンダリングは、プラグインのプリンターのフォントの選択 コマンドを変更し、プリンターに送信できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554277" data-raw-source="[&lt;strong&gt;IPrintOemUni::TextOutAsBitmap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554277)"><strong>IPrintOemUni::TextOutAsBitmap</strong></a></p></td>
<td><p>レンダリングは、プラグインのテキスト文字列のビットマップ イメージを作成できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554279" data-raw-source="[&lt;strong&gt;IPrintOemUni::TTDownloadMethod&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554279)"><strong>IPrintOemUni::TTDownloadMethod</strong></a></p></td>
<td><p>レンダリングを Unidrv が、指定する TrueType フォントを使用する形式を指定するプラグインに使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554283" data-raw-source="[&lt;strong&gt;IPrintOemUni::TTYGetInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554283)"><strong>IPrintOemUni::TTYGetInfo</strong></a></p></td>
<td><p>レンダリングは、テキストのみのプリンターに関連する情報 Unidrv を指定するプラグインできます。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 




