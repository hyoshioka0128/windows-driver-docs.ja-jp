---
title: IPrintOemDriverPS COM インターフェイス
description: IPrintOemDriverPS COM インターフェイス
ms.assetid: 32975728-501f-45ac-a53d-34cf286bc433
keywords:
- IPrintOemDriverPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89a298090fb3e4d4383af4563a7f4026730e12aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549938"
---
# <a name="iprintoemdriverps-com-interface"></a>IPrintOemDriverPS COM インターフェイス





`IPrintOemDriverPS` COM インターフェイスのプラグインの Pscript5 プリンター グラフィックス DLL によって提供されるユーティリティ操作へのアクセスをレンダリングを提供します。 これらの操作では、印刷スプーラをデータ ストリームを送信し、ドライバー管理の情報を取得します。

次の表とによって定義されたメソッドのすべてについて説明します、`IPrintOemDriverPS`インターフェイス。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553102" data-raw-source="[&lt;strong&gt;IPrintOemDriverPS::DrvGetDriverSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553102)"><strong>IPrintOemDriverPS::DrvGetDriverSetting</strong></a></p></td>
<td><p>プリンターの機能とその他の内部情報の現在の状態を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553103" data-raw-source="[&lt;strong&gt;IPrintOemDriverPS::DrvWriteSpoolBuf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553103)"><strong>IPrintOemDriverPS::DrvWriteSpoolBuf</strong></a></p></td>
<td><p>プリンター データをスプーラーに送信します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)を参照してください。

 

 




