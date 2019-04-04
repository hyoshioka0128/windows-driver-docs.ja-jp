---
title: KsCallbackReturn rule ()
description: KsCallbackReturn ルールでは、カーネル ストリーミング (KS) ミニポート ドライバー コールバック関数が許可される状態値のみを返すことを指定します。
ms.assetid: 1779301C-5C2C-471F-88D8-3E5F2C90357D
ms.date: 05/21/2018
keywords:
- KsCallbackReturn rule ()
topic_type:
- apiref
api_name:
- KsCallbackReturn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f02bcdc1007a9434bca667fad3ea6c6f7af8baa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531283"
---
# <a name="kscallbackreturn-rule-"></a>KsCallbackReturn rule ()


KsCallbackReturn ルールでは、カーネル ストリーミング (KS) ミニポート ドライバー コールバック関数が許可される状態値のみを返すことを指定します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081005) |

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
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>関連項目
--------

[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)
[*AVStrMiniPinSetDeviceState*](https://msdn.microsoft.com/library/windows/hardware/ff556359)
[*AVStrMiniPinSetDataFormat*](https://msdn.microsoft.com/library/windows/hardware/ff556355)
 

 





