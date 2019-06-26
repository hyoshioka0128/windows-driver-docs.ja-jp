---
title: バグ チェック 0x138 GPIO_CONTROLLER_DRIVER_ERROR
description: GPIO_CONTROLLER_DRIVER_ERROR のバグ チェックでは、0x00000138 の値を持ちます。 このバグ チェックでは、GPIO クラスの拡張機能ドライバーに致命的なエラーが発生したことを示します。
ms.assetid: 4025D968-10F9-4F2F-953F-914A4BE7D883
keywords:
- バグ チェック 0x138 GPIO_CONTROLLER_DRIVER_ERROR
- GPIO_CONTROLLER_DRIVER_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- GPIO_CONTROLLER_DRIVER_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1bef9442e3142a7aba536dbf65e4c4d690c109cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367834"
---
# <a name="bug-check-0x138-gpiocontrollerdrivererror"></a>バグ チェック 0x138:GPIO\_コント ローラー\_ドライバー\_エラー


GPIO\_コント ローラー\_ドライバー\_エラーのバグ チェックが 0x00000138 の値を持ちます。 このバグ チェックでは、GPIO クラスの拡張機能ドライバーに致命的なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="gpiocontrollerdrivererror-parameters"></a>GPIO\_コント ローラー\_ドライバー\_エラー パラメーター


*パラメーター 1*違反の種類を示します。 その他のパラメーターの意味は、の値によって異なります。*パラメーター 1*します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>GSIV</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>特定の GSIV を管理する GPIO コント ローラーが登録されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>コンテキストの値</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>クライアント ドライバーでは、ロックに無効なコンテキストを指定または要求のロックを解除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>重要な切り替えが要求されているかどうかを示します。</p></td>
<td align="left"><p>かどうか、銀行は既に F1 重大でない遷移が原因を示します。</p></td>
<td align="left"><p>かどうか、銀行は既に F1 により重要な移行を示します。</p></td>
<td align="left"><p>PoFx では、GPIO コント ローラーが、不適切な F1 電源の状態や重要な遷移を使用して銀行を送信することを要求します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>重要な切り替えが要求されているかどうかを示します。</p></td>
<td align="left"><p>銀行が重要ではない移行のための f1 がかどうかを示します。</p></td>
<td align="left"><p>銀行が重要な移行のための f1 があるかどうかを示します。</p></td>
<td align="left"><p>PoFx では、GPIO コント ローラーが、不適切な F0 電源の状態や重要な遷移を使用して銀行を送信することを要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>NTSTATUS</p></td>
<td align="left"><p>GPIO デバイス拡張機能</p></td>
<td align="left"><p>GPIO 割り込みパラメーター</p></td>
<td align="left"><p>Soc に GPIO 割り込み操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>NTSTATUS</p></td>
<td align="left"><p>GPIO デバイス拡張機能</p></td>
<td align="left"><p>GPIO IO パラメーター</p></td>
<td align="left"><p>Soc に GPIO IO 操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>リビジョン ID</p></td>
<td align="left"><p>関数インデックス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>_DSM メソッドには、不適切なデータが返されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




