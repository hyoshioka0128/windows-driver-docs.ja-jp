---
title: WIA\_DPC\_POWER\_モード
description: WIA\_DPC\_POWER\_モード プロパティは、カメラ デバイスの現在の電源を定義します。
ms.assetid: b99d9ebc-6a1f-4bfc-be3a-07dba5b38186
keywords:
- WIA_DPC_POWER_MODE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_POWER_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71a09fae56d34b7259a6fc8a423c7adfe32d7606
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570650"
---
# <a name="wiadpcpowermode"></a>WIA\_DPC\_POWER\_モード


WIA\_DPC\_POWER\_モード プロパティは、カメラ デバイスの現在の電源を定義します。

## <span id="ddk_wia_dpc_power_mode_si"></span><span id="DDK_WIA_DPC_POWER_MODE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用です。

<a name="remarks"></a>コメント
-------

アプリケーションは、WIA を読み取ります\_DPC\_POWER\_ソース、カメラの電源を判断する MODE プロパティを使用します。

次の表に、WIA で有効な定数\_DPC\_POWER\_モード。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>POWERMODE_BATTERY</p></td>
<td><p>カメラ デバイスがバッテリ電源で動作します。</p></td>
</tr>
<tr class="even">
<td><p>POWERMODE_LINE</p></td>
<td><p>カメラ デバイス電源アダプターで動作しています。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のオペレーティング システムで古いものであり使用できなくする必要があります。 ただし、アプリケーションやデバイス向けの Windows Server 2003、Windows XP、および Windows の以前のバージョンと互換性のこのプロパティが現在も Windows Vista で定義します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





