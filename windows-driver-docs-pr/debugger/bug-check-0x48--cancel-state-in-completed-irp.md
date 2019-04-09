---
title: Bug Check 0x48 CANCEL_STATE_IN_COMPLETED_IRP
description: CANCEL_STATE_IN_COMPLETED_IRP のバグ チェックでは、0x00000048 の値を持ちます。 これは、I/O 要求パケット (IRP) が完了しましたが、および、し、取り消された後を示します。
ms.assetid: e706cf9b-8800-41ce-9bad-e4b9a8503051
keywords:
- Bug Check 0x48 CANCEL_STATE_IN_COMPLETED_IRP
- CANCEL_STATE_IN_COMPLETED_IRP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CANCEL_STATE_IN_COMPLETED_IRP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ded2f30d55bfa8c58892e813b8fb224c0aa7f39
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238625"
---
# <a name="bug-check-0x48-cancelstateincompletedirp"></a>バグ チェック 0x48:キャンセル\_状態\_IN\_完了\_IRP


キャンセル\_状態\_IN\_完了\_IRP のバグ チェックが 0x00000048 の値を持ちます。 これは、I/O 要求パケット (IRP) が完了しましたが、および、し、取り消された後を示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="cancelstateincompletedirp-parameters"></a>キャンセル\_状態\_IN\_完了\_IRP パラメーター


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
<td align="left"><p>IRP へのポインター</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>設定、ドライバーによってキャンセル ルーチン</p></td>
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

含まれていた IRP を*キャンセル*が日常的なセットが正常に完了しました。 ドライバーが IRP のと呼ばれる完了した後、*キャンセル*ルーチン。

これは、ドライバーは IRP の完了、キャンセルしようとして発生する可能性があります。

これは、ことも原因 2 つのドライバーによって、不適切な方法で同じ IRP にアクセスしようとした各します。

<a name="resolution"></a>解決方法
----------

どのドライバーまたはスタックは、バグのチェックを原因を確認するのには、キャンセル ルーチン パラメーターを使用できます。

 

 




