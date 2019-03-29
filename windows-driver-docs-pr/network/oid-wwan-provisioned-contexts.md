---
title: OID_WWAN_PROVISIONED_CONTEXTS
description: OID_WWAN_PROVISIONED_CONTEXTS の読み取りや MB デバイスまたはサブスクライバー Identity モジュール (SIM) で格納されているプロビジョニングされたコンテキストのエントリを更新します。
ms.assetid: 7634fc32-9059-4f89-a591-7aa663b0c188
ms.date: 08/08/2017
keywords: -OID_WWAN_PROVISIONED_CONTEXTS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 78ea8f12f45601342fe47b3e6e0abd8baabd0adb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578640"
---
# <a name="oidwwanprovisionedcontexts"></a>OID\_WWAN\_プロビジョニング済み\_コンテキスト


OID\_WWAN\_プロビジョニング済み\_コンテキストの読み取りや MB デバイスまたはサブスクライバー Identity モジュール (SIM) で格納されているプロビジョニングされたコンテキストのエントリを更新します。

ミニポート ドライバー セットを処理する必要があり、クエリ要求が最初に、非同期に返す NDIS\_状態\_を示す値\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_プロビジョニング済み\_コンテキスト**](ndis-status-wwan-provisioned-contexts.md)状態通知を含む、 [ **NDIS\_WWAN\_プロビジョニング済み\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff567914) MB デバイスまたはデバイス セットまたはクエリの要求の完了に関係なくサブスクライバー Identity モジュール (SIM) で格納されているプロビジョニングされたコンテキストのエントリに関する情報を提供する構造体。

<a name="remarks"></a>コメント
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN パケット コンテキスト管理](https://msdn.microsoft.com/library/windows/hardware/ff559086)します。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_サポート MB デバイスがプロビジョニングされているコンテキストの取得をサポートしていない場合にサポートされます。

必要に応じて、GSM ベースのデバイスはクエリをサポートし、操作を設定します。 CDMA ベースのデバイスは、クエリ操作の単純な IP のレポートをサポートできます必要に応じて (WWAN\_CTRL\_CAP\_CDMA\_単純\_IP)。

MB デバイスまたは SIM に格納されているプロビジョニングされたコンテキストのエントリは、デバイスに対してローカルです。 ミニポート ドライバーは、これらのフィールドを読み取るようにネットワークに接続する必要がありますできません。

入力セットの要求の構造は、NDIS\_WWAN\_設定\_プロビジョニング済み\_このオブジェクトのコンテキストと状態を示す値は、NDIS\_状態\_WWAN\_プロビジョニング済み\_コンテキスト。

プロビジョニングのコンテキストは、GPRS コンテキストの定義では、3 gpp APNs の一覧をキャッシュするのと同じではないです。 プロビジョニングのコンテキストは、接続パラメーター (AccessString、UserName、およびパスワード) はいずれかの事前にプロビジョニングされる、演算子、または、OTA デバイスによってプロビジョニングされ、デバイスのメモリまたは SIM で格納されていることができますです。 プロビジョニング済みのコンテキストによって返される接続パラメーターは、PDP アクティブ化の MB サービスによって使用されます。

両方のクエリし、このオブジェクトのセットの形式が使用されます。

この要求の処理は、ネットワーク アクセスが必要としない、SIM または MB デバイスの補助メモリへのアクセスが必要です。

ミニポート ドライバー送信 NDIS\_状態\_WWAN\_プロビジョニング済み\_オペレーティング システムへの通知のコンテキスト。 **ContextListHeader.ElementType**メンバーを設定するものと*WwanStructContext*します。 ミニポート ドライバーを設定する必要があります、 **ContextListHeader.ElementCount**メンバー セットの要求に対する応答で通知を送信するときは 0 にします。

MB サービスは、任意の個々 のコンテキストのアクティブ化または非アクティブ化を実施する前に、デバイスからプロビジョニングのコンテキストの一覧を取得する必要があります。 プロビジョニングのコンテキストの一覧は、デバイスは、複数のネットワーク プロバイダー コンテキストを保存する機能を持っている場合でも、ホーム プロバイダー ネットワークのみに制限する必要があります。 コンテキストの一覧は、ホーム プロバイダー ネットワークをローミング場合でも同じ特定常にあります。

設定の OID\_WWAN\_プロビジョニング済み\_操作のコンテキストでセットの要求で指定されているネットワーク プロバイダー コンテキストを関連付ける必要があります**ProviderId** WWANのメンバー\_設定\_CONTEXT 構造体。 プロビジョニングのコンテキストを使って格納されている設定 OID\_WWAN\_プロビジョニング済み\_コンテキストの要求は、システム全体で保持する必要がありますが再起動し、デバイスの電源をリサイクルします。

空のすべてのコンテキストでは、ホーム プロバイダー ネットワークに適用可能なプロビジョニングのコンテキストと共にクエリに報告する必要があります。

SimpleIP、WWAN でのレポートが構成されている CDMA デバイス\_CTRL\_CAP\_CDMA\_単純\_WwanControlCaps で IP は、少なくとも 1 つのプロビジョニングされたコンテキストで塗りつぶさを返すことができます必要に応じて、正しい**AccessString**、 **UserName**、および**パスワード**MB サービスからのクエリ要求のメンバー。

プロビジョニングのコンテキストの一覧はセット OID によって更新、デバイスの事前プロビジョニングする必要があります\_WWAN\_プロビジョニング済み\_コンテキスト操作、または SMS または OTA デバイス/演算子によって更新します。 更新してはいけない OID で提供されるコンテキスト情報に基づいて動的に\_WWAN\_MB サービスで接続操作です。

MB デバイスの一覧でプロビジョニングされた各コンテキストから AccessString、UserName、およびパスワードにアクセスする方法の詳細については、次を参照してください。 [ **WWAN\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff571201)します。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[WWAN パケット コンテキスト管理](https://msdn.microsoft.com/library/windows/hardware/ff559086)

 

 




