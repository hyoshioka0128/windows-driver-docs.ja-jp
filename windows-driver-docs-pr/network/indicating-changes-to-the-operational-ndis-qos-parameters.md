---
title: 稼働中の NDIS QoS パラメーターへの変更の表示
description: 稼働中の NDIS QoS パラメーターへの変更の表示
ms.assetid: BAE99C83-2732-4216-BC49-23F541AA3F10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99bce96bad6f25c140ba9618737fb2bbc646cfb6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374820"
---
# <a name="indicating-changes-to-the-operational-ndis-qos-parameters"></a>稼働中の NDIS QoS パラメーターへの変更の表示


NDIS サービスの品質 (QoS) の問題をサポートしているミニポート ドライバー、 [ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)ドライバーの運用上の NDIS QoS パラメーターは、最初に、または後で変更するときに解決されたときに状態を示す値。 ミニポート ドライバーでは、QoS パケットの転送を実行するこれらのオペレーションのパラメーターをネットワーク アダプターを構成します。

ミニポート ドライバーが発行するための次のガイドラインに従う必要があります、 [ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状態を示す値。

-   ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状態表示後の運用上の NDIS QoS パラメーターを解決は、それらのネットワーク アダプターを構成します。

    **注**場合は、レジストリの専用のローカル NDIS QoS パラメーターを持つ、ミニポート ドライバーがプロビジョニングされると、ドライバーを発行する必要があります、 [ **NDIS\_状態\_QOS\_操作\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状態の表示中またはへの呼び出し後すぐに[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)します。 この場合、ドライバーを初期化します、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)その独自のローカル NDIS QoS パラメーター設定を含む構造体。

    ドライバーがその運用上の NDIS QoS パラメーター設定を解決する方法の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを解決する](resolving-operational-ndis-qos-parameters.md)します。

-   この最初の状態を示す値後、ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)運用上の NDIS QoS パラメーターが変更されたときに状態を示す値。 たとえば、運用上の NDIS QoS パラメーターは、次の条件下で変更できます。

    -   運用上の NDIS QoS パラメーターは、変更のため、ローカルの NDIS QoS パラメーターを変更します。 これらのパラメーターの OID メソッド要求を通じて変更[OID\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)または独立系ハードウェア ベンダー (IHV) によって開発された管理アプリケーションを使用します。

    -   リモート ピアから QoS の設定と競合するため、運用上の NDIS QoS パラメーターを変更します。

        ミニポート ドライバーは、IEEE 802.1 qaz を使用して Data Center Bridging Exchange (DCBX) プロトコルをリモート ピアの QoS パラメーターを検出します。 状態のような場面 DCBX が有効になっている場合、ドライバーは、DCBX 状態のエンジンに対して定義されている手順に従って、QoS パラメーターと、リモート ピアの QoS のパラメーターの違いを解決する必要があります。 この状態のエンジンの詳細については、IEEE 802.1 qaz を参照してくださいドラフト標準。

        ローカル DCBX の詳細については、状態のような場面を参照してください[DCBX 許容状態のローカル管理](managing-the-local-dcbx-willing-state.md)します。

    **注**発行するミニポート ドライバーでは、ローカルまたはリモートの NDIS QoS パラメーターを受信すると、 [ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)運用上の NDIS QoS パラメーターを変更されているなしの状態を示す値。 ドライバーはこの不要な状態の表示を行う場合 NDIS が重なってドライバーを示す値を渡すことができません。

-   ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状態表示ときに、運用上の NDIS QoS パラメーターを解決するために使用されたローカルの NDIS QoS パラメーターを上書きする必要があります。

    ミニポート ドライバーに通知の NDIS および上にあるドライバーを発行して、ローカルの NDIS QoS パラメーターがオーバーライドされること、 [ **NDIS\_状態\_QOS\_OPERATIONAL\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状態を示す値。 この種類の表示にするには、ドライバーは、適切な設定する必要があります**NDIS\_QOS\_パラメーター\_*Xxx*\_CHANGED** フラグ**フラグ**のメンバー、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体をローカルの NDIS QoS パラメーターをオーバーライドの理由を指定します。

    ミニポート ドライバーがローカルの QoS パラメーターを管理する方法の詳細については、次を参照してください。 [NDIS QoS パラメーターをローカル設定](setting-local-ndis-qos-parameters.md)します。

    ミニポート ドライバーがその運用上の QoS パラメーターを解決する方法の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを解決する](resolving-operational-ndis-qos-parameters.md)します。

