---
title: AllowStandardUserPinUnlock
description: AllowStandardUserPinUnlock
ms.assetid: 3fb6de78-662b-46d0-bf0c-9efde15b0861
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cc86418798a74818008867cd11837c7cb340566
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235303"
---
# <a name="allowstandarduserpinunlock"></a>AllowStandardUserPinUnlock

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

> [!IMPORTANT]
> Windows 10 バージョン1507以降では、この要素は非推奨とされており、今後のバージョンの Windows ではサポートされない可能性があります。

AllowStandardUserPinUnlock 要素は、標準ユーザーが PIN のロック解除操作を実行できるかどうかを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


```syntax
<AllowStandardUserPinUnlock>
  text
</ AllowStandardUserPinUnlock >
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


ブール値。 **true**の場合、標準ユーザーは PIN のロック解除操作を実行でき、 **false**の場合は無効になります。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


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
<td><p>使用する購入およびインターネットのモバイルブロードバンドプロファイルを指定します。または、標準ユーザーが PIN のロック解除操作を実行できるかどうかを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="AllowStandardUserPinUnlock" type="xs:boolean" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


AllowStandardUserPinUnlock 要素は省略可能です。

 

 





