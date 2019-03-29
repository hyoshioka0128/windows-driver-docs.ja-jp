---
title: ModelID
description: ModelID
ms.assetid: 6873f5b6-453e-4f8e-b534-0bc805865905
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66dace2065e2d9ee6c87c6720e028c2dd89f5dec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572870"
---
# <a name="modelid"></a>ModelID

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ModelID 要素には、物理デバイスの GUID を指定します。

**注意**   、 [ModelIDList](modelidlist.md) ModelID 要素は、サービス メタデータ パッケージのサポートされていません。 使用する必要があります、 [HardwareIDList](hardwareidlist.md)と[HardwareID](hardwareid.md)要素代わりにします。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<ModelID>
  text
</ModelID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


値として書式設定、 [GUIDType](guidtype-packageinfo.md) XML 単純型。

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
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a></p></td>
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a>要素は、デバイス メタデータ パッケージ内で指定されたデバイスでサポートされているハードウェア モデルごとの GUID を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


ModelID 要素には、デバイスでサポートされているハードウェアのモデルのモデル ID を指定します。 各モデルの ID は GUID を指定します。

**注意**   、 [ModelIDList](modelidlist.md) ModelID 要素は、サービス メタデータ パッケージのサポートされていません。 使用する必要があります、 [HardwareIDList](hardwareidlist.md)と[HardwareID](hardwareid.md)要素代わりにします。

 

モデル Id は、ビジネスの定義または物理デバイスの SKU に基づいています。 各モデルの ID は、すべての製造元とモデルの物理デバイスに一意である必要があります。

次の一覧には、ハードウェアと物理デバイスのモデル Id の違いについて説明します。

-   指定されたハードウェア Id、 [HardwareID](hardwareid.md)要素、bus 固有の値に基づくハードウェア関数を識別します。 ハードウェア Id では、デバイスのインスタンスにデバイス ドライバーをマッピングできます。 たとえば、同じハードウェア ID を持つ 2 つのデバイスは、同じドライバーによって使用される機能インターフェイスを共有します。

-   ModelID 要素で指定されたモデル Id には、バスまたはインターフェイスのテクノロジの独立した物理デバイスを一意に識別するには、OEM または独立系ハードウェア ベンダー (IHV) が有効にします。 たとえば、別のモデル Id を持つ 2 つのデバイスには、そのコンポーネントの同じハードウェア Id があります。

-   ハードウェア Id では、デバイス メタデータ パッケージを特定のバスまたはインターフェイス上のデバイスのインスタンスにマップします。

-   モデル Id は、デバイス メタデータ パッケージをコンピューターにデバイスを接続する方法に関係なく、物理デバイスにマップします。

 

 





