---
title: IPrintOemPS COM インターフェイス
description: IPrintOemPS COM インターフェイス
ms.assetid: 504db6ab-291e-4fba-995d-49a22a3a7c7f
keywords:
- IPrintOemPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936ccd8ddb014f8a8ad0f25c89b3bfc341da7c04
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349576"
---
# <a name="iprintoemps-com-interface"></a>IPrintOemPS COM インターフェイス





`IPrintOemPS`の COM インターフェイスは、の方法で、[プリンター グラフィックス DLL](printer-graphics-dll.md) Pscript5 がプラグインのレンダリングと通信するのです。 `IPrintOemPS`インターフェイスは、各レンダリング プラグインによって実装されます。

次の表とによって提供されるメソッドのすべてについて説明します、`IPrintOemPS`インターフェイス。 プラグインを表示、表示されているすべてのメソッドを定義する必要があります。 かどうか、メソッドは必要ありません、単に返すことができます E\_NOTIMPL します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553199" data-raw-source="[&lt;strong&gt;IPrintOemPS::Command&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553199)"><strong>IPrintOemPS::Command</strong></a></p></td>
<td><p>印刷ジョブのデータ ストリームに Postscript コマンドを挿入するプラグインを表示を許可します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553205" data-raw-source="[&lt;strong&gt;IPrintOemPS::DevMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553205)"><strong>IPrintOemPS::DevMode</strong></a></p></td>
<td><p>レンダリング プラグインのプライベートに対して操作を実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>メンバー。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553207" data-raw-source="[&lt;strong&gt;IPrintOemPS::DisableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553207)"><strong>IPrintOemPS::DisableDriver</strong></a></p></td>
<td><p>レンダリング プラグインでは、によって割り当てられたリソースを解放<a href="https://msdn.microsoft.com/library/windows/hardware/ff553212" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553212)"> <strong>IPrintOemPS::EnableDriver</strong> </a>メソッド。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553209" data-raw-source="[&lt;strong&gt;IPrintOemPS::DisablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553209)"><strong>IPrintOemPS::DisablePDEV</strong></a></p></td>
<td><p>レンダリングで割り当てられたプライベート PDEV 構造を削除するプラグインは、その<a href="https://msdn.microsoft.com/library/windows/hardware/ff553215" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553215)"> <strong>IPrintOemPS::EnablePDEV</strong> </a>メソッド。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553212" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553212)"><strong>IPrintOemPS::EnableDriver</strong></a></p></td>
<td><p>レンダリングは、一部のグラフィックス DDI 関数をフックするプラグインできます。 注意このメソッドと<strong>IPrintOemPS::DisableDriver</strong>見なす必要がありますのペアとして 1 つが実装されている場合、もう一方も実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553215" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553215)"><strong>IPrintOemPS::EnablePDEV</strong></a></p></td>
<td><p>レンダリングを独自の PDEV 構造を作成するプラグインに使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553221" data-raw-source="[&lt;strong&gt;IPrintOemPS::GetInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553221)"><strong>IPrintOemPS::GetInfo</strong></a></p></td>
<td><p>(必要な実装です。)プラグインの識別情報を表示します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553228" data-raw-source="[&lt;strong&gt;IPrintOemPS::PublishDriverInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553228)"><strong>IPrintOemPS::PublishDriverInterface</strong></a></p></td>
<td><p>(必要な実装です。)Pscript5 ドライバーへのポインターを提供<a href="iprintoemdriverps-com-interface.md" data-raw-source="[IPrintOemDriverPS COM interface](iprintoemdriverps-com-interface.md)">IPrintOemDriverPS COM インターフェイス</a>、 <a href="iprintcoreps2-com-interface.md" data-raw-source="[IPrintCorePS2 COM interface](iprintcoreps2-com-interface.md)">IPrintCorePS2 COM インターフェイス</a>、または<a href="https://msdn.microsoft.com/library/windows/hardware/ff552906" data-raw-source="[IPrintCoreHelperPS interface](https://msdn.microsoft.com/library/windows/hardware/ff552906)">IPrintCoreHelperPS インターフェイス</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553233" data-raw-source="[&lt;strong&gt;IPrintOemPS::ResetPDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553233)"><strong>IPrintOemPS::ResetPDEV</strong></a></p></td>
<td><p>レンダリングは、その PDEV 構造をリセットするプラグインできます。</p></td>
</tr>
</tbody>
</table>

 

詳細については、[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)を参照してください。

 

 




