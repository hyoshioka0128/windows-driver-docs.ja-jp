---
title: ModelID
description: ModelID
ms.assetid: 6873f5b6-453e-4f8e-b534-0bc805865905
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66dace2065e2d9ee6c87c6720e028c2dd89f5dec
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750041"
---
# <a name="modelid"></a>ModelID

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ModelID 要素は、物理デバイスの GUID を指定します。

注意   [modelidlist](modelidlist.md)要素と modelid 要素は、サービスメタデータパッケージではサポートされていません。 代わりに、[ハードウェア Id リスト](hardwareidlist.md)と[HardwareID](hardwareid.md)要素を使用する必要があります。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<ModelID>
  text
</ModelID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


[Guidtype](guidtype-packageinfo.md) XML 単純型として書式設定された値。

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
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a></p></td>
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">Modelidlist</a>要素は、デバイスメタデータパッケージ内で指定されたデバイスでサポートされている各ハードウェアモデルの GUID を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


ModelID 要素は、デバイスでサポートされているハードウェアモデルのモデル ID を指定します。 各モデル ID は、GUID によって指定されます。

注意   [modelidlist](modelidlist.md)要素と modelid 要素は、サービスメタデータパッケージではサポートされていません。 代わりに、[ハードウェア Id リスト](hardwareidlist.md)と[HardwareID](hardwareid.md)要素を使用する必要があります。

 

モデル Id は、物理デバイスのビジネス定義または SKU に基づいています。 各モデル ID は、物理デバイスのすべてのモデルとモデルで一意である必要があります。

次の一覧では、物理デバイスのハードウェア Id とモデル Id の違いについて説明します。

-   [HardwareID](hardwareid.md)要素によって指定されたハードウェア id は、バス固有の値に基づいてハードウェアの機能を識別します。 ハードウェア Id は、デバイスドライバーをデバイスインスタンスにマップすることができます。 たとえば、同じハードウェア ID を持つ2つのデバイスは、同じドライバーで使用される機能インターフェイスを共有します。

-   ModelID 要素によって指定されたモデル Id では、OEM または独立系ハードウェアベンダー (IHV) が、バスやインターフェイスのテクノロジに依存しない物理デバイスを一意に識別できるようにします。 たとえば、異なるモデル Id を持つ2つのデバイスは、そのコンポーネントに対して同じハードウェア Id を持つことができます。

-   ハードウェア Id は、デバイスメタデータパッケージを特定のバスまたはインターフェイスのデバイスインスタンスにマップします。

-   モデル Id は、デバイスがコンピューターに接続されているかどうかに関係なく、デバイスメタデータパッケージを物理デバイスにマップします。

 

 





