---
title: NDIS_STATUS_WWAN_HOME_PROVIDER
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_HOME_PROVIDER 通知を使用して、OID_WWAN_HOME_PROVIDER の完了に関する MB サービスに通知する \ 160;クエリ要求。
ms.assetid: a5733c62-be4e-4f86-9639-6addd31baf0c
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_HOME_PROVIDER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2274f406304e95cbd6e30157ee7df839a6ea4001
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537415"
---
# <a name="ndisstatuswwanhomeprovider"></a>NDIS\_状態\_WWAN\_ホーム\_プロバイダー


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_ホーム\_MB サービスに通知の完了に関する通知をプロバイダー [OID\_WWAN\_ホーム\_プロバイダー](oid-wwan-home-provider.md)  要求のクエリを実行します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_ホーム\_プロバイダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567909)構造体。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーは、OID に応答する場合、次の規則に準拠する必要があります\_WWAN\_ホーム\_プロバイダー クエリ要求。

-   GSM ベースのデバイス:ホーム プロバイダー名は、SIM で EFSPN 基本ファイルからのようにいくつかのメソッドを使用してサブスクライバー Identity モジュール (SIM) から取得できます (EFSPN の [サービスのプロバイダー名] セクション 3 gpp TS 31.102 で定義) またはオペレーターの特定拡張機能、EFSPN がプロビジョニングされていない場合は。 ホーム プロバイダー名を取得し、IMSI から MCC mnc もを抽出しを参照してくださいを GSMA SE.13 データベースでを実行する演算子に固有の要件の仕様を参照してください。 演算子に固有のホーム プロバイダー名を取得するとき、EFSPN がプロビジョニングされていない場合は、オペレーターに問い合わせてください。 ミニポート ドライバーにプロバイダー名を設定する必要があります、SIM が EFSPN またはその他のメカニズムを通じてホーム プロバイダーの名前を持つ準備されていない場合**NULL**します。

    詳細については、SIM カードのファイル システムは、3 gpp TS 11.11 の仕様を参照してください。 ミニポート ドライバーが WWAN を返す場合 Subscriber Identity Module (SIM カード) では、プロバイダー id は準備されていない、\_状態\_読み取り\_エラー。

-   CDMA ベースのデバイス:ホーム プロバイダー名を返すことは必須です。 Ihv がネットワークの個人用設定の一部として、デバイスでは、この情報を提供することをお勧めします。 CDMA ベースのプロバイダーのミニポート ドライバーを設定する必要があります、プロバイダー id が使用できない場合、 **Provider.ProviderId**の NDIS メンバー\_WWAN\_ホーム\_WWANプロバイダー構造体\_CDMA\_既定\_プロバイダー\_id。

デバイスの準備完了状態を変更するときに、ミニポート ドライバーはこの情報を返す必要があります**WwanReadyStateInitialized** 、WWAN のすべてのメンバーの書式を設定して\_に応じて、プロバイダーの構造体。

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


[OID\_WWAN\_ホーム\_プロバイダー](oid-wwan-home-provider.md)

[**NDIS\_WWAN\_ホーム\_プロバイダー**](https://msdn.microsoft.com/library/windows/hardware/ff567909)

 

 




