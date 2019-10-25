---
title: KSEVENT\_PINCAPS\_FORMATCHANGE
description: KSEVENT\_PINCAPS\_FORMATCHANGE イベントは、オーディオデバイスのオーディオデータ形式が変更されたことをオーディオスタックに示します。
ms.assetid: ca9ee246-7fca-42df-89e0-7ace6b1f808a
keywords:
- KSEVENT_PINCAPS_FORMATCHANGE オーディオデバイス
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
ms.openlocfilehash: 2cb5a4119f2ebcf9ba08a9b90b5d3a77c1491d29
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833146"
---
# <a name="ksevent_pincaps_formatchange"></a>KSEVENT\_PINCAPS\_FORMATCHANGE


`KSEVENT_PINCAPS_FORMATCHANGE` イベントは、オーディオデバイスのオーディオデータ形式が変更されたことをオーディオスタックに示します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespan-usage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">イベント値の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

イベント値の種類 (操作データ) は、このイベントに使用する通知方法を指定する**KSEVENTDATA**構造体です。

<a name="remarks"></a>注釈
-------

オーディオポートドライバーは、そのミニポートドライバーの[**EventHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nc-portcls-pcpfnevent_handler)ルーチンを呼び出すと、 [**PCEVENT\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request)構造体を渡します。 この構造体には、フィルター、ピン、またはノードでサポートされるイベントを記述するために使用される[**Pcevent\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item)構造体へのポインターが含まれています。

そのため、たとえば、`KSEVENT_PINCAPS_FORMATCHANGE` イベントをサポートするドライバーは、次のように**Pcevent\_項目**構造を設定する必要があります。

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

前のコード例では、MyEventHandler カスタムイベントハンドラーは、KSEVENT\_PINCAPS\_FORMATCHANGE がトリガーされたときに、`KSEVENT_PINCAPS_FORMATCHANGE` イベントを監視し、Portcls に登録する必要があります。 ミニポートドライバーは、 [**Iportevents:: AddEventToEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-addeventtoeventlist)メソッドを呼び出して、イベントを登録する必要があります。

ミニポートドライバーでサポートされているピン、ノード、接続、およびプロパティの説明を取得するために、ポートドライバーは[**IMiniport:: GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)メソッドを呼び出します。 このメソッド呼び出しは、オートメーションテーブル ([**Pcfilter\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcautomation_table)) を指す[**PCFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)構造体を返します。 **Pcautomation\_テーブル**構造には、 **Events**メンバーがあります。 このメンバーは、ミニポートドライバーがサポートするフィルターに関連付けられているイベントの配列を指します。 その**ため、イベントメンバーを**、`KSEVENT_PINCAPS_FORMATCHANGE` イベントの**PCEVENT\_項目**構造を含むイベント配列を指すように設定する必要があります。

ミニポートドライバーで動的な形式の変更が検出された場合は、 [**Iportevents:: GenerateEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-generateeventlist)メソッドを呼び出して、`KSEVENT_PINCAPS_FORMATCHANGE` イベントを通知する必要があります。

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
<td align="left"><p>Windows 7 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nc-portcls-pcpfnevent_handler)

[**IMiniport:: GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)

[**IPortEvents:: AddEventToEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-addeventtoeventlist)

[**IPortEvents:: GenerateEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-generateeventlist)

[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**PCAUTOMATION\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcautomation_table)

[**PCEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item)

[**PCEVENT\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request)

[**PCFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)

 

 






