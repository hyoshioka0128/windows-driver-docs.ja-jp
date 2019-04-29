---
title: OID_QOS_PARAMETERS
description: データ センター ブリッジング (DCB) コンポーネント (Msdcb.sys) は、ネットワーク アダプターでローカルの NDIS サービスの品質 (QoS) パラメーターを構成する OID_QOS_PARAMETERS のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 1CA97C8A-8F5B-4AB2-B68E-DF1FA772C08F
ms.date: 08/08/2017
keywords: -OID_QOS_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 26d72a6148c7e5c1ad8f55b9b8d1ecc8f7fd0455
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364128"
---
# <a name="oidqosparameters"></a>OID\_QOS\_パラメーター


OID のオブジェクト識別子 (OID) メソッド要求を発行するデータ センター ブリッジング (DCB) コンポーネント (Msdcb.sys)\_QOS\_ネットワーク アダプターでローカルの NDIS サービスの品質 (QoS) パラメーターを構成するパラメーター。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体。

**注**この OID メソッド要求は、IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスの NDIS QoS をサポートするミニポート ドライバーに対して必須です。



<a name="remarks"></a>コメント
-------

OID の OID メソッドの要求をローカルの NDIS QoS パラメーターを取得するミニポート ドライバー\_QOS\_パラメーター。 これらのパラメーターは、ネットワーク アダプターが、送信に優先順位を定義または*エグレス*パケット。 これらのパラメーターの詳細については、次を参照してください。 [NDIS QoS パラメーターの概要](https://msdn.microsoft.com/library/windows/hardware/hh440130)します。

**注**DCB コンポーネントは、OID の OID メソッド要求を発行できるのみ\_QOS\_パラメーター。 上位のプロトコルまたはフィルター ドライバーをこの OID を発行する必要があります。 DCB のコンポーネントの詳細については、次を参照してください。[データ センター ブリッジングの NDIS QoS アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/hh451627)します。



DCB のコンポーネントの問題、OID\_QOS\_次の条件でパラメーター要求。

-   システム管理者では、インストールまたは Microsoft DCB サーバーの機能をアンインストールします。

    DCB のサーバー機能の詳細については、次を参照してください。 [System-Provided DCB コンポーネント](https://msdn.microsoft.com/library/windows/hardware/hh440259)します。

-   システム管理者は、有効または機能がまだインストールされているときに、DCB サーバー機能を無効にします。

-   システム管理者は、DCB サーバー機能のパラメーターのいずれかを変更します。

-   オペレーティング システムでは、開始またはがインストールされるため、DCB サーバー機能を再起動します。

ミニポート ドライバーが OID の OID メソッド要求を処理するときに\_QOS\_パラメーターでは、次のガイドラインに従ってする必要があります。

-   ミニポート ドライバー内のデータのコピー、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)の NDIS QoS パラメーターをローカル キャッシュに構造体。 ドライバーは、NDIS QoS パラメーターをローカルのキャッシュとキャッシュのリモート ピアから受信した NDIS QoS パラメーターに基づいて、運用の NDIS QoS パラメーターを解決します。

    ミニポート ドライバーがその運用パラメーターを解決する方法の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを解決する](https://msdn.microsoft.com/library/windows/hardware/hh440220)します。

-   ミニポート ドライバーが含まれるすべてのデータを変更する必要があります、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体。 ドライバーが、OID メソッド要求を完了し、内で元のデータを返す必要があります、 **NDIS\_QOS\_パラメーター**構造体。

-   **NDIS\_QOS\_パラメーター\_WILLING**フラグは、ミニポート ドライバーが有効または、ローカル Data Center Bridging Exchange (DCBX) しようとして状態を無効にするかどうかを指定します。 ドライバーは、次のように、このフラグを処理します。

    -   このフラグが設定されている場合は、ミニポート ドライバーにしようとして状態ローカル DCBX が有効にする必要があります。 これにより、QoS の設定でリモートで構成されるドライバーができます。 この場合、ドライバーは、リモートの QoS パラメーターに基づく運用 QoS パラメーターを解決します。 ミニポート ドライバーでは、独立系ハードウェア ベンダー (IHV) で定義されている独自の QoS 設定に基づいて、運用の QoS パラメーターを解決することもできます。

    -   このフラグが設定されていない場合、ミニポート ドライバーはしようとして状態ローカル DCBX を無効にする必要があります。 これにより、リモートの QoS パラメーターではなく、ローカルの QoS パラメーターから、運用の QoS パラメーターを解決するのには、ドライバーができます。 ミニポート ドライバーを無効にするかをローカルの QoS パラメーターをオーバーライドする必要がありますも、関連する**NDIS\_QOS\_パラメーター\_*Xxx*\_構成済み**フラグは設定されません。

        たとえば、ミニポート ドライバーは IHV によって定義されている QoS パラメーターに独自の設定で構成されていないローカル QoS パラメーターをオーバーライドできます。 ローカルの QoS パラメーターで指定されていない独自の設定がない場合、 **NDIS\_QOS\_パラメーター\_*Xxx*\_構成済み**フラグ、ドライバーは、ネットワーク アダプターにこれらの QoS パラメーターを使用を無効にする必要があります。

        **注**プロトコルや、ネットワーク アダプターで有効になっているテクノロジによって使用される QoS パラメーターが侵害される場合、ドライバーは構成されているローカル QoS パラメーターを上書きもできます。 たとえば、ドライバーは、Ethernet (FCoE) プロトコル経由でファイバー チャネル経由のリモート ブート用にネットワーク アダプターが有効になっている場合、ローカル QoS パラメーターをオーバーライドできます。

    ローカル DCBX の詳細については、状態のような場面を参照してください[DCBX 許容状態のローカル管理](https://msdn.microsoft.com/library/windows/hardware/hh706282)します。

ミニポート ドライバーがローカルの QoS パラメーターを上書きする方法の詳細については、次を参照してください。 [NDIS QoS パラメーターを管理する](https://msdn.microsoft.com/library/windows/hardware/hh464015)します。

**注**ローカル QoS パラメーターを上書きする必要があります OID の OID メソッド要求は失敗するミニポート ドライバーが発生しない\_QOS\_パラメーター。

ミニポート ドライバーがローカルの QoS パラメーターを管理する方法の詳細については、次を参照してください。 [NDIS QoS パラメーターをローカル設定](https://msdn.microsoft.com/library/windows/hardware/hh440225)します。

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーでは、次のステータス コードのいずれかを返します。

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
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_PENDING</p></td>
<td><p>保留中の入力候補の OID 要求です。 ミニポート ドライバーを呼び出すと<a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong></a>NDIS は最終的な状態コードを渡すし、呼び出し元の要求の後の OID 要求の完了ハンドラーに結果が完了しました。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポート ドライバーでは、NDIS QoS インターフェイスはサポートしません。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh451640" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451640)"> <strong>NDIS_QOS_PARAMETERS</strong> </a>構造が正しくない値を含めることができます。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さがより小さい<strong>sizeof</strong>(<a href="https://msdn.microsoft.com/library/windows/hardware/hh451640" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451640)"><strong>NDIS_QOS_PARAMETERS</strong></a>)。 NDIS セット、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_QOS\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)

[**NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)

[**NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)








