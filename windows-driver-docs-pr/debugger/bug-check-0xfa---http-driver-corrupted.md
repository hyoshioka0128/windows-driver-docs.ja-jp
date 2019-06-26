---
title: バグ チェック 0xFA HTTP_DRIVER_CORRUPTED
description: HTTP_DRIVER_CORRUPTED のバグ チェックでは、0x000000FA の値を持ちます。 これは、HTTP カーネル ドライバー (Http.sys) が破損した状態し、回復できないことを示します。
ms.assetid: f7e3c1bf-2259-4aa6-af19-267b537dedfe
keywords:
- バグ チェック 0xFA HTTP_DRIVER_CORRUPTED
- HTTP_DRIVER_CORRUPTED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- HTTP_DRIVER_CORRUPTED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8ad79360e94385965c31beb630906bb57f6612a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367040"
---
# <a name="bug-check-0xfa-httpdrivercorrupted"></a>バグ チェック 0xFA:HTTP\_ドライバー\_破損しました。


HTTP\_ドライバー\_破損したバグ チェックが 0x000000FA の値を持ちます。 これは、HTTP カーネル ドライバー (Http.sys) が破損した状態し、回復できないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="httpdrivercorrupted-parameters"></a>HTTP\_ドライバー\_破損したパラメーター


パラメーター 1 では、HTTP カーネル ドライバーの正確な状態を識別します。

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
<td align="left"><p>0x1</p></td>
<td align="left"><p>作業項目のアドレス</p></td>
<td align="left"><p>作業項目のチェックを含むファイルの名前</p></td>
<td align="left"><p>ファイル内で作業項目のチェックの行番号</p></td>
<td align="left"><p>作業項目が無効です。 これは最終的にスレッド プールの破損やアクセス違反が発生します。</p></td>
</tr>
</tbody>
</table>

 

 

 




