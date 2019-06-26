---
title: NDKPI の用語
description: NDKPI ドキュメントでは、次の用語を使用して、NDK プロバイダーとコンシューマーについて説明します。
ms.assetid: 740A78B3-B7AD-4A8C-8097-D49B39BC9F47
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5909903d1577d96daa5c62fc300367ad352dcf92
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364034"
---
# <a name="ndkpi-terminology"></a>NDKPI の用語


NDKPI ドキュメントでは、次の用語を使用して、NDK プロバイダーとコンシューマーについて説明します。

-   [プロバイダー関数](#provider-function)
-   [コンシューマーのコールバック](#consumer-callback)
-   [完了コールバック](#completion-callback)
-   [イベントのコールバック](#event-callback)
-   [親オブジェクト](#parent-object)
-   [子オブジェクト](#child-object)
-   [継続元のオブジェクト](#antecedent-object)
-   [後続のオブジェクト](#successor-object)
-   [endpoint](#endpoint)
-   [関連トピック](#related-topics)

## <a name="provider-function"></a>プロバイダー関数


NDK オブジェクトの関数のディスパッチ テーブルで NDKPI 関数。 プロバイダーの関数は NDK プロバイダーによって実装され、NDK コンシューマーによって呼び出されます。 プロバイダーのすべての関数は、最初のパラメーターとして、動作するオブジェクトへのポインターをあります。 このポインターは、C++ では、"this"ポインターに似ています。 このポインターは常に明示的にコンシューマーによって関数に渡す、プロバイダー。

## <a name="consumer-callback"></a>コンシューマーのコールバック


NDKPI 関数は、NDK コンシューマーによって実装され、NDK プロバイダーによって呼び出されます。 コンシューマーのコールバックの 2 種類があります。 完了コールバックとイベントのコールバック。

## <a name="completion-callback"></a>完了コールバック


コンシューマーのコールバックで、非同期プロバイダー関数の完了を知らせる NDK プロバイダーによって呼び出されます。 NDKPI 1.1 と 1.2 では、3 つの完了コールバックがあります。

-   *NdkCloseCompletion* ([*NDK\_FN\_CLOSE\_COMPLETION*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_close_completion))
-   *NdkCreateCompletion* ([*NDK\_FN\_CREATE\_COMPLETION*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_completion))
-   *NdkRequestCompletion* ([*NDK\_FN\_REQUEST\_COMPLETION*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_request_completion))

## <a name="event-callback"></a>イベントのコールバック


非同期プロバイダー関数によってトリガーされず、非同期的に NDK オブジェクトの特定のイベントを示すために NDK プロバイダーによって呼び出すことができるコンシューマー コールバック。 NDKPI 1.1 と 1.2 では、4 つのイベントのコールバックがあります。

-   *NdkCqNotificationCallback* ([*NDK\_FN\_CQ\_NOTIFICATION\_CALLBACK*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback))
-   *NdkConnectEventCallback* ([*NDK\_FN\_CONNECT\_EVENT\_CALLBACK*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback))
-   *NdkDisconnectEventCallback* ([*NDK\_FN\_DISCONNECT\_EVENT\_CALLBACK*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_disconnect_event_callback))
-   *NdkSrqNotificationCallback* ([*NDK\_FN\_SRQ\_NOTIFICATION\_CALLBACK*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_srq_notification_callback))

## <a name="parent-object"></a>親オブジェクト


関数のディスパッチ テーブルが含まれるは、1 つ以上含まれています。 NDK オブジェクト*NdkCreate*Xxx * * プロバイダー関数を他のオブジェクトを作成します。 NDKPI バージョン 1.1 と 1.2 では、2 つの親オブジェクトがあります。

NDK アダプター オブジェクト ([**NDK\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter)) の親であります。

-   [**NDK\_CONNECTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector)
-   [**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_cq)
-   [**NDK\_LISTENER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_listener)
-   [**NDK\_LOGICAL\_ADDRESS\_MAPPING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_logical_address_mapping)
-   [**NDK\_PD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_pd)
-   [**NDK\_SHARED\_エンドポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_shared_endpoint)

NDK 保護ドメイン (PD) オブジェクト ([**NDK\_PD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_pd)) の親であります。

-   [**NDK\_MR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mr)
-   [**NDK\_MW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mw)
-   [**NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)
-   [**NDK\_SRQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_srq)

## <a name="child-object"></a>子オブジェクト


いずれかを呼び出すことによって作成される NDK オブジェクト、 *NdkCreate*Xxx * *、親オブジェクトのディスパッチ テーブル内のプロバイダー関数。

## <a name="antecedent-object"></a>継続元のオブジェクト


機能を提供するために別のオブジェクトが依存している NDK オブジェクト。 継続元のオブジェクトは、後続のオブジェクトの前に作成する必要があります。 すべての親オブジェクトは、継続元のオブジェクトが、逆はできませんに注意してください。

## <a name="successor-object"></a>後続のオブジェクト


継続元のオブジェクトに依存している NDK オブジェクト。 継続元のオブジェクトは、後続のオブジェクトの前に作成する必要があります。 すべての子オブジェクトは、後続のオブジェクトが、逆はできませんに注意してください。 継続元/後続処理の関係を可能性がある必要な省略可能なまたは遅延の点に場合によっては後続の作成後に注意してください。

次の後続の継続元/リレーションシップは、NDKPI バージョン 1.1 と 1.2 (に加えて、親/子リレーションシップ定義で継続元/後続処理の関係) で定義されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">継続元</th>
<th align="left">後続</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_cq" data-raw-source="[&lt;strong&gt;NDK_CQ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_cq)"><strong>NDK_CQ</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)"><strong>NDK_QP</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mr" data-raw-source="[&lt;strong&gt;NDK_MR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mr)"><strong>NDK_MR</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mw" data-raw-source="[&lt;strong&gt;NDK_MW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mw)"><strong>NDK_MW</strong> </a> (を参照してください<em>NdkBind</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_bind" data-raw-source="[&lt;em&gt;NDK_FN_BIND&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_bind)"><em>NDK_FN_BIND</em></a>).)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_srq" data-raw-source="[&lt;strong&gt;NDK_SRQ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_srq)"><strong>NDK_SRQ</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)"><strong>NDK_QP</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)"><strong>NDK_QP</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector)"><strong>NDK_CONNECTOR</strong> </a> (を参照してください<em>NdkConnect</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect)"><em>NDK_FN_CONNECT</em></a>)、 <em>NdkAccept</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_accept" data-raw-source="[&lt;em&gt;NDK_FN_ACCEPT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_accept)"> <em>NDK_FN_ACCEPT</em></a>)、および<em>NdkConnectWithSharedEndpoint</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_WITH_SHARED_ENDPOINT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)"><em>NDK_FN_CONNECT_WITH_SHARED_ENDPOINT</em></a>).)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_shared_endpoint" data-raw-source="[&lt;strong&gt;NDK_SHARED_ENDPOINT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_shared_endpoint)"><strong>NDK_SHARED_ENDPOINT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector)"><strong>NDK_CONNECTOR</strong> </a> (を参照してください<em>NdkConnectWithSharedEndpoint</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_WITH_SHARED_ENDPOINT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)"><em>NDK_FN_CONNECT_WITH_SHARED_ENDPOINT</em></a>).)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_listener" data-raw-source="[&lt;strong&gt;NDK_LISTENER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_listener)"><strong>NDK_LISTENER</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector)"><strong>NDK_CONNECTOR</strong> </a> (を参照してください<em>NdkConnectEventCallback</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_EVENT_CALLBACK&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback)"><em>NDK_FN_CONNECT_EVENT_CALLBACK</em></a>).)</p></td>
</tr>
</tbody>
</table>

 

## <a name="endpoint"></a>エンドポイント (endpoint)


どの接続を開始したり、10.1.1.1:445 を受け入れられる、ローカルのポイントを識別するローカル アドレスと NetworkDirect ポート番号の暗黙的または明示的な形式:

-   [ **NDK\_リスナー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_listener)暗黙的なエンドポイントがあります (を呼び出すときに、コンシューマーが指定する*NdkListen* ([*NDK\_FN\_リッスン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_listen)))。
-   [ **NDK\_コネクタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector)呼び出すことによって接続されている*NdkConnect* ([*NDK\_FN\_CONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect)) も暗黙的なエンドポイントがあります。
-   [ **NDK\_SHARED\_エンドポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_shared_endpoint)明示的なエンドポイントを表します。 NDK コンシューマーは、直接のエンドポイントを作成し、呼び出すことによって 1 つまたは複数の接続を開始するために明示的に使用*NdkConnectWithSharedEndpoint* ([*NDK\_FN\_接続\_WITH\_SHARED\_エンドポイント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint))。

**注**  An NDK エンドポイントがない NDSPI バージョン 1 と同じ[ **INDEndpoint** ](https://docs.microsoft.com/previous-versions/windows/desktop/cc904370(v=vs.85))インターフェイスまたはバージョン 2 NDSPI **INDQueuePair**インターフェイスです。

 

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






