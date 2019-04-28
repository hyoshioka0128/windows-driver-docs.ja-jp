---
title: WIA\_DPS\_デバイス\_ID
description: WIA\_DPS\_デバイス\_web サービス スキャナーのデバイスの ID プロパティに関数のインスタンスの一意の識別子が含まれます。
ms.assetid: 48c45b94-86b1-41b5-89bc-e3270ad56d7e
keywords:
- WIA_DPS_DEVICE_ID イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_DEVICE_ID
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dd5c51d593d8fcf3604b9d1fdfe2c3cf5c96778
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382276"
---
# <a name="wiadpsdeviceid"></a>WIA\_DPS\_デバイス\_ID


WIA\_DPS\_デバイス\_web サービス スキャナーのデバイスの ID プロパティに関数のインスタンスの一意の識別子が含まれます。 この識別子は、WIA ミニドライバーと通信しているスキャナー デバイス上の web サービスを表します。 この識別子の形式に関する仮定は行われません。 WIA ミニドライバーは、作成し、このプロパティを保持します。

WIA アプリケーションは、WIA の値を使用できる\_DPS\_デバイス\_関数検出 API、WIA の現在のセッションで使用する web サービス スキャナーのデバイスを表す関数インスタンス オブジェクトを使用して見つけるには、ID。

プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

WIA ミニドライバーの鍵を読み取ることによって実行時にこのプロパティを初期化します\_PNPX\_関数インスタンスのオブジェクトからのデバイス プロパティの ID。

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


[**WIA\_DPS\_GLOBAL\_の ID**](wia-dps-global-identity.md)

[**WIA\_DPS\_サービス\_ID**](wia-dps-service-id.md)

 

 






