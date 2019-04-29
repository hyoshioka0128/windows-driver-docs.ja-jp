---
title: Bug Check 0x156 WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP
description: WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP のバグ チェックでは、0x00000156 の値を持ちます。 これは、Winsock がハングしたトランスポート エンドポイントの閉じる要求を検出したことを示します。
ms.assetid: F5B53149-3051-459C-834A-6AE17C56AEE6
keywords:
- Bug Check 0x156 WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP
- WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 99d2f912626b29977d10403e7e65f7574eb53aef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335554"
---
# <a name="bug-check-0x156-winsockdetectedhungclosesocketlivedump"></a>バグ チェック 0x156:WINSOCK\_検出\_ハング\_CLOSESOCKET\_LIVEDUMP


WINSOCK\_検出\_ハング\_CLOSESOCKET\_LIVEDUMP バグ チェックが 0x00000156 の値を持ちます。 これは、Winsock がハングしたトランスポート エンドポイントの閉じる要求を検出したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="winsockdetectedhungclosesocketlivedump-parameters"></a>WINSOCK\_検出\_ハング\_CLOSESOCKET\_LIVEDUMP パラメーター


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
<td align="left">AFD エンドポイント ポインター (! afdkd.endp &lt;ptr&gt;)</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>エンドポイントのトランスポートの種類</p>
<p>0x1:UDP データグラム</p>
<p>0x2:生のデータグラム</p>
<p>0x3:TCP リスナー</p>
<p>0x4:TCP エンドポイント</p></td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">データグラム エンドポイント用にバッファリングされた送信バイト数</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">afd!NETIO_SUPER_TRIAGE_BLOCK</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Closesocket 要求を処理中には、Winsock はハングしたトランスポート エンドポイントの終了要求を検出しました。 システムは、分析、ライブのダンプを生成し、ハングしたトランスポート エンドポイントの終了要求の完了を待つことがなく closesocket 要求が完了します。

 

 




