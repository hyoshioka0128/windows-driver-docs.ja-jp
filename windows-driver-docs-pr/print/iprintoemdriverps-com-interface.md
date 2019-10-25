---
title: IPrintOemDriverPS COM インターフェイス
description: IPrintOemDriverPS COM インターフェイス
ms.assetid: 32975728-501f-45ac-a53d-34cf286bc433
keywords:
- IPrintOemDriverPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae9fd5789c32ffde3b067452e25387f7b5387fcd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844321"
---
# <a name="iprintoemdriverps-com-interface"></a>IPrintOemDriverPS COM インターフェイス





`IPrintOemDriverPS` COM インターフェイスは、Pscript5 のプリンターグラフィックス DLL によって提供されるユーティリティ操作へのアクセスを備えたレンダリングプラグインを提供します。 これらの操作は、データストリームを印刷スプーラに送信し、ドライバーによって管理される情報を取得します。

次の表に、`IPrintOemDriverPS` インターフェイスで定義されているすべてのメソッドとその説明を示します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverps-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverPS::DrvGetDriverSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverps-drvgetdriversetting)"><strong>IPrintOemDriverPS::D rvGetDriverSetting</strong></a></p></td>
<td><p>プリンター機能とその他の内部情報の現在の状態を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverps-drvwritespoolbuf" data-raw-source="[&lt;strong&gt;IPrintOemDriverPS::DrvWriteSpoolBuf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverps-drvwritespoolbuf)"><strong>IPrintOemDriverPS::D rvWriteSpoolBuf</strong></a></p></td>
<td><p>プリンターデータをスプーラに送信します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 




