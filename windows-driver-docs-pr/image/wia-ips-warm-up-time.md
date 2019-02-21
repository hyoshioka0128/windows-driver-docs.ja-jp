---
title: WIA\_IP\_ウォーム\_を\_時間
description: WIA\_IP\_ウォーム\_を\_時のプロパティには、最大のウォーム アップ時間 (ミリ秒) で、スキャン操作を開始する前に必要なデバイスが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 081cdb91-d5d8-4458-9a78-72fcbb13c7da
keywords:
- WIA_IPS_WARM_UP_TIME イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_WARM_UP_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31c328a98905f5769e9881efa64da011d92088ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537325"
---
# <a name="wiaipswarmuptime"></a>WIA\_IP\_ウォーム\_を\_時間


WIA\_IP\_ウォーム\_を\_時のプロパティには、最大のウォーム アップ時間 (ミリ秒) で、スキャン操作を開始する前に必要なデバイスが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ips_warm_up_time_si"></span><span id="DDK_WIA_IPS_WARM_UP_TIME_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

アプリケーションは、WIA を読み取ることができます\_IP\_ウォーム\_を\_時のプロパティをデバイスの最大のウォーム アップ時間を決定します。 そうすると、アプリケーションでは、待機または一時停止には、何も発生する前に発生する可能性をユーザーに通知する「ウォーム アップするを待っている」ダイアログ ボックスが表示できます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





