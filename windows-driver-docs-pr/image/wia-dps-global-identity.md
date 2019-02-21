---
title: WIA\_DPS\_GLOBAL\_の ID
description: WIA\_DPS\_GLOBAL\_ID プロパティには、web サービス スキャナー デバイスの SOAP アドレスが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 4ee25eb9-eb5b-43b2-8b35-7bc8ac45c90a
keywords:
- WIA_DPS_GLOBAL_IDENTITY イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_GLOBAL_IDENTITY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f32d8d372575835b8084f3ff61d6993538e952d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559460"
---
# <a name="wiadpsglobalidentity"></a>WIA\_DPS\_GLOBAL\_の ID


WIA\_DPS\_GLOBAL\_ID プロパティには、web サービス スキャナー デバイスの SOAP アドレスが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

WIA ミニドライバーの鍵を読み取ることによって実行時にこのプロパティを初期化します\_PNPX\_関数インスタンスのオブジェクトから GlobalIdentity デバイス プロパティ。

両方の鍵\_PNPX\_GlobalIdentity と鍵\_PNPX\_ID は、UPnP デバイスの一意の ID を含めることができます。 違いは、その鍵\_PNPX\_GlobalIdentity は常に鍵の中に、すべての関数インスタンスのルート デバイスの UUID を含む\_PNPX\_ID にはデバイス/サブ Device の UUID が含まれている関数インスタンスを表します。

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

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_デバイス\_ID**](wia-dps-device-id.md)

[**WIA\_DPS\_サービス\_ID**](wia-dps-service-id.md)

 

 






