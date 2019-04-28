---
title: バグ チェック 0x73 CONFIG_LIST_FAILED
description: CONFIG_LIST_FAILED のバグ チェックでは、0x00000073 の値を持ちます。 このバグ チェックでは、コア システム ハイブとも呼ばれる、最上位のレジストリ キーのいずれかのレジストリ ツリーではリンクできませんを示します。
ms.assetid: fec1f3ee-5405-49c2-8082-75adfdabd6b8
keywords:
- バグ チェック 0x73 CONFIG_LIST_FAILED
- CONFIG_LIST_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CONFIG_LIST_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d3d1a132d29a294a5c72ee92599db5c5dc6842b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367518"
---
# <a name="bug-check-0x73-configlistfailed"></a>バグ チェック 0x73:CONFIG\_一覧\_失敗


CONFIG\_一覧\_失敗のバグ チェックが 0x00000073 の値を持ちます。 このバグ チェックでは、コア システム ハイブとも呼ばれる、最上位のレジストリ キーのいずれかのレジストリ ツリーではリンクできませんを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="configlistfailed-parameters"></a>CONFIG\_一覧\_FAILED パラメーター


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
<td align="left"><p>ハイブの読み込みに失敗したことを想定する Windows オペレーティング システムの原因となった NT 状態コード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>Hive の一覧での hive のインデックス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ハイブのファイル名を格納する UNICODE_STRING 構造体へのポインター</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

レジストリ ハイブをリンクできませんには、SAM、セキュリティ、ソフトウェア、または既定値があります。 正常に読み込まれたため、hive は有効です。

なぜ、hive レジストリ ツリーでリンクに失敗してパラメーター 2 を確認します。 このエラーの一般的な原因の 1 つは、Windows オペレーティング システムがシステム ドライブのディスク領域があります。 (この場合、このパラメーターは 0xC000017D、ステータス\_いいえ\_ログ\_領域です)。もう 1 つの一般的な問題は、プールを割り当てることが失敗したことができます。 (この場合、パラメーター 2 は 0xC000009A、ステータス\_不十分\_リソースです)。その他の状態コードを調査する必要があります。

 

 




