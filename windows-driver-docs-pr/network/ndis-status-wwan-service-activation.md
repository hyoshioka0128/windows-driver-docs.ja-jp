---
title: NDIS_STATUS_WWAN_SERVICE_ACTIVATION
description: ミニポート ドライバーでは、OID_WWAN_SERVICE_ACTIVATION の OID セットの要求に応答する NDIS_STATUS_WWAN_SERVICE_ACTIVATION 通知を使用します。
ms.assetid: c5700759-b903-4564-a8b8-c49140d2acd3
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_SERVICE_ACTIVATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9429f62e9c7d16de1f983d603e105e4c603786f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528234"
---
# <a name="ndisstatuswwanserviceactivation"></a>NDIS\_状態\_WWAN\_サービス\_アクティブ化


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_サービス\_OID に応答するアクティブ化通知設定の要求[OID\_WWAN\_サービス\_アクティベーション](oid-wwan-service-activation.md)します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知は、NDIS\_WWAN\_サービス\_アクティベーション\_ステータス構造体。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーの OID セット要求への応答でサービスのアクティブ化の状態を返す必要があります[OID\_WWAN\_サービス\_アクティベーション](oid-wwan-service-activation.md)します。

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

 

 




