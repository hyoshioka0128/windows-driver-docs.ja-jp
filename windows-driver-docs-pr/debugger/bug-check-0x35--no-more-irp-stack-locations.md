---
title: バグ チェック 0x35 NO_MORE_IRP_STACK_LOCATIONS
description: NO_MORE_IRP_STACK_LOCATIONS のバグ チェックでは、0x00000035 の値を持ちます。 このバグ チェックでは、保留パケットがある残りのスタックの場所がなくなると発生します。
ms.assetid: 1a8d5a1b-70aa-4846-bafe-0fef041570c1
keywords:
- バグ チェック 0x35 NO_MORE_IRP_STACK_LOCATIONS
- NO_MORE_IRP_STACK_LOCATIONS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NO_MORE_IRP_STACK_LOCATIONS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56c2aa094e8171c97b18db81c5da5d511b9d5675
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519505"
---
# <a name="bug-check-0x35-nomoreirpstacklocations"></a>バグ チェック 0x35:いいえ\_詳細\_IRP\_スタック\_場所


いいえ、\_詳細\_IRP\_スタック\_場所のバグ チェックが 0x00000035 の値を持ちます。 このバグ チェックが発生したときに、**保留**パケットが残りのスタックの場所がなくなります。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="nomoreirpstacklocations-parameters"></a>いいえ\_詳細\_IRP\_スタック\_場所パラメーター


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
<td align="left"><p>1</p></td>
<td align="left"><p>IRP のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

下位レベルのドライバーを呼び出すしようとしましたより高度なドライバー、**保留**インターフェイスがパケット内の複数スタック場所がありません。 これにより、下位レベルのドライバーでそのパラメーターにアクセスできなくなります。

これは、(必要に応じて) 下位レベルのドライバーのパラメーターが入力されていない場合より高いレベルのドライバーは先に進むために、悲惨な状況では、です。 後者のドライバーのスタックの場所がないため、前者が実際に書き込まれた、パケットの終わり。 これは、その他のメモリの一部がも破損していることを意味します。

 

 




