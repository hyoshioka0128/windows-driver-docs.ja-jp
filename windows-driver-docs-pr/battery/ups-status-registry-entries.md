---
title: UPS 状態レジストリ エントリ
description: UPS ミニドライバーは、特定の UPS 状態レジストリ エントリを設定する必要があります。
ms.assetid: c24ef185-ba8d-4cfd-9d33-b70682905f00
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 874a732c925e8663acd04de22c970860f8dba5f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328422"
---
# <a name="upsstatus-registry-entries"></a>UPS\\レジストリ エントリの状態


## <span id="ddk_ups_status_registry_entries_kg"></span><span id="DDK_UPS_STATUS_REGISTRY_ENTRIES_KG"></span>


次のレジストリ エントリで、 **UPS**\\**状態**キー、UPS ミニドライバーを設定する必要があります。

### <a name="span-idbatterycapacityspanspan-idbatterycapacityspanspan-idbatterycapacityspanbatterycapacity"></a><span id="BatteryCapacity"></span><span id="batterycapacity"></span><span id="BATTERYCAPACITY"></span>BatteryCapacity

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>値の名前  
**BatteryCapacity**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>値の型  
REG\_DWORD

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>値  
UPS バッテリ残量の割合。 この割合は 0 ~ 100 の範囲内の値として表されます。 (表示される値は、最も近い整数に丸められます)。

<span id="Default_Value"></span><span id="default_value"></span><span id="DEFAULT_VALUE"></span>既定値  
0

### <a name="span-idbatterystatusspanspan-idbatterystatusspanspan-idbatterystatusspanbatterystatus"></a><span id="BatteryStatus"></span><span id="batterystatus"></span><span id="BATTERYSTATUS"></span>BatteryStatus

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>値の名前  
**BatteryStatus**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>値の型  
REG\_DWORD

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>値  
UPS バッテリの現在の状態。 値は、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>バッテリの状態が不明です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>バッテリは、[ok] です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>バッテリを交換する必要があります。</p></td>
</tr>
</tbody>
</table>

 

<span id="Default_Value"></span><span id="default_value"></span><span id="DEFAULT_VALUE"></span>既定値  
0

### <a name="span-idcommstatusspanspan-idcommstatusspanspan-idcommstatusspancommstatus"></a><span id="CommStatus"></span><span id="commstatus"></span><span id="COMMSTATUS"></span>CommStatus

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>値の名前  
**CommStatus**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>値の型  
REG\_DWORD

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>値  
UPS への通信パスの状態です。 値は、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>UPS への通信パスは不明です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>UPS への通信パスは、[ok] です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>UPS への通信パスが失われました。</p></td>
</tr>
</tbody>
</table>

 

<span id="Default_Value"></span><span id="default_value"></span><span id="DEFAULT_VALUE"></span>既定値  
1

### <a name="span-idfirmwarerevspanspan-idfirmwarerevspanspan-idfirmwarerevspanfirmwarerev"></a><span id="FirmwareRev"></span><span id="firmwarerev"></span><span id="FIRMWAREREV"></span>FirmwareRev

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>値の名前  
**FirmwareRev**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>値の型  
REG\_SZ

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>値  
表示可能な文字列として UPS ファームウェアのリビジョンを報告します。

<span id="Default_Value_"></span><span id="default_value_"></span><span id="DEFAULT_VALUE_"></span>既定値:  
""

### <a name="span-idserialnumberspanspan-idserialnumberspanspan-idserialnumberspanserialnumber"></a><span id="SerialNumber"></span><span id="serialnumber"></span><span id="SERIALNUMBER"></span>シリアル番号

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>値の名前  
**シリアル番号**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>値の型  
REG\_SZ

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>値  
UPS のシリアル番号が表示可能な文字列であることを報告します。

<span id="Default_Value_"></span><span id="default_value_"></span><span id="DEFAULT_VALUE_"></span>既定値:  
""

### <a name="span-idtotalupsruntimespanspan-idtotalupsruntimespanspan-idtotalupsruntimespantotalupsruntime"></a><span id="TotalUPSRuntime"></span><span id="totalupsruntime"></span><span id="TOTALUPSRUNTIME"></span>TotalUPSRuntime

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>値の名前  
**TotalUPSRuntime**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>値の型  
REG\_DWORD

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>値  
分単位での実行時に、残りの UPS の量。

<span id="Default_Value"></span><span id="default_value"></span><span id="DEFAULT_VALUE"></span>既定値  
0

### <a name="span-idutilitypowerstatusspanspan-idutilitypowerstatusspanspan-idutilitypowerstatusspanutilitypowerstatus"></a><span id="UtilityPowerStatus"></span><span id="utilitypowerstatus"></span><span id="UTILITYPOWERSTATUS"></span>UtilityPowerStatus

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>値の名前  
**UtilityPowerStatus**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>値の型  
REG\_DWORD

<span id="Value_"></span><span id="value_"></span><span id="VALUE_"></span>値:  
UPS に供給する電源の状態を報告します。 値は、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>ユーティリティが提供する電源の状態が不明です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>電源の供給は問題ありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>電源障害が発生しました。</p></td>
</tr>
</tbody>
</table>

 

<span id="Default_Value"></span><span id="default_value"></span><span id="DEFAULT_VALUE"></span>既定値  
0

 

 




