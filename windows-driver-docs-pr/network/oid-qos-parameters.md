---
title: OID_QOS_PARAMETERS
description: データセンターブリッジング (DCB) コンポーネント (Msdcb) は、OID_QOS_PARAMETERS のオブジェクト識別子 (OID) メソッド要求を発行して、ネットワークアダプターでローカルの NDIS Quality of Service (QoS) パラメーターを構成します。
ms.assetid: 1CA97C8A-8F5B-4AB2-B68E-DF1FA772C08F
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_QOS_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: f7c295ef30da68bc07fb353789dc79027e3ad270
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844025"
---
# <a name="oid_qos_parameters"></a>OID\_QOS\_パラメーター


データセンターブリッジング (DCB) コンポーネント (Msdcb) は、OID のオブジェクト識別子 (OID) メソッド要求を発行し、ネットワークアダプターでローカルの NDIS Quality Service (QoS) パラメーターを構成するために QOS\_パラメーターを\_します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体へのポインターが含まれています。

**メモ** この OID メソッド要求は、IEEE 802.1 Data Center ブリッジング (DCB) インターフェイスの NDIS QoS をサポートするミニポートドライバーに必須です。



<a name="remarks"></a>注釈
-------

ミニポートドライバーは、oid\_QOS\_パラメーターを使用して、ローカル NDIS QoS パラメーターを取得します。 これらのパラメーターは、ネットワークアダプターがパケットの送信*または*送信に優先順位を設定する方法を定義します。 これらのパラメーターの詳細については、「 [NDIS QoS パラメーターの概要](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)」を参照してください。

**メモ** DCB コンポーネントのみが、oid の oid メソッド要求を\_QOS\_パラメーターに発行できます。 プロトコルまたはフィルタードライバーがこの OID を発行することはできません。 DCB コンポーネントの詳細については、「[データセンターブリッジングの NDIS QoS アーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-qos-architecture-for-data-center-bridging)」を参照してください。



DCB コンポーネントは、次の条件下で、OID\_QOS\_PARAMETERS 要求を発行します。

-   システム管理者は、Microsoft DCB server 機能をインストールまたはアンインストールします。

    DCB サーバー機能の詳細については、「[システム指定の DCB コンポーネント](https://docs.microsoft.com/windows-hardware/drivers/network/system-provided-dcb-components)」を参照してください。

-   システム管理者は、機能がまだインストールされている間は、DCB サーバーの機能を有効または無効にします。

-   システム管理者は、DCB サーバー機能のパラメーターのいずれかを変更します。

-   DCB サーバー機能のインストール中に、オペレーティングシステムが起動または再起動します。

ミニポートドライバーが oid\_の oid メソッド要求を処理するときに、QOS\_パラメーターの場合は、次のガイドラインに従う必要があります。

-   ミニポートドライバーは、 [**ndis\_qos\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造内のデータをローカル ndis qos パラメーターのキャッシュにコピーします。 その後、ドライバーは、ローカル NDIS QoS パラメーターのキャッシュと、リモートピアから受信した NDIS QoS パラメーターのキャッシュに基づいて、動作している NDIS qos パラメーターを解決します。

    ミニポートドライバーが操作パラメーターを解決する方法の詳細については、「[運用 NDIS QoS パラメーターの解決](https://docs.microsoft.com/windows-hardware/drivers/network/resolving-operational-ndis-qos-parameters)」を参照してください。

-   ミニポートドライバーは、 [**NDIS\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体内に含まれるデータを変更することはできません。 ドライバーは OID メソッド要求を完了し、 **NDIS\_QOS\_PARAMETERS**構造内の元のデータを返す必要があります。

-   [ **NDIS\_QOS\_PARAMETERS\_** ] フラグは、ミニポートドライバーがローカルデータセンターブリッジング (dcbx) の許可状態を有効または無効にするかどうかを指定します。 ドライバーは、このフラグを次のように処理します。

    -   このフラグが設定されている場合は、ミニポートドライバーでローカルの DCBX の状態を有効にする必要があります。 これにより、ドライバーは QoS 設定を使用してリモートで構成できます。 この場合、ドライバーは、リモート QoS パラメーターに基づいて、操作の QoS パラメーターを解決します。 また、ミニポートドライバーは、独立系ハードウェアベンダー (IHV) によって定義されている独自の QoS 設定に基づいて、動作中の QoS パラメーターを解決することもできます。

    -   このフラグが設定されていない場合、ミニポートドライバーはローカルの DCBX の状態を無効にする必要があります。 これにより、ドライバーは、リモート QoS パラメーターではなく、ローカルの QoS パラメーターから操作 QoS パラメーターを解決できます。 また、ミニポートドライバーは、関連する**NDIS\_qos\_パラメーター\_*XXX*\_構成**フラグが設定されていないローカル qos パラメーターも無効または無効にする必要があります。

        たとえば、ミニポートドライバーは、構成されていないローカル QoS パラメーターを、IHV によって定義された QoS パラメーターの独自の設定で上書きすることができます。 **NDIS\_qos\_parameters\_*XXX*\_構成**されたフラグで指定されていないローカル qos パラメーターに固有の設定がない場合、ドライバーはネットワークでこれらの QoS パラメーターの使用を無効にする必要があります。アダプター.

        **メモ** また、ネットワークアダプターで有効になっているプロトコルやテクノロジによって使用される QoS パラメーターが危害を受けた場合に、構成されたローカル QoS パラメーターを上書きすることもできます。 たとえば、ネットワークアダプターでファイバーチャネル over Ethernet (FCoE) プロトコルによるリモートブートが有効になっている場合、ドライバーはローカルの QoS パラメーターを上書きできます。

    ローカルの DCBX の状態の詳細については、「[ローカルの dcbx の状態の管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-the-local-dcbx-willing-state)」を参照してください。

ミニポートドライバーがローカル QoS パラメーターを上書きする方法の詳細については、「 [NDIS Qos パラメーターの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-ndis-qos--parameters)」を参照してください。

**メモ** ローカルの QoS パラメーターをオーバーライドして、ミニポートドライバーが oid の oid メソッド要求を失敗させないようにする必要があります。これは、QOS\_パラメーター\_ます。

ミニポートドライバーでローカルの QoS パラメーターを管理する方法の詳細については、「[ローカル NDIS Qos パラメーターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-local-ndis-qos-parameters)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

ミニポートドライバーは、次のいずれかの状態コードを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_PENDING</p></td>
<td><p>OID 要求の完了が保留されています。 ミニポートドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>を呼び出すと、NDIS は、要求が完了した後に、最終的なステータスコードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポートドライバーは、NDIS QoS インターフェイスをサポートしていません。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが<strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>) 未満です。 NDIS はデータを設定<strong>します。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由で要求が失敗しました。</p></td>
</tr>
</tbody>
</table>



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
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_QOS\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

[**NDIS\_ステータス\_QOS\_操作\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)

[**NDIS\_ステータス\_QOS\_リモート\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)








