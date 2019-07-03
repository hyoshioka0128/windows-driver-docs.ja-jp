---
title: バグ チェック 0x75 CANNOT_WRITE_CONFIGURATION
description: CANNOT_WRITE_CONFIGURATION のバグ チェックでは、0x00000075 の値を持ちます。 このバグ チェックでは、マップ ファイルをシステム レジストリ ハイブ ファイルを変換することはできませんを示します。
ms.assetid: 0190de02-8bd1-4c20-839d-bf9fb517567d
keywords:
- バグ チェック 0x75 CANNOT_WRITE_CONFIGURATION
- CANNOT_WRITE_CONFIGURATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CANNOT_WRITE_CONFIGURATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e6db578c4ddbb19a371f730e882e7cb11ec46ff
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519213"
---
# <a name="bug-check-0x75-cannotwriteconfiguration"></a>バグ チェック 0x75:できません\_書き込み\_構成


できない\_書き込み\_構成のバグ チェックが 0x00000075 の値を持ちます。 このバグ チェックでは、マップ ファイルをシステム レジストリ ハイブ ファイルを変換することはできませんを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="cannotwriteconfiguration-parameters"></a>できません\_書き込み\_構成パラメーター


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
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>ハイブを変換することがありましたが失敗したことを想定する Windows オペレーティング システムの原因となった NT 状態コード</p></td>
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

できない\_書き込み\_システムは、プールから、Windows オペレーティング システムは、hive を再び開くことはできませんと構成のバグ チェックが通常に発生します。

十分なプールが使用できるように、システムの初期化中に早いハイブ ファイルの変換が発生したため、このバグ チェックは発生ほぼしません。

 

 




