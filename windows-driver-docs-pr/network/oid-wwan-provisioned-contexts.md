---
title: OID_WWAN_PROVISIONED_CONTEXTS
description: OID_WWAN_PROVISIONED_CONTEXTS は、MB デバイスまたはサブスクライバー Id モジュール (SIM) に格納されている、プロビジョニングされたコンテキストエントリを読み取りまたは更新します。
ms.assetid: 7634fc32-9059-4f89-a591-7aa663b0c188
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_PROVISIONED_CONTEXTS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: ee4ef4382aa1dc7eb6007f972c0efa7df28c508c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843806"
---
# <a name="oid_wwan_provisioned_contexts"></a>OID\_WWAN\_プロビジョニングされた\_コンテキスト


OID\_WWAN\_プロビジョニングされた\_コンテキストは、MB デバイスまたはサブスクライバー Id モジュール (SIM) に格納されているプロビジョニング済みのコンテキストエントリを読み取りまたは更新します。

ミニポートドライバーは、セットおよびクエリ要求を非同期的に処理し、最初に NDIS\_の\_状態を返し、元の要求に必要な\_を示し、後で[**ndis\_ステータス\_WWAN を送信する必要があり\_** ](ndis-status-wwan-provisioned-contexts.md)プロビジョニングされた\_コンテキストの状態通知では、プロビジョニングされたコンテキストエントリに関する情報を提供するために、 [**NDIS\_WWAN\_プロビジョニング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)された\_コンテキスト構造が含まれています。Set 要求またはクエリ要求の完了に関係なく、id モジュール (SIM)。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN パケットコンテキスト管理](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-context-management)」を参照してください。

サポートされている MB のデバイスでプロビジョニングされたコンテキストの取得がサポートされていない場合、ミニポートドライバーは NDIS\_の状態\_返す必要があり\_サポートされていません。

GSM ベースのデバイスでは、必要に応じてクエリと設定操作をサポートできます。 CDMA ベースのデバイスでは、必要に応じて、簡易 IP を報告するクエリ操作 (WWAN\_CTRL\_CAPS\_CDMA\_単純\_IP) をサポートできます。

MB デバイスまたは SIM に格納されているプロビジョニング済みのコンテキストエントリは、デバイスに対してローカルです。 ミニポートドライバーは、これらのフィールドを読み取るためにネットワークに接続しないでください。

Set 要求の入力構造は、NDIS\_WWAN\_SET\_プロビジョニングされた\_コンテキスト、およびこのオブジェクトの状態の表示は、プロビジョニングされた\_コンテキスト\_の NDIS\_STATUS\_状態を示します。

プロビジョニングされたコンテキストは、APNs の一覧をキャッシュする3GPP の GPRS コンテキスト定義と同じではありません。 プロビジョニングされたコンテキストとは、デバイスによってプロビジョニングされたオペレーターまたは OTA によって事前にプロビジョニングされた接続パラメーター (AccessString、UserName、および Password) のことで、デバイスのメモリまたは SIM のいずれかに格納できます。 プロビジョニングされたコンテキストによって返された接続パラメーターは、PDP のアクティブ化のために MB サービスによって使用されます。

このオブジェクトのクエリと set の両方の形式が使用されます。

この要求の処理にはネットワークアクセスは必要ありませんが、MB デバイスの SIM または補助メモリへのアクセスが必要です。

ミニポートドライバーは、NDIS\_ステータス\_WWAN\_プロビジョニングされた\_コンテキストの通知をオペレーティングシステムに送信します。 **ContextListHeader**メンバーは*WwanStructContext*に設定されている必要があります。 通知が set 要求に応答して送信される場合、ミニポートドライバーは**ContextListHeader**メンバーを0に設定する必要があります。

MB サービスは、個々のコンテキストのアクティブ化または非アクティブ化を実行する前に、デバイスからプロビジョニングされたコンテキストの一覧を取得する必要があります。 プロビジョニングされたコンテキストの一覧は、デバイスに複数のネットワークプロバイダーコンテキストを格納する機能がある場合でも、ホームプロバイダーネットワークのみに制限する必要があります。 ローミングの場合でも、コンテキストリストは常にホームプロバイダーネットワーク固有である必要があります。

OID\_\_プロビジョニングされた\_コンテキスト操作は、コンテキストを、WWAN\_SET\_CONTEXT 構造体の**ProviderId**メンバーの set 要求で指定されているネットワークプロバイダーに関連付ける必要があります。 Set OID\_WWAN\_\_プロビジョニングされた、プロビジョニングされたコンテキストは、システムの再起動とデバイスの電力リサイクルの間に保持する必要があります。

すべての空のコンテキストは、ホームプロバイダーネットワークに適用されるプロビジョニング済みのコンテキストと共に、クエリで報告する必要があります。

SimpleIP 用に構成された CDMA デバイス、WWAN でのレポート\_CTRL\_CAPS\_CDMA\_単純な\_IP を使用して、必要に応じて、適切な**Accessstring**が入力された1つ以上のプロビジョニング済みコンテキストを返すことができますMB サービスからのクエリ要求の、**ユーザー名**、および**パスワード**のメンバー。

プロビジョニングされたコンテキストリストは、デバイスで事前プロビジョニングされている必要があります。また、set OID\_WWAN\_プロビジョニングされた\_コンテキスト操作によって更新されるか、SMS または OTA を使用してデバイス/オペレーターによって更新されます。 OID\_WWAN\_の MB サービスによる接続操作で指定されたコンテキスト情報に基づいて動的に更新することはできません。

リスト内のプロビジョニングされた各コンテキストについて、MB デバイスから AccessString、UserName、および Password にアクセスする方法の詳細については、「 [**WWAN\_context**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_context)」を参照してください。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[WWAN パケットコンテキスト管理](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-context-management)

 

 




