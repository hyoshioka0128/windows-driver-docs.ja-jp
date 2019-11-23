---
title: NDKPI の用語
description: NDKPI ドキュメントでは、次の用語を使用して、NDK プロバイダーとコンシューマーについて説明します。
ms.assetid: 740A78B3-B7AD-4A8C-8097-D49B39BC9F47
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68dac8baf832d391abe5a35ec70c9db81c6c8fe7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831889"
---
# <a name="ndkpi-terminology"></a>NDKPI の用語


NDKPI ドキュメントでは、次の用語を使用して、NDK プロバイダーとコンシューマーについて説明します。

-   [プロバイダー関数](#provider-function)
-   [コンシューマーコールバック](#consumer-callback)
-   [完了コールバック](#completion-callback)
-   [イベントコールバック](#event-callback)
-   [親オブジェクト](#parent-object)
-   [子オブジェクト](#child-object)
-   [継続元オブジェクト](#antecedent-object)
-   [後継オブジェクト](#successor-object)
-   [終点](#endpoint)
-   [関連トピック](#related-topics)

## <a name="provider-function"></a>プロバイダー関数


NDK オブジェクトの関数ディスパッチテーブル内の NDKPI 関数。 プロバイダー関数は、NDK プロバイダーによって実装され、NDK コンシューマーによって呼び出されます。 すべてのプロバイダー関数は、最初のパラメーターとして、操作対象のオブジェクトへのポインターを持ちます。 このポインターは、のC++"this" ポインターに似ています。 このポインターは、常にコンシューマーによってプロバイダー関数に明示的に渡されます。

## <a name="consumer-callback"></a>コンシューマーコールバック


NDK コンシューマーによって実装され、NDK プロバイダーによって呼び出される NDKPI 関数。 コンシューマーコールバックには、完了コールバックとイベントコールバックの2種類があります。

## <a name="completion-callback"></a>完了コールバック


非同期プロバイダー関数の完了を通知するために NDK プロバイダーによって呼び出されるコンシューマーコールバック。 NDKPI 1.1 および1.2 では、3つの完了コールバックがあります。

-   *NdkCloseCompletion* ([*NDK\_FN\_終了\_完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_close_completion))
-   *NdkCreateCompletion* ([*NDK\_FN\_作成\_完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_completion))
-   *Ndkrequestcompletion* ([*NDK\_FN\_要求\_完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_request_completion))

## <a name="event-callback"></a>イベントコールバック


Ndk プロバイダーが、非同期プロバイダー関数によってトリガーされることなく、NDK オブジェクトの特定のイベントを非同期に示すために呼び出すことができるコンシューマーコールバック。 NDKPI 1.1 および1.2 では、4つのイベントコールバックがあります。

-   *NdkCqNotificationCallback* ([*NDK\_FN\_CQ\_NOTIFICATION\_コールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback))
-   *Ndkconnecteventcallback* ([*NDK\_FN\_CONNECT\_イベント\_コールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback))
-   *Ndkdisconnect Eventcallback* ([*NDK\_FN\_切断\_イベント\_コールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_disconnect_event_callback))
-   *Ndksrqnotificationcallback* ([*NDK\_FN\_で\_通知\_コールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_srq_notification_callback))

## <a name="parent-object"></a>親オブジェクト


他のオブジェクトを作成するための1つ以上の*Ndkcreate*Xxx * * プロバイダー関数を含む関数ディスパッチテーブルを持つ NDK オブジェクト。 NDKPI バージョン1.1 および1.2 では、次の2つの親オブジェクトがあります。

NDK アダプタオブジェクト ([**ndk\_アダプタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)) は、次の親になります。

-   [**NDK\_コネクタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)
-   [**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq)
-   [**NDK\_リスナー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener)
-   [**NDK\_論理\_アドレス\_マッピング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_logical_address_mapping)
-   [**NDK\_PD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_pd)
-   [**NDK\_共有\_エンドポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint)

NDK protection ドメイン (PD) オブジェクト ([**ndk\_PD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_pd)) は、次の親になります。

-   [**NDK\_MR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr)
-   [**NDK\_MW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw)
-   [**NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)
-   [**NDK\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq)

## <a name="child-object"></a>子オブジェクト


親オブジェクトのディスパッチテーブルで*Ndkcreate*Xxx * * プロバイダー関数の1つを呼び出すことによって作成される NDK オブジェクト。

## <a name="antecedent-object"></a>継続元オブジェクト


機能を提供するために別のオブジェクトが依存する NDK オブジェクト。 継続元オブジェクトは、後続オブジェクトの前に作成する必要があります。 すべての親オブジェクトが継続元オブジェクトであることに注意してくださいが、その逆は当てはまりません。

## <a name="successor-object"></a>後継オブジェクト


継続元オブジェクトに依存する NDK オブジェクト。 継続元オブジェクトは、後続オブジェクトの前に作成する必要があります。 すべての子オブジェクトが後続処理オブジェクトであることに注意してください。ただし、逆の場合は無効です。 継続元/後続関係は、必要に応じて、省略可能な場合もあれば、後続の作成後のポイントまで遅延する場合もあります。

次の継続元/後続関係は、NDKPI バージョン1.1 および1.2 によって定義されています (親/子のリレーションシップに加えて、定義別の継続元/後続関係)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Antecedent</th>
<th align="left">後続</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq" data-raw-source="[&lt;strong&gt;NDK_CQ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq)"><strong>NDK_CQ</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)"><strong>NDK_QP</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr" data-raw-source="[&lt;strong&gt;NDK_MR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr)"><strong>NDK_MR</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw" data-raw-source="[&lt;strong&gt;NDK_MW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw)"><strong>NDK_MW</strong></a> (「 <em>ndkbind</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_bind" data-raw-source="[&lt;em&gt;NDK_FN_BIND&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_bind)"><em>NDK_FN_BIND</em></a>)」を参照してください)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq" data-raw-source="[&lt;strong&gt;NDK_SRQ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq)"><strong>NDK_SRQ</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)"><strong>NDK_QP</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)"><strong>NDK_QP</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)"><strong>NDK_CONNECTOR</strong></a> (「 <em>ndkconnect</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect)"><em>NDK_FN_CONNECT</em></a>)」、「 <em>ndkconnect</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_accept" data-raw-source="[&lt;em&gt;NDK_FN_ACCEPT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_accept)"><em>NDK_FN_ACCEPT</em></a>)」、および「 <em>ndkconnectwithsharedendpoint</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_WITH_SHARED_ENDPOINT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)"><em>NDK_FN_CONNECT_WITH_SHARED_ENDPOINT</em></a>)」を参照してください。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint" data-raw-source="[&lt;strong&gt;NDK_SHARED_ENDPOINT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint)"><strong>NDK_SHARED_ENDPOINT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)"><strong>NDK_CONNECTOR</strong></a> (「 <em>Ndkconnectwithsharedendpoint</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_WITH_SHARED_ENDPOINT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)"><em>NDK_FN_CONNECT_WITH_SHARED_ENDPOINT</em></a>)」を参照してください)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener" data-raw-source="[&lt;strong&gt;NDK_LISTENER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener)"><strong>NDK_LISTENER</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)"><strong>NDK_CONNECTOR</strong></a> (「 <em>Ndkconnecteventcallback</em> (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_EVENT_CALLBACK&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback)"><em>NDK_FN_CONNECT_EVENT_CALLBACK</em></a>)」を参照してください)。</p></td>
</tr>
</tbody>
</table>

 

## <a name="endpoint"></a>endpoint


接続を開始または受け入れ可能なローカルポイントを識別する、ローカルアドレスと NetworkDirect ポート番号の暗黙的または明示的な表現です。たとえば、10.1.1.1: 445 のようになります。

-   [**NDK\_リスナー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener)には、暗黙的なエンドポイントがあります (コンシューマーは、 *ndklisten* ([*NDK\_FN\_LISTEN*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_listen)) を呼び出すときに指定します)。
-   *Ndkconnect* ([*ndk\_FN\_CONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect)) を呼び出すことによって接続される[**ndk\_コネクタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)には、暗黙のエンドポイントもあります。
-   [**NDK\_SHARED\_エンドポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint)は、明示的なエンドポイントを表します。 NDK コンシューマーは、エンドポイントを直接作成し、それを明示的に使用して1つ以上の接続を開始します。そのためには、 *Ndkconnectwithsharedendpoint* ([*NDK\_FN\_CONNECT\_と\_共有\_エンドポイント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)) を呼び出します。

NDK エンドポイントが NDSPI version 1 [**Indendpoint**](https://docs.microsoft.com/previous-versions/windows/desktop/cc904370(v=vs.85))インターフェイスまたは ndspi Version 2 **indqueuepair**インターフェイスと異なる  に**注意**してください。

 

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






