---
title: KSEVENT\_PINCAPS\_段落
description: KSEVENT\_PINCAPS\_オーディオ デバイスのオーディオ データ形式が変更されたこと、オーディオ スタックに段落のイベントを示します。
ms.assetid: ca9ee246-7fca-42df-89e0-7ace6b1f808a
keywords:
- KSEVENT_PINCAPS_FORMATCHANGE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSEVENT_PINCAPS_FORMATCHANGE
api_location:
- Ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e48cadb86e5767cbd91ab57dbf2c7c812b16d060
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391529"
---
# <a name="kseventpincapsformatchange"></a>KSEVENT\_PINCAPS\_段落


`KSEVENT_PINCAPS_FORMATCHANGE`イベント オーディオ デバイスのオーディオ データ形式が変更されたことをオーディオ スタックを示します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespan-usage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span> 使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">対象</th>
<th align="left">イベント記述子の種類</th>
<th align="left">イベント値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

イベント値の型 (データの操作) は、 **KSEVENTDATA**をこのイベントに使用する通知方法を指定します。

<a name="remarks"></a>注釈
-------

オーディオ ポート、ドライバーを呼び出すと、 [ **EventHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nc-portcls-pcpfnevent_handler) 、ミニポート ドライバーのルーチンを渡す、 [ **PCEVENT\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-_pcevent_request)構造体。 この構造体にはへのポインターが含まれています、 [ **PCEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcevent_item)フィルター、pin、またはノードでサポートされているイベントについて説明するために使用する構造体。

そのため、たとえば、ドライバーをサポートする、`KSEVENT_PINCAPS_FORMATCHANGE`イベントを設定する必要があります、 **PCEVENT\_項目**次のように構造体します。

```cpp
static PCEVENT_ITEM FormatChangePinEvent[] = {
  {
    &KSEVENTSETID_PinCapsChange,
    KSEVENT_PINCAPS_FORMATCHANGE,
    KSEVENT_TYPE_ENABLE | KSEVENT_TYPE_BASICSUPPORT,
    MyEventHandler
  }
};
```

上記のコード例で MyEventHandler カスタム イベント ハンドラーを監視する必要があります、`KSEVENT_PINCAPS_FORMATCHANGE`イベント Portcls に登録と KSEVENT\_PINCAPS\_段落がトリガーされます。 ミニポート ドライバーを呼び出す必要があります、 [ **IPortEvents::AddEventToEventList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportevents-addeventtoeventlist)イベントを登録するメソッド。

ポート ドライバーを呼び出し、pin、ノード、接続およびミニポート ドライバーでサポートされるプロパティの説明を取得するには、するには、 [ **IMiniport::GetDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-getdescription)メソッド。 このメソッドの呼び出しを返します、 [ **PCFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcfilter_descriptor) 、automation のテーブルを指す構造体 ([**PCAUTOMATION\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcautomation_table)). **PCAUTOMATION\_テーブル**構造体が、**イベント**メンバー。 このメンバーは、ミニポート ドライバーがサポートするフィルターに関連付けられているイベントの配列を指します。 設定する必要があります、**イベント**メンバーを含むイベントの配列を指す、 **PCEVENT\_項目**用の構造、`KSEVENT_PINCAPS_FORMATCHANGE`イベント。

呼び出す必要がありますが、ミニポート ドライバーでは、動的形式の変更を検出すると、 [ **IPortEvents::GenerateEventList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportevents-generateeventlist)を通知するメソッド、`KSEVENT_PINCAPS_FORMATCHANGE`イベント。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**EventHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nc-portcls-pcpfnevent_handler)

[**IMiniport::GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-getdescription)

[**IPortEvents::AddEventToEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportevents-addeventtoeventlist)

[**IPortEvents::GenerateEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportevents-generateeventlist)

[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)

[**PCAUTOMATION\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcautomation_table)

[**PCEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcevent_item)

[**PCEVENT\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-_pcevent_request)

[**PCFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcfilter_descriptor)

 

 






