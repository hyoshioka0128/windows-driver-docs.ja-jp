---
title: バグ チェック 0x178 ELAM_DRIVER_DETECTED_FATAL_ERROR
description: ELAM_DRIVER_DETECTED_FATAL_ERROR のバグ チェックでは、0x00000178 の値を持ちます。 これは、ELAM ドライバーに致命的なエラーが検出されたことを示します。
ms.assetid: 4D37FE16-0189-426C-8015-9F14DA3C52F6
keywords:
- バグ チェック 0x178 ELAM_DRIVER_DETECTED_FATAL_ERROR
- ELAM_DRIVER_DETECTED_FATAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ELAM_DRIVER_DETECTED_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c3e53dbbb71526fce1ea7ea7cba930ca4c82eac
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519900"
---
# <a name="bug-check-0x178-elamdriverdetectedfatalerror"></a>バグ チェック 0x178:ELAM\_ドライバー\_検出\_FATAL\_エラー


ELAM\_ドライバー\_検出\_FATAL\_エラーのバグ チェックが 0x00000178 の値を持ちます。 これは、ELAM ドライバーに致命的なエラーが検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="elamdriverdetectedfatalerror-parameters"></a>ELAM\_ドライバー\_検出\_FATAL\_エラー パラメーター


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
<td align="left">エラーの種類。
<p>0x0 :TPM 構成証明書が失効していない可能性があります。</p>
2 - ドライバーの BDCB_IMAGE_INFORMATION 構造体ポインター 3 - TBS_RESULT エラー コードを検査します。
<p>0x10000:ELAM ベンダー定義のエラー</p>
2 - (省略可能) ELAM ベンダー値 3 - (省略可能) ELAM ベンダー提供の値を指定します。</td>
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
<td align="left">(省略可能)ELAM ベンダーは、汎用データ ブロックを提供</td>
</tr>
</tbody>
</table>

 

 

 




