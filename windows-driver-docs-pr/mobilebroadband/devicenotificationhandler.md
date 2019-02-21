---
title: DeviceNotificationHandler
description: DeviceNotificationHandler
ms.assetid: 04c4edb5-6dd1-4810-b23a-4f7ddc8af338
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b205e4e1cf09058c665ca8ea3a8c2446cabbc9df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553452"
---
# <a name="devicenotificationhandler"></a>DeviceNotificationHandler

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

DeviceNotificationHandler 要素には、デバイスの通知ハンドラーを指定します。 デバイスの通知ハンドラーを Microsoft Store アプリが実行されていない場合でも、モバイル ネットワーク オペレーター管理 SMS、USSD または通知などのイベントに応答コードを実行できます。 通知ハンドラーを実装する方法の詳細については、次を参照してください。、[モバイル オペレーター通知](https://go.microsoft.com/fwlink/?linkid=242062)ホワイト ペーパー。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<DeviceNotificationHandler EventID=”xs:string” EventAsset=”xs:string”/>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>イベント ID</p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p>デバイスの通知ハンドラーのイベント ID。</p></td>
</tr>
<tr class="even">
<td><p>EventAsset</p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p>デバイスの通知ハンドラーのイベントの資産。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="devicenotificationhandlers.md" data-raw-source="[DeviceNotificationHandlers](devicenotificationhandlers.md)">DeviceNotificationHandlers</a></p></td>
<td><p>デバイスの通知のハンドラーを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="DeviceNotificationHandler" type="tns:DeviceNotificationHandlerType" maxOccurs="unbounded" />

<xs:complexType name="DeviceNotificationHandlerType">
  <xs:attribute name="EventID" type="xs:string" use="required"/>
  <xs:attribute name="EventAsset" type="xs:string" use="required"/>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


-   DeviceNotificationHandler を指定すると、[アプリケーション](application-softwareinfo-schema.md)要素、システムはイベント ハンドラーを呼び出すし、デバイス状態の変更時にイベントを呼び出します。

-   **EventID**属性が SMS デバイス ケースの SMSEventHandler します。

-   **EventAsset**属性は Windows.BackgroundTasks の拡張機能として、アプリ マニフェストで指定した同じ値です。

DeviceNotificationHandler 要素は省略可能です。

 

 





