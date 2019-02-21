---
title: C28161
description: 浮動小数点演算ハードウェアを使用する権利を取得しなくても C28161 の終了を警告します。
ms.assetid: 4132409d-10aa-4014-a2d9-77c62e137795
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28161
ms.openlocfilehash: 4e0dcc8479f32f2a66301c67047e9ce03d0dc324
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548565"
---
# <a name="c28161"></a>C28161


C28161 を警告します。浮動小数点演算ハードウェアを使用する権限を取得せずに終了します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>この関数は、使用可能な浮動小数点で終了する注釈が付けられています。</p></td>
</tr>
</tbody>
</table>

 

**\_カーネル\_float\_保存\_** 注釈は、浮動小数点数を使用する権利の取得に使用されたが、既知を実行する機能はありませんが、関数内のパスが検出されました操作が正常に呼び出されます。 この警告になっているため、条件文 (**\_とき\_**) 注釈が必要なまたはコード エラーを示す可能性があります。

 

 





