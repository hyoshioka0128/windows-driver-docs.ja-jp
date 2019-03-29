---
title: バグ チェック 0x126 NETIO_INVALID_POOL_CALLER
description: NETIO_INVALID_POOL_CALLER のバグ チェックでは、0x00000126 の値を持ちます。 これは、無効なプールの要求を FSB や MDL など、マネージ netio メモリ プールにしたことを示します。
ms.assetid: D155D39D-0E8B-4BA5-91B4-AF8F291F7F1F
keywords:
- バグ チェック 0x126 NETIO_INVALID_POOL_CALLER
- NETIO_INVALID_POOL_CALLER
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- NETIO_INVALID_POOL_CALLER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ffea7416fc30165647522f46136a8c67870ddb99
ms.sourcegitcommit: 598259684cbfcf39b16dcc91bd8d341b43fb8876
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2019
ms.locfileid: "56582871"
---
# <a name="bug-check-0x126-netioinvalidpoolcaller"></a>バグ チェック 0x126:NETIO\_無効な\_プール\_呼び出し元


NETIO\_無効な\_プール\_呼び出し元のバグ チェックが 0x00000126 の値を持ちます。 これは、無効なプールの要求を FSB や MDL など、マネージ netio メモリ プールにしたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="netioinvalidpoolcaller-parameters"></a>NETIO\_無効な\_プール\_呼び出し元のパラメーター


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
<p>0x1:無効なプール。 プールが、状態が無効です。</p>
パラメーター 2 - メモリ ブロックへのポインターまたは MDL です。
パラメーター 3 - ページへのポインター。
パラメーター 4 - CPU のプールへのポインター。
<p>0x2:無効な MDL します。 MDL では、無効な状態にあります。</p>
パラメーター 2 - MDL へのポインター。
パラメーター 3 - CPU のプールへのポインター。
パラメーター 4 - プール ヘッダーへのポインター。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
</tbody>
</table>

 

 

 




