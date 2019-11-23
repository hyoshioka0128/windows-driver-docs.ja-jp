---
title: NDIS_STATUS_WWAN_HOME_PROVIDER
description: ミニポートドライバーは、NDIS_STATUS_WWAN_HOME_PROVIDER 通知を使用して、MB サービスに OID_WWAN_HOME_PROVIDER \ 160; の完了を通知します。クエリ要求。
ms.assetid: a5733c62-be4e-4f86-9639-6addd31baf0c
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_HOME_PROVIDER
ms.localizationpriority: medium
ms.openlocfilehash: 67cbe24dbbefe26027dfdca97cc178f8275a22dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843027"
---
# <a name="ndis_status_wwan_home_provider"></a>NDIS\_ステータス\_WWAN\_ホーム\_プロバイダー


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_ホーム\_プロバイダー通知を使用して、 [OID\_wwan\_ホーム\_プロバイダー](oid-wwan-home-provider.md)  クエリ要求の完了を MB サービスに通知します。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_HOME\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)構造を使用します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、OID\_WWAN\_ホーム\_プロバイダーのクエリ要求に応答するときに、次の規則に準拠する必要があります。

-   GSM ベースのデバイス: ホームプロバイダー名は、SIM の EFSPN 基本ファイルからのようないくつかの方法を使用してサブスクライバー Id モジュール (SIM) から取得できます (EFSPN は、セクションサービスプロバイダー名の下の 3GPP TS 31.102 で定義されています)。または、EFSPN がプロビジョニングされていない場合のオペレーター固有の拡張機能。 ホームプロバイダー名を取得し、IMSI から MCC を抽出し、GSMA SE. 13 データベースで検索を実行するために、オペレーター固有の要件の仕様を参照する必要があります。 EFSPN がプロビジョニングされていない場合、オペレーター固有のホームプロバイダー名を取得するには、オペレーターに問い合わせてください。 EFSPN またはその他のメカニズムを使用して、ホームプロバイダー名を使用して SIM がプロビジョニングされていない場合、ミニポートドライバーではプロバイダー名を**NULL**に設定する必要があります。

    SIM カードのファイルシステムの詳細については、3GPP TS 11.11 の仕様を参照してください。 プロバイダー id がサブスクライバー Id モジュール (SIM カード) でプロビジョニングされていない場合、ミニポートドライバーは、\_の失敗\_、WWAN\_ステータスを返す必要があります。

-   CDMA ベースのデバイス: ホームプロバイダー名を返すことは必須です。 ネットワークのパーソナル化の一環として、この情報をデバイスに提供することをお勧めします。 プロバイダー id が使用できない場合、CDMA ベースのプロバイダーのミニポートドライバーは、NDIS\_WWAN\_HOME\_プロバイダー構造の**プロバイダーの ProviderId**メンバー\_を、既定\_プロバイダー\_ID に設定する必要があります。\_

ミニポートドライバーは、デバイスの準備完了状態が**WwanReadyStateInitialized**に変更されたときにこの情報を返す必要があります。また、必要に応じて、WWAN\_プロバイダー構造のすべてのメンバーをフォーマットします。

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_ホーム\_プロバイダー](oid-wwan-home-provider.md)

[**NDIS\_WWAN\_ホーム\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)

 

 




