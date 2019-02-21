---
title: バグ チェック 0x44 MULTIPLE_IRP_COMPLETE_REQUESTS
description: MULTIPLE_IRP_COMPLETE_REQUESTS のバグ チェックでは、0x00000044 の値を持ちます。 これは、ドライバーが IRP は完了要求しようとしたことを示します既にを完了します。
ms.assetid: bc60b4b3-aded-4c67-bbaa-aad1b6b38d30
keywords:
- バグ チェック 0x44 MULTIPLE_IRP_COMPLETE_REQUESTS
- MULTIPLE_IRP_COMPLETE_REQUESTS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MULTIPLE_IRP_COMPLETE_REQUESTS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dcabee01463fa41253f27803dab9ac3705d32c29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557845"
---
# <a name="bug-check-0x44-multipleirpcompleterequests"></a>バグ チェック 0x44 の。複数\_IRP\_完了\_要求


複数\_IRP\_完了\_要求のバグ チェックが 0x00000044 の値を持ちます。 これは、ドライバーが IRP は完了要求しようとしたことを示します既にを完了します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="multipleirpcompleterequests-parameters"></a>複数\_IRP\_完了\_要求パラメーター


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

ドライバーが呼び出されて**IoCompleteRequest** IRP が完了したことを確認するが、パケットは既に完了します。

<a name="resolution"></a>解決方法
----------

これは、難しいバグを最も簡単なケースでは、-、独自のパケットを 2 回完了しようとしています。 ドライバー - には、問題の原因は通常ありませんので、見つけるです。 多くの場合、2 つ個別のドライバーごとに手順を完了しようとしましたが、パケットの場合、自分が所有と思われる各します。 最初の要求が成功し、このバグ チェックでその結果、2 つ目が失敗しました。

どのドライバーがシステムのエラーの原因を追跡は、最初のドライバーの記録は、2 つ目でカバーされていたために、困難です。 ただし、現在の要求のドライバー スタックは、スタック内の場所の各デバイス オブジェクトのフィールドを調べることで確認できます。

 

 




