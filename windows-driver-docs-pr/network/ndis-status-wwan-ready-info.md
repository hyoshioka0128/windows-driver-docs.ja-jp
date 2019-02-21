---
title: NDIS_STATUS_WWAN_READY_INFO
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_READY_INFO 通知を使用して、OID_WWAN_READY_INFO に対応のデバイスの準備完了状態の変更点の MB サービスに通知 \ 160; クエリ要求。
ms.assetid: 92ddf95f-8829-4259-b53a-c7ce56ee53f0
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_READY_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cb93eb3d2b2974d7fabe9a40c50ae90c237c609e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528810"
---
# <a name="ndisstatuswwanreadyinfo"></a>NDIS\_状態\_WWAN\_準備\_情報


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_準備\_MB のサービスへの応答でのデバイスの準備完了状態の変更の通知に情報通知[OID\_WWAN\_準備ができて\_情報](oid-wwan-ready-info.md) 要求のクエリを実行します。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_準備\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567916)構造体。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーでは、要請していないイベントとしてすべてのデバイスの準備完了状態の変更を報告する必要があります。 ミニポート ドライバーで、WWAN を設定する必要があります、ミニポート ドライバー MB デバイスの初期化時\_準備\_情報**ReadyState**メンバー **WwanReadyStateOff**します。 その後、ミニポート ドライバーでは、この通知による MB サービスに、デバイスの準備完了状態の変更を報告する必要があります。 たとえば、ミニポート ドライバーがデバイスの準備完了状態を報告する必要がありますを変更するときに、 **ReadyState**メンバーから変更**WwanReadyStateOff**に**WwanReadyStateDeviceLocked**、または**WwanReadyStateBadSim**、または**WwanReadyStateSimNotInserted**、またはその他のさまざまなデバイスの準備完了の状態。

ほとんどのデバイスの準備完了状態の変更は、デバイスの初期化、ラジオ スタックおよび SIM カード (必要な場合) ときに発生します。 変更も MB サービスとユーザーが、SIM カードの変更など、ミニポート ドライバーとのセッションの実行中に発生します。 新しいデバイスの準備完了の状態に基づいて適切 MB サービスの動作を変更するものとします。

<a name="requirements"></a>要件
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


[**NDIS\_WWAN\_準備\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567916)

[OID\_WWAN\_準備\_情報](oid-wwan-ready-info.md)

 

 




