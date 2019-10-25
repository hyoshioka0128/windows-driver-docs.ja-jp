---
title: 稼働中の NDIS QoS パラメーターへの変更の表示
description: 稼働中の NDIS QoS パラメーターへの変更の表示
ms.assetid: BAE99C83-2732-4216-BC49-23F541AA3F10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 575876f14ba851747a6037e2215c65365cadb905
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824718"
---
# <a name="indicating-changes-to-the-operational-ndis-qos-parameters"></a>稼働中の NDIS QoS パラメーターへの変更の表示


NDIS Quality of Service (QoS) をサポートするミニポートドライバーでは、 [**ndis\_の状態\_qos\_operational\_\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)に関する問題が発生し、ドライバーの運用 NDIS QoS パラメーターが最初の実行時、または後で変更されたときに解決されます。 ミニポートドライバーは、これらの操作パラメーターを使用してネットワークアダプターを構成し、QoS パケット転送を実行します。

ミニポートドライバーは、次のガイドラインに従って、 [**NDIS\_状態\_QOS\_操作\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)に発行し、状態の表示を変更\_必要があります。

-   ミニポートドライバーは、 [**ndis\_の状態\_QOS\_操作\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)を発行する必要があります。また、動作している ndis QOS パラメーターを解決してネットワークアダプターを構成した後に、状態の変更を通知\_.

    **メモ** ミニポートドライバーが、レジストリ内に独自のローカル NDIS QoS パラメーターを使用してプロビジョニングされている場合、ドライバーは、またはの実行中に[ **\_QoS\_操作\_\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)を使用して、\_状態の通知を発行する必要があります。[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)の呼び出しの直後。 この場合、ドライバーは、独自のローカル NDIS QoS パラメーター設定を使用して、 [**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体を初期化します。

    ドライバーが動作している NDIS QoS パラメーター設定を解決する方法の詳細については、「[運用 Ndis Qos パラメーターの解決](resolving-operational-ndis-qos-parameters.md)」を参照してください。

-   この初期状態を示すと、ミニポートドライバーは、 [**ndis\_の状態\_QOS\_操作\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)を発行し、動作している ndis QOS パラメーターが変更されたときに状態を変更\_します。 たとえば、次のような状況では、運用 NDIS QoS パラメーターが変更される可能性があります。

    -   ローカル NDIS QoS パラメーターが変更されたため、operational NDIS QoS パラメーターが変更されます。 これらのパラメーターは、Oid の oid メソッド要求、 [\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters) 、または独立系ハードウェアベンダー (IHV) によって開発された管理アプリケーションによって変更される可能性があります。

    -   リモートピアからの QoS 設定との競合が原因で、operational NDIS QoS パラメーターが変更されています。

        ミニポートドライバーは、IEEE 802.1 Qaz Data Center ブリッジング Exchange (DCBX) プロトコルを使用して、リモートピアの QoS パラメーターを検出します。 DCBX の状態が有効になっている場合、ドライバーは、DCBX 状態エンジンに対して定義されている手順に従って、QoS パラメーターとリモートピアの QoS パラメーターの違いを解決する必要があります。 この状態エンジンの詳細については、「IEEE 802.1 Qaz draft standard」を参照してください。

        ローカルの DCBX の状態の詳細については、「[ローカルの dcbx の状態の管理](managing-the-local-dcbx-willing-state.md)」を参照してください。

    **メモ** ミニポートドライバーがローカルまたはリモートの NDIS QoS パラメーターを受信する場合、 [**ndis\_の状態\_qos\_操作\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)には発行しないでください。変更がない場合は、状態の変更を通知\_運用 NDIS QoS パラメーター。 ドライバーによってこのような不要な状態が示された場合、NDIS では、表示されていないドライバーを渡すことはできません。

-   ミニポートドライバーは、 [**ndis\_ステータス\_QOS\_操作\_\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)を発行する必要があります。また、運用 ndis の解決に使用されたローカルの NDIS QOS パラメーターを上書きする必要がある場合は、変更状態を示します。QoS パラメーター。

    ミニポートドライバーは、ndis およびそれ以降のドライバーに対して、ndis [ **\_ステータス\_QoS\_操作\_\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)を発行して、ローカル ndis QoS パラメーターを上書きしたことを通知します。 この種の兆候を示すために、ドライバーは、 [**ndis\_qos\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体の**flags**メンバーで、適切な**ndis\_qos\_パラメーター\_*Xxx*\_変更され**たフラグを設定する必要があります。ローカル NDIS QoS パラメーターを上書きする理由を指定します。

    ミニポートドライバーでローカルの QoS パラメーターを管理する方法の詳細については、「[ローカル NDIS Qos パラメーターの設定](setting-local-ndis-qos-parameters.md)」を参照してください。

    ミニポートドライバーが動作する QoS パラメーターを解決する方法の詳細については、「[運用 NDIS Qos パラメーターの解決](resolving-operational-ndis-qos-parameters.md)」を参照してください。

**メモ** ミニポートドライバーは、ndis [ **\_ステータス\_qos\_操作\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)を発行する必要があります。 **\_qos**キーワードを使用して ndis QOS 機能が現在有効になっている場合は、状態のインジケーターを変更\*標準化された INF キーワード。 詳細については、「 [NDIS QoS の標準化](standardized-inf-keywords-for-ndis-qos.md)された INF キーワード」を参照してください。

## <a name="guidelines-for-issuing-the-ndis_status_qos_operational_parameters_change-status-indication"></a>NDIS\_ステータス\_QOS\_操作\_パラメーターを発行するためのガイドライン\_変更の状態の表示


ミニポートドライバーは、次の手順に従って、 [**NDIS\_ステータス\_QOS\_操作\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)を発行すると、状態の表示が変更さ\_ます。

1.  ミニポートドライバーは、次のものを格納するのに十分な大きさのバッファーを割り当てます。

    -   Ndis qos の構成設定を含む ndis [ **\_qos\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造と、ndis qos traffic classes のグローバルな操作パラメーター。

    -   [**NDIS\_QOS\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)構造の配列。 これらの各構造体は、パケットデータパターン (*条件*) と関連付けられている IEEE 802.1 p の優先度レベル (*action*) によって定義されたトラフィックの分類を指定します。 ネットワークアダプターが、条件に一致する送信*パケットまたは*送信パケット内のパターンを検出すると、関連付けられている優先度レベルをパケットに割り当てます。 また、アダプターは、優先度レベルに基づいて、他の NDIS QoS ポリシーをパケットに適用します。

2.  ミニポートは、 [**ndis\_qos\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体を、運用 ndis qos パラメーターを使用して初期化します。 ドライバーは、ネットワークアダプターで構成されていない可能性があるパラメーターを含む、操作パラメーターの完全なセットを提供する必要があります。

    ミニポートドライバーは、**ヘッダー**メンバーを初期化するときに、**ヘッダー**の**TYPE**メンバーを NDIS\_OBJECT\_type\_QOS\_PARAMETERS に設定します。 ミニポートドライバーは、**ヘッダー**の**リビジョン**メンバーを NDIS\_QOS\_パラメーター\_リビジョン\_1、 **SIZE**メンバーを NDIS\_SIZEOF\_qos\_パラメーター\_リビジョンに設定します。\_1 です。

    ミニポートドライバーは、対応するメンバーに、ミニポート driverdriverが発行されてから変更されたデータが含まれている場合に、適切な**NDIS\_QOS\_パラメーター\_*XXX*\_変更**され**たフラグを**設定します。[**NDIS\_ステータス\_QOS\_操作\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)の状態の表示を示します。

    **メモ**  **NDIS\_QOS\_パラメーターの設定\_*XXX*\_変更された**フラグは省略可能です。 Ndis では常に、前の[**ndis\_の\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)から QOS\_パラメーターを変更していない場合でも、NDIS [ **\_qos**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)のメンバーが最新であることを前提としています。状態を示します。

    **Flags**メンバーを設定する方法の詳細については、「 [ **flags**メンバーを設定するためのガイドライン](#guidelines-for-setting-the-flags-member)」を参照してください。

3.  ミニポートドライバーは、運用 NDIS QoS パラメーターからのトラフィック分類ごとに、 [**ndis\_qos\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)構造を初期化します。 ドライバーは、これらの要素を、 [**NDIS\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体の最後にバッファーに追加します。

    **メモ** ミニポートドライバーでは、ndis\_QOS の\_分類\_\_設定しないでください。\_ミニポートフラグによって、任意の[**ndis\_qos\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)構造の**フラグ**メンバーになります。

    このドライバーは、 [**NDIS\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体の**NumClassificationElements**メンバーに、配列内の分類要素の数を設定します。 ドライバーは、バッファーの先頭からの最初の要素のバイトオフセットに**FirstClassificationElementOffset**メンバーを設定します。 また、ドライバーは、配列内の各要素の長さ (バイト単位) に**ClassificationElementSize**メンバーを設定します。

    **メモ** NDIS 6.30 以降では、ミニポートドライバーは**ClassificationElementSize**メンバーを `sizeof(NDIS_QOS_CLASSIFICATION_ELEMENT`) に設定する必要があります。

4.  ミニポートドライバーは、次の方法で状態を示すように、 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体を初期化します。

    -   **StatusCode**メンバーを NDIS\_\_STATUS に設定し、QOS\_OPERATIONAL\_PARAMETERS\_CHANGE に設定する必要があります。

    -   **Statusbuffer**メンバーは、Operational NDIS QoS パラメーターを含むバッファーへのポインターに設定する必要があります。

    -   **Statusbuffersize**メンバーは、バッファーの長さ (バイト単位) に設定する必要があります。

5.  ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出すことによって状態を示します。 ドライバーは、 [**NDIS\_STATUS\_を示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)ポインターを*statusindication*パラメーターに渡す必要があります。

## <a name="guidelines-for-setting-the-flags-member"></a>Flags メンバーを設定するためのガイドライン

ミニポートドライバーは、 [**ndis\_qos\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体の**flags**メンバーに次のフラグを設定して、ネットワークアダプターで構成または変更されたオペレーション NDIS qos パラメーターを指定します。

<a href="" id="ndis-qos-parameters-ets-configured"></a>**構成\_構成されている NDIS\_QOS\_パラメーター\_**  
このフラグが設定されている場合、ミニポートドライバーは、次のメンバーに含まれているパラメーターを使用してネットワークアダプターを構成しています。

-   **NumTrafficClasses**

-   **優先順位のテーブル**

-   **TcBandwidthAssignmentTable**

-   **Tsaのテーブル**

**メモ** ミニポートドライバーは、DCB の NDIS QoS をサポートするために、の使用をサポートする必要があります。 ただし、このフラグの設定では、ネットワークアダプターが設定をサポートするかどうかは指定されません。 代わりに、このフラグの設定では、ネットワークアダプター上でのパラメーターの設定が構成されているかどうかのみを指定します。

<a href="" id="ndis-qos-parameters-ets-changed"></a>**NDIS\_QOS\_パラメーター\_変更\_変更**  
このフラグが設定されている場合、次のメンバーで1つ以上のパラメーターが変更されています。

-   **NumTrafficClasses**

-   **優先順位のテーブル**

-   **TcBandwidthAssignmentTable**

-   **Tsaのテーブル**

<a href="" id="ndis-qos-parameters-pfc-configured"></a>**NDIS\_QOS\_パラメーター\_PFC\_構成済み**  
このフラグが設定されている場合、ミニポートドライバーは、 **Pfcenable**メンバーに含まれている pfc 設定を使用してネットワークアダプターを構成しています。

**メモ** ミニポートドライバーは、DCB の NDIS QoS をサポートするために、PFC をサポートする必要があります。 このフラグの設定では、ネットワークアダプターが PFC をサポートするかどうかは指定されません。 このフラグの設定では、ネットワークアダプターで PFC パラメーターが有効になっているかどうかのみを指定します。



<a href="" id="ndis-qos-parameters-pfc-changed"></a>**NDIS\_QOS\_パラメーター\_PFC\_変更されました**  
このフラグが設定されている場合、 **Pfcenable**メンバーで1つまたは複数の pfc 設定が変更されています。

<a href="" id="ndis-qos-parameters-classification-configured"></a>**NDIS\_QOS\_パラメーター\_分類\_構成済み**  
このフラグが設定されている場合、ミニポートドライバーは、次のメンバーに指定されている QoS トラフィック分類パラメーターを使用してネットワークアダプターを構成しています。

-   **NumClassificationElements**

-   **ClassificationElementSize**

-   **FirstClassificationElementOffset**

<a href="" id="ndis-qos-parameters-classification-changed"></a>**NDIS\_QOS\_パラメーター\_分類\_変更されました**  
このフラグが設定されている場合、次のメンバーで1つまたは複数の QoS トラフィック分類パラメーターが変更されています。

-   **NumClassificationElements**

-   **ClassificationElementSize**

-   **FirstClassificationElementOffset**

**メモ** Ndis [ **\_qos\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造に ndis QOS パラメーターの設定が含まれている場合は、 **ndis\_qos\_パラメーター\_*Xxx*\_構成さ**れたフラグを設定する必要があります。 ミニポートドライバーは、設定が変更されたかどうかに関係なく、これらのフラグを設定する必要があります。 ただし、ドライバーでは、変更された設定に対してのみ、 **NDIS\_QOS\_パラメーター\_*XXX*\_変更さ**れたフラグを設定する必要があります。