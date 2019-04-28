---
title: レンダリング プラグインからドライバー設定にアクセスする
description: レンダリング プラグインからドライバー設定にアクセスする
ms.assetid: d13526f5-85e1-4036-98fb-aea2c6d5a1e3
keywords:
- プラグインを WDK 印刷ドライバーへのアクセス設定の表示
- WDK 印刷プラグインのステータス情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0784a4ebe720ecd0124c5edc29b28d75d386aa84
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372876"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553126" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetDriverSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553126)"><strong>IPrintOemDriverUni::DrvGetDriverSetting</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553129" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetStandardVariable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553129)"><strong>IPrintOemDriverUni::DrvGetStandardVariable</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553128" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553128)"><strong>IPrintOemDriverUni::DrvGetGPDData</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553102" data-raw-source="[&lt;strong&gt;IPrintOemDriverPS::DrvGetDriverSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553102)"><strong>IPrintOemDriverPS::DrvGetDriverSetting</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




