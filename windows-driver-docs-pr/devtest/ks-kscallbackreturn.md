---
title: KsCallbackReturn ルール ()
description: KsCallbackReturn ルールは、カーネルストリーミング (KS) ミニポートドライバーのコールバック関数が、許可されている状態値のみを返すことを指定します。
ms.assetid: 1779301C-5C2C-471F-88D8-3E5F2C90357D
ms.date: 05/21/2018
keywords:
- KsCallbackReturn ルール ()
topic_type:
- apiref
api_name:
- KsCallbackReturn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73d227ef69922a23a17c7ce6d9b47b0f8f0eca56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839426"
---
# <a name="kscallbackreturn-rule-"></a>KsCallbackReturn ルール ()


KsCallbackReturn ルールは、カーネルストリーミング (KS) ミニポートドライバーのコールバック関数が、許可されている状態値のみを返すことを指定します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00081005) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>この規則を確認するには、コマンドプロンプトウィンドウを開きます。 ドライバー検証ツールコマンドを入力し、「 <strong>/domain ks</strong>」と指定します。</p>
<p>次に、例を示します。</p>
<p><strong>verifier/domain ks</strong> [<em>オプション</em>] <strong>/driver</strong> <em>&lt;ドライバー&gt;</em></p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>関連項目
--------

[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)
[*Avstrminipinsetdevicestate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)
[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)
 

 





