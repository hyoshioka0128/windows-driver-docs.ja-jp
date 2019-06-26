---
title: IWiaLog COM インターフェイス
description: IWiaLog COM インターフェイス
ms.assetid: e5d42b5d-796f-42f3-9c01-4234b8765ca6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80cda9b71779f3686c99dd1ca97c48e1cbff8231
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378896"
---
# <a name="iwialog-com-interface"></a>IWiaLog COM インターフェイス





[ **IWiaLog インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwialog) Microsoft Windows XP では古いおよびそれ以降は、現在サポートされていません。 WIA 診断ログのマクロを代わりに使用します。

これは、旧バージョンとの互換性を保つのために提供されます。 このインターフェイスのメソッドは、エラー、トレース、および警告メッセージをログに書き込む、ミニドライバーを許可します。 **IWiaLog**インターフェイスは、次のメソッドを提供します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-initializelog" data-raw-source="[&lt;strong&gt;IWiaLog::InitializeLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-initializelog)"><strong>IWiaLog::InitializeLog</strong></a></p></td>
<td><p>ログ記録ユーティリティを初期化します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-log" data-raw-source="[&lt;strong&gt;IWiaLog::Log&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-log)"><strong>IWiaLog::Log</strong></a></p></td>
<td><p>ファイルまたはその他のターゲットにメッセージを記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-hresult" data-raw-source="[&lt;strong&gt;IWiaLog::hResult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-hresult)"><strong>IWiaLog::hResult</strong></a></p></td>
<td><p>HRESULT を文字列に変換します。</p></td>
</tr>
</tbody>
</table>

 

このインターフェイスの詳細については、次を参照してください。 [IWiaLog インターフェイスおよび診断ログ マクロ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)します。

 

 




