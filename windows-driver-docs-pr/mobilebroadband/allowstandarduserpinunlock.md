---
title: AllowStandardUserPinUnlock
description: AllowStandardUserPinUnlock
ms.assetid: 3fb6de78-662b-46d0-bf0c-9efde15b0861
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e60bc78d534ae988f8569a46bf3fa3ff6f6d2ff7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574439"
---
[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

> [!IMPORTANT]
> この要素は、Windows 10 バージョン 1507、以降は非推奨し、Windows の将来のバージョンではサポートされない可能性があります。

# <a name="allowstandarduserpinunlock"></a>AllowStandardUserPinUnlock


AllowStandardUserPinUnlock 要素では、暗証番号 (pin) のロック解除操作を実行する標準ユーザーが許可されている場合を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


```syntax
<AllowStandardUserPinUnlock>
  text
</ AllowStandardUserPinUnlock >
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


ブール値の where **true**により、標準ユーザーが暗証番号 (pin) を実行する操作のロックを解除と**false**はありません。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="networkconfiguration.md" data-raw-source="[NetworkConfiguration](networkconfiguration.md)">NetworkConfiguration</a></p></td>
<td><p>購入して、インターネットを指定するためのモバイル ブロード バンド プロファイルまたは標準ユーザーが暗証番号 (pin) を実行するかどうかの操作のロックを解除します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="AllowStandardUserPinUnlock" type="xs:boolean" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


AllowStandardUserPinUnlock 要素は省略可能です。

 

 





