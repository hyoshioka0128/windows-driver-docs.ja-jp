---
title: IWiaLog COM インターフェイス
description: IWiaLog COM インターフェイス
ms.assetid: e5d42b5d-796f-42f3-9c01-4234b8765ca6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c06a0225ddce866cb513e258040fbc0aea6ee40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537110"
---
# <a name="iwialog-com-interface"></a>IWiaLog COM インターフェイス





[ **IWiaLog インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff543935) Microsoft Windows XP では古いおよびそれ以降は、現在サポートされていません。 WIA 診断ログのマクロを代わりに使用します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543932" data-raw-source="[&lt;strong&gt;IWiaLog::InitializeLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543932)"><strong>IWiaLog::InitializeLog</strong></a></p></td>
<td><p>ログ記録ユーティリティを初期化します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543939" data-raw-source="[&lt;strong&gt;IWiaLog::Log&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543939)"><strong>IWiaLog::Log</strong></a></p></td>
<td><p>ファイルまたはその他のターゲットにメッセージを記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543928" data-raw-source="[&lt;strong&gt;IWiaLog::hResult&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543928)"><strong>IWiaLog::hResult</strong></a></p></td>
<td><p>HRESULT を文字列に変換します。</p></td>
</tr>
</tbody>
</table>

 

このインターフェイスの詳細については、[IWiaLog インターフェイスおよび診断ログ マクロ](https://msdn.microsoft.com/library/windows/hardware/ff543937)を参照してください。

 

 




