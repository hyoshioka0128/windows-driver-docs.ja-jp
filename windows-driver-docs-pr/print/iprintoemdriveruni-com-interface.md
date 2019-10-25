---
title: IPrintOemDriverUni COM インターフェイス
description: IPrintOemDriverUni COM インターフェイス
ms.assetid: 84b3f43c-039a-4e9d-b596-41c08f1e0284
keywords:
- IPrintOemDriverUni
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41947e28b9765f72c913dc98dfafa688db714bd7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844323"
---
# <a name="iprintoemdriveruni-com-interface"></a>IPrintOemDriverUni COM インターフェイス





`IPrintOemDriverUni COM` インターフェイスは、Unidrv 用プリンターグラフィックス DLL によって提供されるユーティリティ操作へのアクセスを備えたレンダリングプラグインを提供します。 これらの操作は、データストリームを印刷スプーラに送信し、ドライバーによって管理される情報を取得します。

次の表に、 **Iprintoemdriveruni**インターフェイスで定義されているすべてのメソッドとその説明を示します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetDriverSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetdriversetting)"><strong>IPrintOemDriverUni::D rvGetDriverSetting</strong></a></p></td>
<td><p>プリンター機能とその他の内部情報の現在の状態を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata)"><strong>IPrintOemDriverUni::D rvGetGPDData</strong></a></p></td>
<td><p>プリンターの<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-generic-printer-description--gpd-" data-raw-source="&lt;em&gt;generic printer description (GPD)&lt;/em&gt;"><em>汎用プリンターの説明 (GPD)</em></a>ファイルで定義されているデータを取得するためのプラグインのレンダリングを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetstandardvariable" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetStandardVariable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetstandardvariable)"><strong>IPrintOemDriverUni::D rvGetStandardVariable</strong></a></p></td>
<td><p>レンダリングプラグインを有効にして、Unidrv の<a href="standard-variables.md" data-raw-source="[standard variables](standard-variables.md)">標準変数</a>の現在の値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvUniTextOut&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)"><strong>IPrintOemDriverUni::D rvUniTextOut</strong></a></p></td>
<td><p>デバイスで管理された描画サーフェイスを使用してレンダリングプラグインを有効にし、テキスト文字列を簡単に出力できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwriteabortbuf" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvWriteAbortBuf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwriteabortbuf)"><strong>IPrintOemDriverUni::D rvWriteAbortBuf</strong></a></p></td>
<td><p>ユーザーが印刷ジョブを終了した後に、レンダリングプラグインがプリンターをリセットできるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvWriteSpoolBuf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf)"><strong>IPrintOemDriverUni::D rvWriteSpoolBuf</strong></a></p></td>
<td><p>プリンターデータをスプーラに送信します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvxmoveto" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvXMoveTo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvxmoveto)"><strong>IPrintOemDriverUni::D rvXMoveTo</strong></a></p></td>
<td><p>カーソルの x 位置の変更を Unidrv に通知します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvymoveto" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvYMoveTo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvymoveto)"><strong>IPrintOemDriverUni::D rvYMoveTo</strong></a></p></td>
<td><p>カーソルの y 位置の変更を Unidrv に通知します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 