**注**ミニポート ドライバーを発行する必要があります[ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状態インジケーターの NDIS QoS 機能は、現在を有効になっている場合、  **\*QOS**キーワードに標準化された INF キーワード。 詳細については、次を参照してください。[の NDIS QoS の標準化された INF キーワード](standardized-inf-keywords-for-ndis-qos.md)します。

## <a name="guidelines-for-issuing-the-ndisstatusqosoperationalparameterschange-status-indication"></a>NDIS を発行するためのガイドライン\_状態\_QOS\_運用\_パラメーター\_変更状態の表示


発行するとき、ミニポート ドライバーが次の手順を次の[ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状態を示す値。

1.  ミニポート ドライバーでは、以下を格納するのに十分な大きさであるバッファーを割り当てます。

    -   [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters) NDIS QoS の構成設定とグローバルの運用パラメーターの NDIS QoS トラフィック クラスを含む構造体。

    -   配列の[ **NDIS\_QOS\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_classification_element)構造体。 パケット データのパターンで定義されているトラフィックの分類を指定の各構造体 (*条件*) および関連する IEEE 802.1p の優先度レベル (*アクション*)。 ネットワーク アダプター、送信、パターンを検索する場合または*エグレス*条件に一致するパケットの場合、パケットに関連付けられている優先度レベルを割り当てられます。 アダプターでは、他の NDIS QoS ポリシーが優先度レベルに基づいて、パケットにも適用されます。

2.  ミニポートを初期化します、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)運用上の NDIS QoS パラメーターを持つ構造体。 ドライバーは、ネットワーク アダプターで構成されていないこれらのパラメーターを含むオペレーションのパラメーターの完全なセットを提供する必要があります。

    ミニポート ドライバーを初期化します、**ヘッダー**メンバー、設定、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_QOS\_パラメーター。 ミニポート ドライバーのセット、**リビジョン**のメンバー**ヘッダー** NDIS に\_QOS\_パラメーター\_リビジョン\_1 と**サイズ** NDIS メンバー\_SIZEOF\_QOS\_パラメーター\_リビジョン\_1。

    ミニポート ドライバーは、適切な設定**NDIS\_QOS\_パラメーター\_*Xxx*\_CHANGED**のフラグ、 **フラグ**ミニポート driverissued 以降に変更されたデータが対応するメンバーに含まれている場合、メンバー、 [ **NDIS\_状態\_QOS\_OPERATIONAL\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状態を示す値。

    **注**設定、 **NDIS\_QOS\_パラメーター\_*Xxx*\_CHANGED**フラグは省略可能です。 NDIS が常に想定するのメンバー、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)前からに変更されていない場合でも、現在は[ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状態を示す値。

    詳細を設定する方法について、**フラグ**、メンバーを参照してください[設定するためのガイドライン、**フラグ**メンバー](#guidelines-for-setting-the-flags-member)します。

3.  ミニポート ドライバーを初期化します、 [ **NDIS\_QOS\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_classification_element)運用上の NDIS QoS から各トラフィックの分類の構造パラメーター。 ドライバーでは、これらの要素を追加の最後に、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)バッファー内の構造体。

    **注**ミニポート ドライバーは、NDIS を設定する必要がありますいない\_QOS\_分類\_強制\_BY\_ミニポート フラグ、**フラグ**任意のメンバー[**NDIS\_QOS\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_classification_element)構造体。

    ドライバーのセット、 **NumClassificationElements**のメンバー、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体の数配列内の要素を分類します。 ドライバーのセット、 **FirstClassificationElementOffset**バッファーの先頭から最初の要素のバイト オフセットにメンバー。 ドライバーも設定、 **ClassificationElementSize**メンバー配列内の各要素の長さ、(バイト単位)。

    **注意してください**NDIS 6.30 以降、ミニポート ドライバーを設定する必要があります、 **ClassificationElementSize**メンバー `sizeof(NDIS_QOS_CLASSIFICATION_ELEMENT`)。

4.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体の次のように状態の表示。

    -   **StatusCode** NDIS にメンバーを設定する必要があります\_状態\_QOS\_運用\_パラメーター\_変更します。

    -   **StatusBuffer**メンバーは、運用上の NDIS QoS パラメーターを格納しているバッファーへのポインターを設定する必要があります。

    -   **StatusBufferSize**メンバーは、バッファーの長さ、(バイト単位) を設定する必要があります。

5.  ミニポート ドライバーが呼び出すことによって、状態を示す値を発行[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)します。 ドライバーへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体を*StatusIndication*パラメーター。

## <a name="guidelines-for-setting-the-flags-member"></a>フラグのメンバーを設定するためのガイドライン

ミニポート ドライバー、次のフラグを設定する、**フラグ**のメンバー、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体を指定するには運用上の NDIS QoS パラメーターを構成またはネットワーク アダプター上で変更されました。

<a href="" id="ndis-qos-parameters-ets-configured"></a>**NDIS\_QOS\_パラメーター\_ETS\_構成済み**  
このフラグが設定されている場合、ミニポート ドライバーでは、次のメンバーに含まれている ETS パラメーターを使用してネットワーク アダプターが構成します。

-   **NumTrafficClasses**

-   **PriorityAssignmentTable**

-   **TcBandwidthAssignmentTable**

-   **TsaAssignmentTable**

**注**ミニポート ドライバーは、DCB の NDIS QoS をサポートするために ETS をサポートする必要があります。 ただし、このフラグの設定は指定しないかどうか、ネットワーク アダプターは ETS をサポートしています。 代わりに、このフラグの設定を指定しますのみ ETS パラメーターが、ネットワーク アダプターに構成されているかどうか。

<a href="" id="ndis-qos-parameters-ets-changed"></a>**NDIS\_QOS\_パラメーター\_ETS\_CHANGED**  
このフラグが設定されている場合、次のメンバーの 1 つまたは複数の ETS パラメーターが変更されました。

-   **NumTrafficClasses**

-   **PriorityAssignmentTable**

-   **TcBandwidthAssignmentTable**

-   **TsaAssignmentTable**

<a href="" id="ndis-qos-parameters-pfc-configured"></a>**NDIS\_QOS\_パラメーター\_PFC\_構成済み**  
ミニポート ドライバーに含まれる PFC 設定でネットワーク アダプターを構成してこのフラグが設定されている場合、 **PfcEnable**メンバー。

**注**DCB の NDIS QoS をサポートするために、ミニポート ドライバーで PFC をサポートする必要があります。 このフラグの設定は、ネットワーク アダプターが PFC をサポートしているかどうかを指定しません。 代わりに、このフラグの設定を指定しますのみ PFC パラメーターが、ネットワーク アダプターで有効にするかどうか。



<a href="" id="ndis-qos-parameters-pfc-changed"></a>**NDIS\_QOS\_パラメーター\_PFC\_CHANGED**  
1 つまたは複数の PFC 設定では変更がこのフラグが設定されている場合、 **PfcEnable**メンバー。

<a href="" id="ndis-qos-parameters-classification-configured"></a>**NDIS\_QOS\_パラメーター\_分類\_構成済み**  
ミニポート ドライバーがトラフィックの QoS の分類で、ネットワーク アダプターを構成してこのフラグが設定されている場合、次のメンバーで指定されたパラメーター。

-   **NumClassificationElements**

-   **ClassificationElementSize**

-   **FirstClassificationElementOffset**

<a href="" id="ndis-qos-parameters-classification-changed"></a>**NDIS\_QOS\_パラメーター\_分類\_CHANGED**  
このフラグが設定されている場合、次のメンバーの 1 つまたは複数の QoS トラフィック分類パラメーターが変更されました。

-   **NumClassificationElements**

-   **ClassificationElementSize**

-   **FirstClassificationElementOffset**

**注**、 **NDIS\_QOS\_パラメーター\_*Xxx*\_構成済み**場合、フラグを設定する必要があります、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体には、パラメーターの NDIS QoS の設定が含まれています。 ミニポート ドライバーには、設定が変更されたかどうかに関係なく、これらのフラグを設定する必要があります。 ただし、ドライバーを設定する必要があります、 **NDIS\_QOS\_パラメーター\_*Xxx*\_CHANGED**が変更されたこれらの設定のみのフラグ。