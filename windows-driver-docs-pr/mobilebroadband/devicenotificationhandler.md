---
title: DeviceNotificationHandler
description: DeviceNotificationHandler
ms.assetid: 04c4edb5-6dd1-4810-b23a-4f7ddc8af338
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b205e4e1cf09058c665ca8ea3a8c2446cabbc9df
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323619"
---
# <a name="devicenotificationhandler"></a>DeviceNotificationHandler

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

DeviceNotificationHandler 要素は、デバイス通知ハンドラーを指定します。 デバイス通知ハンドラーを使用すると、Microsoft Store アプリが実行されていない場合でも、モバイルネットワークオペレーター管理 SMS や USSD 通知などのイベントに応答してコードを実行できます。 通知ハンドラーの実装の詳細については、「[モバイルオペレーター通知](https://go.microsoft.com/fwlink/?linkid=242062)」ホワイトペーパーを参照してください。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<DeviceNotificationHandler EventID=”xs:string” EventAsset=”xs:string”/>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>タスクバーの検索ボックスに</th>
<th>必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>イベント ID</p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p>デバイス通知ハンドラーのイベント ID。</p></td>
</tr>
<tr class="even">
<td><p>EventAsset</p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p>デバイス通知ハンドラーのイベントアセット。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="devicenotificationhandlers.md" data-raw-source="[DeviceNotificationHandlers](devicenotificationhandlers.md)">DeviceNotificationHandlers</a></p></td>
<td><p>デバイス通知ハンドラーを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="DeviceNotificationHandler" type="tns:DeviceNotificationHandlerType" maxOccurs="unbounded" />

<xs:complexType name="DeviceNotificationHandlerType">
  <xs:attribute name="EventID" type="xs:string" use="required"/>
  <xs:attribute name="EventAsset" type="xs:string" use="required"/>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   [アプリケーション](application-softwareinfo-schema.md)要素で DeviceNotificationHandler を指定すると、システムはイベントハンドラーを呼び出し、デバイスが状態に変化したときにイベントを呼び出します。

-   **EventID**属性は、SMS デバイスケースの SMSEventHandler です。

-   **Eventasset**属性は、アプリケーションマニフェストで、Windows の backgroundtasks の拡張機能として指定した値と同じです。

DeviceNotificationHandler 要素は省略可能です。

 

 





