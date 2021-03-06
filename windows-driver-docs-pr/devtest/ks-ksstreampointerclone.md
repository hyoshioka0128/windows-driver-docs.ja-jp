---
title: KsStreamPointerClone ルール)
description: KsStreamPointerClone ルールでは、カーネル ストリーム (KS) ミニポート ドライバーが正しく KsStreamPointerClone と KsStreamPointerDelete 関数を使用しているを指定します。
ms.assetid: 5ECF0070-0E36-4A91-B9FA-AA0DB7636B0E
ms.date: 05/21/2018
keywords:
- KsStreamPointerClone ルール)
topic_type:
- apiref
api_name:
- KsStreamPointerClone
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5036831a5be2e766e295711a572f281c83196331
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392742"
---
# <a name="ksstreampointerclone-rule-"></a>KsStreamPointerClone ルール)


KsStreamPointerClone ルールでは、カーネル ストリーム (KS) ミニポート ドライバーが正しく使用を指定します、 [ **KsStreamPointerClone** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)と[ **KsStreamPointerDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)関数。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00081002) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>このルールを確認するには、コマンド プロンプト ウィンドウを開きます。 Driver Verifier のコマンドを入力し、指定<strong>/domain ks</strong>します。</p>
<p>次に、例を示します。</p>
<p><strong>verifier /domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





