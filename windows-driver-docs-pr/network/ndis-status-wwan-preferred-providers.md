---
title: NDIS_STATUS_WWAN_PREFERRED_PROVIDERS
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_PREFERRED_PROVIDERS 通知を使用して、優先プロバイダー一覧 (PPL) に変更された MB サービスに通知します。
ms.assetid: b0c06db9-82ca-4f94-80e6-3cf13197abf5
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_PREFERRED_PROVIDERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 089a08a8b4de53142a90d5b4e5992bbbe7f26fa7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341394"
---
# <a name="ndisstatuswwanpreferredproviders"></a>NDIS\_状態\_WWAN\_優先\_プロバイダー


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_優先\_MB サービス優先プロバイダー一覧 (PPL) が変更されたことを通知するためにプロバイダーの通知。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_優先\_プロバイダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567913)構造体。

<a name="remarks"></a>注釈
-------

場合によっては、PPL (GSM ベースのデバイス) はネットワークによって更新されますか Over-The-Air (OTA) やショート メッセージ サービス (SMS) でします。 ミニポート ドライバーでは、PPL を適宜更新する必要があります。 その後、ミニポート ドライバーはこのを示す値を使用して、更新された PPL での更新に関する MB サービスに通知する必要があります。 GSM ベースのネットワークの場合、 **PreferredListHeader** NDIS のメンバー\_WWAN\_優先\_プロバイダーの構造は、更新された PPL を指す必要があります。

ミニポート ドライバーでは、このを示す値を使用して、結果として更新プログラムに関する MB サービスに通知する、 [OID\_WWAN\_優先\_プロバイダー](oid-wwan-preferred-providers.md) MB サービスからの要求のセット。 OID への応答を\_WWAN\_優先\_プロバイダー セット要求内の 0 個の要素を含める必要があります、 **PreferredListHeader**メンバー。

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


[**NDIS\_WWAN\_優先\_プロバイダー**](https://msdn.microsoft.com/library/windows/hardware/ff567913)

[OID\_WWAN\_優先\_プロバイダー](oid-wwan-preferred-providers.md)

 

 




