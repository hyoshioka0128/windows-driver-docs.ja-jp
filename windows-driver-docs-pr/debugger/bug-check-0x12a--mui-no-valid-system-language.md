---
title: バグ チェック 0x12A MUI_NO_VALID_SYSTEM_LANGUAGE
description: MUI_NO_VALID_SYSTEM_LANGUAGE のバグ チェックでは、0x0000012A の値を持ちます。 これは、Windows がシステムの既定の UI 言語ので、インストール、ライセンスされた言語パックを見つかりませんでした。 ことを示します。
ms.assetid: 6424FC7D-BD39-4F35-9E72-E9730D27CC24
keywords:
- バグ チェック 0x12A MUI_NO_VALID_SYSTEM_LANGUAGE
- MUI_NO_VALID_SYSTEM_LANGUAGE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUI_NO_VALID_SYSTEM_LANGUAGE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 623c62f14fcd08777b7be6b2f9dc1d3c5fc10d0c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550714"
---
# <a name="bug-check-0x12a-muinovalidsystemlanguage"></a>バグ チェック 0x12A の。MUI\_いいえ\_有効\_システム\_言語


MUI\_いいえ\_有効\_システム\_言語のバグ チェックが 0x0000012A の値を持ちます。 これは、Windows がシステムの既定の UI 言語ので、インストール、ライセンスされた言語パックを見つかりませんでした。 ことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="muinovalidsystemlanguage-parameters"></a>MUI\_いいえ\_有効\_システム\_言語パラメーター


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
<td align="left">バグチェックのサブタイプ
<p>0x1:Windows が見つかりませんでした、インストールされている言語パック フェーズ中には初期化します。</p>
パラメーター 2 - NT 状態コード エラーの理由を説明します。
<p>0x2:Windows 見つかりませんでした。 インストール、ライセンスされた言語パックも既定のシステム UI 言語カーネル キャッシュの作成中にします。</p>
パラメーター 2 - NT 状態コード エラーの理由を説明します。
.</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">予約済み</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

 

 




