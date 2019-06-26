---
title: レンダリング プラグインからドライバー設定にアクセスする
description: レンダリング プラグインからドライバー設定にアクセスする
ms.assetid: d13526f5-85e1-4036-98fb-aea2c6d5a1e3
keywords:
- プラグインを WDK 印刷ドライバーへのアクセス設定の表示
- WDK 印刷プラグインのステータス情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1b794c6b48d20fe9aeb5cf15a0ad50468673643
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385703"
---
# <a name="accessing-driver-settings-from-rendering-plug-ins"></a>レンダリング プラグインからドライバー設定にアクセスする





プラグインのレンダリングには、プリンターの機能とその他のドライバーの内部情報の現在の状態を取得できます。 次の COM インターフェイス メソッドは、Microsoft のプリンター ドライバー内では実装され、レンダリング プラグインを使用して呼び出すことができます。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>Unidrv レンダリング プラグインでは、次のメソッドを実装します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetDriverSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetdriversetting)"><strong>IPrintOemDriverUni::DrvGetDriverSetting</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetstandardvariable" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetStandardVariable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetstandardvariable)"><strong>IPrintOemDriverUni::DrvGetStandardVariable</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata)"><strong>IPrintOemDriverUni::DrvGetGPDData</strong></a></p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>Pscript5 レンダリング プラグインでは、次のメソッドを実装します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriverps-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverPS::DrvGetDriverSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriverps-drvgetdriversetting)"><strong>IPrintOemDriverPS::DrvGetDriverSetting</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




