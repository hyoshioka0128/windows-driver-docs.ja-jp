---
title: バグチェック 0xBFF BC_BTHMINI_VERIFIER_FAULT
description: BC_BTHMINI_VERIFIER_FAULT のバグチェックの値は0x00000BFF です。 これは、Bluetooth ミニポート拡張ドライバーの検証ツールが違反をキャッチしたことを示します。
ms.assetid: 4BB54209-89EA-455D-B850-CC2A96A43C87
keywords:
- バグチェック 0xBFF BC_BTHMINI_VERIFIER_FAULT
- BC_BTHMINI_VERIFIER_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BC_BTHMINI_VERIFIER_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 014ce8979258d37187c8733570e559491febeb41
ms.sourcegitcommit: d2dab8b8bf335835d0341ca3f0a36eab0ec028f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72892684"
---
# <a name="bug-check-0xbff-bc_bthmini_verifier_fault"></a>バグチェック 0xBFF: BC\_BTHMINI\_検証ツール\_エラー


BC\_BTHMINI\_VERIFIER\_の不具合のバグチェックには、0x00000BFF という値があります。 これは、Bluetooth ミニポート拡張ドライバーの検証ツールが違反をキャッチしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="bc_bthmini_verifier_fault-parameters"></a>BC\_BTHMINI\_VERIFIER\_FAULT パラメーター


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
<td align="left"><p>Bluetooth 検証ツールのエラーのサブタイプ。</p>
<div class="code">
<code>0x1 : An attempt was made to return a packet with type that mis-matched its original request.
                  2 - Returned packet type
                  3 - Expected packet type
                  4 - Reserved
            0x2 : An attempt was made to return an unexpected status code and caused the packet to be discarded.
                  2 - Unexpected return status
                  3 - Reserved
                  4 - Reserved
            0x3 : Incorrect output buffer size was returned to indicate number of bytes written by the lower transport driver.
                  2 - Unexpected buffer size
                  3 - Expected buffer size
                  4 - Reserved</code>
</div></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">「パラメーター1」を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">「パラメーター1」を参照してください。</td>
</tr>
<tr class="even">
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">「パラメーター1」を参照してください。</td>
</tr>
</tbody>
</table>



<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
パラメーター1は違反の種類を示します。 呼び出し履歴を調べて、動作が不適切なドライバーを特定します。








