---
title: NDIS_STATUS_WWAN_RADIO_STATE
description: ミニポート ドライバー NDIS_STATUS_WWAN_RADIO_STATE 通知ハードウェア無線電源、または OID クエリへの応答で、デバイスのソフトウェア ベースの無線電源状態の変更を変更したときに MB サービスに通知を使用するか、OID_WWAN_RADIO_ の要求の設定状態。 ミニポート ドライバーには、この通知が不要なイベントを送信できます。この通知は、NDIS_WWAN_RADIO_STATE 構造体を使用します。
ms.assetid: 77c10b2a-ab43-4349-947a-e89c7af27f68
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_RADIO_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ef21fbf6deb6098db76301ec423e20596e4c0852
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377585"
---
# <a name="ndisstatuswwanradiostate"></a>NDIS\_状態\_WWAN\_ラジオ\_状態


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_ラジオ\_ユーザーがハードウェア無線電源を変更またはデバイスのソフトウェア ベースの無線電源状態の変更で、MB サービスに通知する状態の通知OID クエリへの応答のセットの要求または[OID\_WWAN\_ラジオ\_状態](oid-wwan-radio-state.md)します。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)構造体。

<a name="remarks"></a>注釈
-------

クエリ要求に応答のミニポート ドライバーが両方の現在のハードウェアおよびソフトウェア ベースの無線電源状態を返す必要があります。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)

[OID\_WWAN\_ラジオ\_状態](oid-wwan-radio-state.md)

 

 




