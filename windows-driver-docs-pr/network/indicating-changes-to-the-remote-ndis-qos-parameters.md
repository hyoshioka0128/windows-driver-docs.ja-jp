---
title: リモート NDIS QoS パラメーターへの変更の表示
description: リモート NDIS QoS パラメーターへの変更の表示
ms.assetid: E09EBF25-96B6-417F-9538-D0BEBE5B9E19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfab3b63dc9b9720d8ba659ec8eaf33702334688
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824722"
---
# <a name="indicating-changes-to-the-remote-ndis-qos-parameters"></a>リモート NDIS QoS パラメーターへの変更の表示


NDIS Quality of Service (QoS) をサポートするミニポートドライバーは、 [**ndis\_ステータス\_qos\_リモート\_\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を使用して、リモート NDIS QoS パラメーターがピアから最初に受信されたとき、または後で変更されたときに、ステータス表示を変更します。 ミニポートドライバーは、IEEE 802.1 Qaz Data Center ブリッジング Exchange (DCBX) プロトコルを使用して、リモートピアからこれらの QoS パラメーターを受信します。

ミニポートドライバーは、次のガイドラインに従って、 [**NDIS\_ステータス\_QOS\_リモート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行して、状態の表示を変更\_必要があります。

-   ミニポートドライバーがリモートピアから DCBX フレームを受信していない場合は、 [**NDIS\_ステータス\_QOS\_リモート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行して、状態の表示を変更\_ことはできません。

-   ミニポートドライバーは、リモートピアから QoS 設定を最初に受信した後に、 [ **\_リモート\_\_パラメーター\_NDIS\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行する必要があります。

    **メモ** ネットワークアダプターがピアからリモート QoS パラメーター設定を受信してから、ドライバーのローカル QoS パラメーターが設定されている場合、ミニポートドライバーはこの状態を発行する必要があります。 詳細については、「[ローカル NDIS QoS パラメーターの設定](setting-local-ndis-qos-parameters.md)」を参照してください。

-   この初期状態を示すと、ミニポートドライバーは、リモートピアの QoS 設定の変更を判断したときに、 [ **\_qos\_リモート\_\_パラメーターの NDIS\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)のみを発行する必要があります。

    **メモ** ミニポートドライバーは、リモートの NDIS QoS パラメーターが変更されていない場合に、 [**QOS\_リモート\_\_パラメーター\_、ndis\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行しないようにする必要があります。 ドライバーがこの種類の状態を示している場合、NDIS は、このような指示を後続のドライバーに渡すことはできません。

**メモ** ミニポートドライバーは、ndis QoS 機能が現在有効になっている場合に、 [ **\_リモート\_\_パラメーター\_、ndis\_ステータス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行して、状態のインジケーターを変更する必要があります。 Windows Server 2012 以降では、システム管理者は、Microsoft DCB Server 機能がインストールされているかどうかに関係なく、NDIS QoS およびデータセンターブリッジング (DCB) の設定を表示できます。



## <a name="guidelines-for-issuing-the-ndis_status_qos_remote_parameters_change-status-indication"></a>NDIS\_ステータス\_QOS\_リモート\_パラメーターを発行するためのガイドライン\_変更の状態の表示


ミニポートドライバーは、次の手順に従って、 [**NDIS\_ステータス\_QOS\_リモート\_\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行すると、状態の表示が変更されます。

1.  ミニポートドライバーは、次のものを格納するのに十分な大きさのバッファーを割り当てます。

    -   Ndis qos の構成設定を含む ndis [ **\_qos\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造と、ndis qos traffic classes のグローバルな操作パラメーター。

    -   [**NDIS\_QOS\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)構造の配列。 これらの各構造体は、パケットデータパターン (*条件*) と関連付けられている IEEE 802.1 p の優先度レベル (*action*) によって定義されたトラフィックの分類を指定します。 ネットワークアダプターが、条件に一致する送信*パケットまたは*送信パケット内のパターンを検出すると、関連付けられている優先度レベルをパケットに割り当てます。 また、アダプターは、優先度レベルに基づいて、他の NDIS QoS ポリシーをパケットに適用します。

2.  ミニポートは、 [**ndis\_qos\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体をリモート ndis qos パラメーターを使用して初期化します。 ドライバーは、リモートピアによって送信された DCBX フレームから受信したリモートパラメーターの完全なセットを提供する必要があります。

    ミニポートドライバーは、**ヘッダー**メンバーを初期化するときに、**ヘッダー**の**TYPE**メンバーを NDIS\_OBJECT\_type\_QOS\_PARAMETERS に設定します。 ミニポートドライバーは、**ヘッダー**の**リビジョン**メンバーを NDIS\_QOS\_パラメーター\_リビジョン\_1、 **SIZE**メンバーを NDIS\_SIZEOF\_qos\_パラメーター\_リビジョン\_1 に設定します。

    ミニポートドライバーでは、適切な**ndis\_qos\_パラメーター\_*XXX*\_変更**されたフラグが設定されます。対応するメンバーには、以前に[**ndis\_status**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行した後で変更されたデータが含まれています。\_\_\_\_

    **メモ**  これらの**NDIS\_QOS\_パラメーターの設定\_*XXX*\_変更された**フラグは省略可能です。 Ndis は常に、ndis の[ **\_qos\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)のメンバーが、以前の[**ndis\_の\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)から変更されていない場合でも指定されていることを前提としています。\_\_

    ミニポートドライバーは、**フラグ**メンバーを設定して、 [**NDIS\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体のメンバーに含まれるデータの状態情報を指定します。

    たとえば、ミニポートドライバーによって、適切な**ndis\_qos\_パラメーター\_*XXX*\_変更**されたデータを含むメンバーの**フラグ**が設定されています。これらのメンバーには、以前に[**ndis\_状態\_qos\_リモート\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)されたデータが含まれています。

    **Flags**メンバーを設定する方法の詳細については、「 [ **flags**メンバーを設定するためのガイドライン](#guidelines-for-setting-the-flags-member)」を参照してください。

3.  ミニポートドライバーは、リモート NDIS QoS パラメーターからのトラフィック分類ごとに、 [**ndis\_QOS\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)構造を初期化します。 ドライバーは、これらの要素を、 [**NDIS\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体の末尾を越えてバッファーに追加します。

    **メモ** ミニポートドライバーでは、ndis\_QOS の\_分類\_\_設定しないでください。\_ミニポートフラグによって、任意の[**ndis\_qos\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)構造の**フラグ**メンバーになります。

    このドライバーは、 [**NDIS\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体の**NumClassificationElements**メンバーに、配列内の分類要素の数を設定します。 ドライバーは、バッファーの先頭からの最初の要素のバイトオフセットに**FirstClassificationElementOffset**メンバーを設定します。 また、ドライバーは、配列内の各要素の長さ (バイト単位) に**ClassificationElementSize**メンバーを設定します。

    **メモ** NDIS 6.30 以降では、ミニポートドライバーは**ClassificationElementSize**メンバーを `sizeof(NDIS_QOS_CLASSIFICATION_ELEMENT`) に設定する必要があります。

4.  ミニポートドライバーは、次の方法で状態を示すように、 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体を初期化します。

    -   **StatusCode**メンバーを NDIS\_STATUS\_QOS\_リモート\_パラメーター\_変更に設定する必要があります。

    -   **Statusbuffer**メンバーは、リモート NDIS QoS パラメーターを含むバッファーへのポインターに設定する必要があります。

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

**メモ** Ndis [ **\_qos\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造に ndis QOS パラメーターの設定が含まれている場合は、 **ndis\_qos\_パラメーター\_*Xxx*\_構成さ**れたフラグを設定する必要があります。 ミニポートドライバーは、設定が変更されたかどうかに関係なく、これらのフラグを設定する必要があります。 ただし、ドライバーでは、変更された設定に対して、変更されたフラグ\_Xxx\_変更された場合にのみ、 **NDIS\_QOS\_パラメーター** を設定する必要があります。

## <a name="guidelines-for-indicating-invalid-remote-ndis-qos-parameters"></a>無効なリモート NDIS QoS パラメーターを示すガイドライン


次の条件に該当する場合、ミニポートドライバーはリモート QoS パラメーターを無効にする必要があります。

-   有効期限 (TTL) の値は、リモート QoS パラメーターの有効期限が切れます。

    **メモ** DCBX は、IEEE 802.1 AB-2005 標準で指定されているように、リンクレイヤー検出プロトコル (LLDP) プロトコルを介して実行されます。 LLDP フレームには、常に TTL フィールドが含まれます。

-   別のデータリンクピアが、TTL 値の有効期限が切れる前に DCBX フレームを送信します。 このシナリオは、*マルチピア*条件と呼ばれます。 DCBX を行うには、ミニポートドライバーが1つのデータリンクピアから受信したリモート QoS パラメーターのセットを1つだけ保持する必要があります。

    マルチピア状態が発生した場合、受信したすべての DCBX フレームの TTL 値が期限切れになるまで、ミニポートドライバーはすべてのリモート QoS パラメーターを無効にする必要があります。

ミニポートドライバーがリモート NDIS QoS パラメーターを無効にした場合は、次の手順に従って、 [**ndis\_ステータス\_QoS\_リモート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行して、状態の表示\_変更する必要があります。

1.  ミニポートドライバーは有効なリモート NDIS QoS パラメーターを報告しないため、最初に[**ndis\_QoS\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体にゼロを入力する必要があります。

    ミニポートドライバーは、この構造体の**ヘッダー**メンバーを初期化するときに、**ヘッダー**の**型**メンバーを NDIS\_OBJECT\_type\_QOS\_PARAMETERS に設定します。 ミニポートドライバーは、**ヘッダー**の**リビジョン**メンバーを NDIS\_QOS\_パラメーター\_リビジョン\_1、 **SIZE**メンバーを NDIS\_SIZEOF\_qos\_パラメーター\_リビジョン\_1 に設定します。

    ミニポートドライバーでは、適切な**NDIS\_QOS\_パラメーター\_*XXX*\_変更された**フラグを**フラグ**メンバーに設定します。

2.  ミニポートドライバーは、次の方法で状態を示すように、 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体を初期化します。

    -   **StatusCode**メンバーを NDIS\_STATUS\_QOS\_リモート\_パラメーター\_変更に設定する必要があります。

    -   **Statusbuffer**メンバーは、 [**NDIS\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体のアドレスに設定する必要があります。

    -   **Statusbuffersize**メンバーを `sizeof(NDIS_QOS_PARAMETERS)`に設定する必要があります。

3.  ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出すことによって状態を示します。 ドライバーは、 [**NDIS\_STATUS\_を示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)ポインターを*statusindication*パラメーターに渡す必要があります。