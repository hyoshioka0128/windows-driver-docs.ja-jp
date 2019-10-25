---
title: IPrintOemPS COM インターフェイス
description: IPrintOemPS COM インターフェイス
ms.assetid: 504db6ab-291e-4fba-995d-49a22a3a7c7f
keywords:
- IPrintOemPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1a121186b6f53f905fae6592209baff2f6ae60f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844319"
---
# <a name="iprintoemps-com-interface"></a>IPrintOemPS COM インターフェイス





`IPrintOemPS` COM インターフェイスは、Pscript5 用の[プリンターグラフィックス DLL](printer-graphics-dll.md)がレンダリングプラグインと通信する手段です。 `IPrintOemPS` インターフェイスは、各レンダリングプラグインによって実装されます。

次の表に、`IPrintOemPS` インターフェイスによって提供されるすべてのメソッドとその説明を示します。 レンダリングプラグインでは、表示されているすべてのメソッドを定義する必要があります。 メソッドが不要な場合は、単に E\_NOTIMPL を返すことができます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-command" data-raw-source="[&lt;strong&gt;IPrintOemPS::Command&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-command)"><strong>IPrintOemPS:: Command</strong></a></p></td>
<td><p>レンダリングプラグインが Postscript コマンドを印刷ジョブのデータストリームに挿入できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-devmode" data-raw-source="[&lt;strong&gt;IPrintOemPS::DevMode&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-devmode)"><strong>IPrintOemPS::D evMode</strong></a></p></td>
<td><p>レンダリングプラグインのプライベート<a href="https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)"><strong>Devmodew</strong></a>メンバーに対して操作を実行します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disabledriver" data-raw-source="[&lt;strong&gt;IPrintOemPS::DisableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disabledriver)"><strong>IPrintOemPS::D isableDriver</strong></a></p></td>
<td><p>レンダリングプラグインの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver)"><strong>IPrintOemPS:: EnableDriver</strong></a>メソッドによって割り当てられたリソースを解放します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disablepdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::DisablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disablepdev)"><strong>IPrintOemPS::D isablePDEV</strong></a></p></td>
<td><p>レンダリングプラグインが、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev)"><strong>IPrintOemPS:: EnablePDEV</strong></a>メソッドによって割り当てられたプライベート pdev 構造体を削除できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver)"><strong>IPrintOemPS:: EnableDriver</strong></a></p></td>
<td><p>レンダリングプラグインがいくつかのグラフィックス DDI 関数をフックできるようにします。 このメソッドと<strong>IPrintOemPS::D isableDriver</strong>はペアと見なす必要があることに注意してください。実装されている場合は、もう一方も実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev)"><strong>IPrintOemPS:: EnablePDEV</strong></a></p></td>
<td><p>レンダリングプラグインで独自の PDEV 構造体を作成できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-getinfo" data-raw-source="[&lt;strong&gt;IPrintOemPS::GetInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-getinfo)"><strong>IPrintOemPS:: GetInfo</strong></a></p></td>
<td><p>(実装が必要です)。レンダリングプラグインの識別情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-publishdriverinterface" data-raw-source="[&lt;strong&gt;IPrintOemPS::PublishDriverInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-publishdriverinterface)"><strong>IPrintOemPS::P ublishDriverInterface</strong></a></p></td>
<td><p>(実装が必要です)。Pscript5 ドライバーの<a href="iprintoemdriverps-com-interface.md" data-raw-source="[IPrintOemDriverPS COM interface](iprintoemdriverps-com-interface.md)">Iprintoemdriverps COM インターフェイス</a>、 <a href="iprintcoreps2-com-interface.md" data-raw-source="[IPrintCorePS2 COM interface](iprintcoreps2-com-interface.md)">IPrintCorePS2 COM インターフェイス</a>、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps" data-raw-source="[IPrintCoreHelperPS interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)">iprintcore perps インターフェイス</a>へのポインターを提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-resetpdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::ResetPDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-resetpdev)"><strong>IPrintOemPS:: ResetPDEV</strong></a></p></td>
<td><p>レンダリングプラグインが PDEV 構造をリセットできるようにします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 




