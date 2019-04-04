---
title: 一般的な属性
description: 一般的な属性
ms.assetid: c48fabff-0580-478f-b423-d959815bbeb4
keywords:
- プリンターの WDK Unidrv、一般的な属性します。
- 一般的なプリンターの WDK Unidrv 属性します。
- 一般的なプリンターに関する一般的なプリンターの属性の WDK Unidrv の属性します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e2afe6c70846e5b0fc39cf551e277832391d7a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570327"
---
# <a name="general-attributes"></a>一般的な属性





*一般的な属性*のいずれかを表す、[属性型](attribute-types.md)GPD 言語によって定義されています。 一般的な属性は、特定の機能またはオプションに関連付けられていません。 一般的な属性は、次のグループに分類されます。

[ルート レベルのみの属性](root-level-only-attributes.md)

[一般的な印刷属性](general-printing-attributes.md)

[テキスト印刷属性](text-printing-attributes.md)

[ラスター印刷属性](raster-printing-attributes.md)

[印刷属性のベクター](vector-printing-attributes.md)

ルート レベルで GPD ファイル内のすべての一般的な属性の配置は、通常、(つまり、かっこ内にありません)。 ルート レベルのみの属性は、ルート レベルで常に配置する必要があります。

場合によっては、(ルート レベルのみ属性) を除くの一般的な属性の値は、構成パラメーターに依存します。 内でこのような場合は、属性エントリを配置する場合があります、 \*Option ステートメント、または内で、 [\*ケース](conditional-statements.md)ステートメント (ルート レベルであるかに含まれている、\*ステートメントのオプション)。 ルート レベルで属性がない場合 (に含まれているため、\*ステートメントのオプションは、ルート レベルのため、または\*Case ステートメント)、属性名は、EXTERN によってプレフィックス指定する必要があります\_グローバル シンボル、次のように:

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>EXTERN_GLOBAL: *<em>AttributeName</em>:<em>AttributeValue</em></p></td>
</tr>
</tbody>
</table>

 

構成の依存関係を指定する方法については、[条件付きステートメント](conditional-statements.md)を参照してください。

 

 




