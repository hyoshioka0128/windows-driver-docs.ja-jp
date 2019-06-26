---
title: OID_WWAN_PREFERRED_PROVIDERS
description: OID_WWAN_PREFERRED_PROVIDERS では、GSM ベースのデバイスの推奨されるプロバイダーの一覧に関する情報を返します。
ms.assetid: fa70f1ac-5b14-44f8-a2c4-d2163fe81c5a
ms.date: 08/08/2017
keywords: -OID_WWAN_PREFERRED_PROVIDERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: fa078036ff9709533f800801e0f42e03bf9aef0f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383214"
---
# <a name="oidwwanpreferredproviders"></a>OID\_WWAN\_優先\_プロバイダー


OID\_WWAN\_優先\_プロバイダーが優先 GSM ベースのデバイス プロバイダーの一覧に関する情報を返します。 CDMA ベースのデバイスのミニポート ドライバーは、この OID をサポートする必要はありません。

ミニポート ドライバー セットを処理する必要があり、クエリ要求が最初に、非同期に返す NDIS\_状態\_を示す値\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_優先\_プロバイダー** ](ndis-status-wwan-preferred-providers.md)状態通知を含む、 [ **NDIS\_WWAN\_優先\_プロバイダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)または要求のクエリについて、優先プロバイダー一覧 (PPL) 設定を完了に関係なく情報を指定する構造体。

<a name="remarks"></a>注釈
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN プロバイダー操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)します。

ミニポート ドライバー Subscriber Identity Module (SIM カード) にアクセスできると処理クエリの要求が、プロバイダーのネットワークにアクセスしないでください。

ミニポート ドライバー Subscriber Identity Module (SIM カード) にアクセスできるか、処理するときに、プロバイダーのネットワークは、要求を設定します。

OID を処理するときに\_WWAN\_優先\_プロバイダー、ミニポート ドライバーは WWAN のみを設定できます\_プロバイダー\_状態\_優先または WWAN\_プロバイダー\_状態\_リストの項目をタグ付けするフラグを許可されていません。 禁止されているプロバイダーが可能性があります GSM ベースのデバイス一覧に表示されないことに注意します。

ミニポート driverrs を設定する必要があります、 **PreferredListHeader.ElementType**メンバー *WwanStructProvider*します。 ミニポート ドライバーを設定する必要があります、 **PreferredListHeader.ElementCount** 0 OID に応答するときにメンバー\_WWAN\_優先\_プロバイダーが要求を設定します。

デバイスで PPL を上書きできるか、デバイスの機能、携帯電話のテクノロジや、ネットワーク プロバイダーのポリシーに依存しない処理が要求を設定するとします。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_PPL を設定または取得をサポートしていない場合にサポートされます。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_優先\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)

[**NDIS\_状態\_WWAN\_優先\_プロバイダー**](ndis-status-wwan-preferred-providers.md)

[WWAN プロバイダー操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




