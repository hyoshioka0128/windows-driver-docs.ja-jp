---
title: バグ チェック 0x188 CLUSTER_CSVFS_LIVEDUMP
description: CLUSTER_CSVFS_LIVEDUMP のバグ チェックでは、0x00000188 の値を持ちます。 これは、CSVFS に一貫性のない状態をデバッグする際にこの livedump が開始されたことを示します。
ms.assetid: 220B0CDB-6E10-4262-A07C-042E8BA21D7F
keywords:
- バグ チェック 0x188 CLUSTER_CSVFS_LIVEDUMP
- CLUSTER_CSVFS_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CLUSTER_CSVFS_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c5cc8d46050370f19fe257a3c0dcc43449b5f9d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367677"
---
# <a name="bug-check-0x188-clustercsvfslivedump"></a>バグ チェック 0x188:クラスター\_CSVFS\_LIVEDUMP


クラスター\_CSVFS\_LIVEDUMP バグ チェックが 0x00000188 の値を持ちます。 これは、CSVFS に一貫性のない状態をデバッグする際にこの livedump が開始されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="clustercsvfslivedump-parameters"></a>クラスター\_CSVFS\_LIVEDUMP パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>理由コード</p>
0x1:[なし] に oplock のダウン グレードでキャッシュの消去に失敗しました
<p>2-アドレスの CSVFS! _SCB</p>
0x2:[なし] から oplock のアップグレード時にキャッシュの消去に失敗しました
<p>2-アドレスの CSVFS! _SCB</p>
0x3:消去の障害モードの設定でキャッシュの消去
<p>2-アドレスの CSVFS! _SCB</p>
0x4:キャッシュのフラッシュに失敗しました [なし] に oplock のダウン グレード
<p>2-アドレスの CSVFS! _SCB</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">予約済み</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

最初のパラメーターにはと CSVFS 検出データが破損する現在の状態が発生する理由コードが含まれています、不整合の他の並べ替えとライブのダンプが生成またはこの状態コード。 パラメーター 1 がコードの作成はこのライブ ダンプをどのようなシナリオをポイントします。 その他のパラメーターは、理由コードのコンテキストで解釈する必要があります。

 

 




