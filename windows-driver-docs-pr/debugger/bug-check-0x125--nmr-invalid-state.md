---
title: バグ チェック 0x125 NMR_INVALID_STATE
description: NMR_INVALID_STATE のバグ チェックでは、0x00000125 の値を持ちます。 これは、NMR (ネットワーク モジュールのレジストラー) に無効な状態が検出されたことを示します。 状態の種類のパラメーター 1 を参照してください。
ms.assetid: DD80FC61-8211-46A0-9D44-CF1E729B12D4
keywords:
- バグ チェック 0x125 NMR_INVALID_STATE
- NMR_INVALID_STATE
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- NMR_INVALID_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1a1ca16eb1ec81de3bbbd7102c1223135c4c37a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367886"
---
# <a name="bug-check-0x125-nmrinvalidstate"></a>バグ チェック 0x125:NMR\_無効な\_状態


NMR\_無効な\_状態のバグ チェックが 0x00000125 の値を持ちます。 これは、NMR (ネットワーク モジュールのレジストラー) に無効な状態が検出されたことを示します。 状態の種類のパラメーター 1 を参照してください。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="nmrinvalidstate-parameters"></a>NMR\_無効な\_状態パラメーター


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
<td align="left"><p>バグチェックのサブタイプ。</p>
<p>0x0 :マシン チェック例外</p>
<p>パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。</p>
<p>3 - パラメーター MCi_STATUS 値の上位 32 ビット。</p>
<p>4 - パラメーター MCi_STATUS 値の下位 32 ビット。</p>
<p>0x1:マシン チェックを修正しました</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。
<p>0x2:修正されたプラットフォーム エラー</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。
<p>0x3:マスク不可能割り込み</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。
<p>0x4:PCI Express エラー</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。
<p>0x5。一般的なエラー</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。
<p>0x6:初期化エラー</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。
<p>0x7:起動エラー</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。
<p>0x8:SCI 一般的なエラー</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。
<p>0x9:Itanium マシン チェックの中止</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。
3 - SAL ログのバイト長のパラメーター。
パラメーター 4 - SAL ログのアドレス。
<p>0 xa:Itanium はマシン チェックを修正しました</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。
<p>0xb :Itanium は、プラットフォーム エラーの修正</p>
パラメーター 2 - WHEA_ERROR_RECORD 構造体のアドレス。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">NMI ハンドルへのポインター</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">使用可能な場合は、必要な型へのポインター</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

 

 




