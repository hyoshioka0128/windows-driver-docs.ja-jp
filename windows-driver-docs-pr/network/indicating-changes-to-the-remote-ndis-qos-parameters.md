---
title: リモートの NDIS QoS パラメーターへの変更を示す
description: リモートの NDIS QoS パラメーターへの変更を示す
ms.assetid: E09EBF25-96B6-417F-9538-D0BEBE5B9E19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8e0875d66834c76750e75b0025cf5c1a35f462b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531355"
---
# <a name="indicating-changes-to-the-remote-ndis-qos-parameters"></a>リモートの NDIS QoS パラメーターへの変更を示す


NDIS サービスの品質 (QoS) の問題をサポートしているミニポート ドライバー、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)そのリモートの NDIS QoS パラメーターは、最初に、ピアから受信したか、または後で変更するときの状態を示す値。 ミニポート ドライバーでは、これらの QoS パラメーターを受け取る IEEE 802.1 qaz を通じてリモート ピアから Data Center Bridging Exchange (DCBX) プロトコル。

ミニポート ドライバーが発行するための次のガイドラインに従う必要があります、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態を示す値。

-   発行する必要があります、ミニポート ドライバーは、リモート ピアから DCBX フレームを受信しないが場合、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態を示す値。

-   ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)後の状態の表示リモート ピアから、QoS の設定が最初に受信します。

    **注**ネットワーク アダプターは、ドライバーのローカルの QoS パラメーターを設定する前に、ピアからリモートの QoS パラメーター設定を受信する場合、ミニポート ドライバーはこの状態を示す値を発行する必要があります。 詳細については、[NDIS QoS パラメーターをローカル設定](setting-local-ndis-qos-parameters.md)を参照してください。

-   この最初の状態を示す値を後に、ミニポート ドライバーを発行するのみ、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)リモート ピアの QoS の設定の変更を決定する場合の状態を示す値。

    **注**ミニポート ドライバーが発行する必要があります、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態の表示がないリモートの NDIS QoS パラメーターを変更する場合。 場合は、ドライバーはこの種類の状態表示するには、NDIS が重なってドライバーを示す値を渡すことができません。

**注**ミニポート ドライバーを発行する必要があります[ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態インジケーターの NDIS QoS 機能が現在有効になっている場合。 Windows Server 2012 以降では、これらの問題は、NDIS QoS と DCB の Microsoft サーバーの機能がインストールされているかどうかに関係なくデータ センター ブリッジング (DCB) の設定を表示するシステム管理者を使用できます。



## <a name="guidelines-for-issuing-the-ndisstatusqosremoteparameterschange-status-indication"></a>NDIS を発行するためのガイドライン\_状態\_QOS\_リモート\_パラメーター\_変更状態の表示


発行するとき、ミニポート ドライバーが次の手順を次の[ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態を示す値。

1.  ミニポート ドライバーでは、以下を格納するのに十分な大きさであるバッファーを割り当てます。

    -   [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640) NDIS QoS の構成設定とグローバルの運用パラメーターの NDIS QoS トラフィック クラスを含む構造体。

    -   配列の[ **NDIS\_QOS\_分類\_要素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)構造体。 パケット データのパターンで定義されているトラフィックの分類を指定の各構造体 (*条件*) および関連する IEEE 802.1p の優先度レベル (*アクション*)。 ネットワーク アダプター、送信、パターンを検索する場合または*エグレス*条件に一致するパケットの場合、パケットに関連付けられている優先度レベルを割り当てられます。 アダプターでは、他の NDIS QoS ポリシーが優先度レベルに基づいて、パケットにも適用されます。

2.  ミニポートを初期化します、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)リモートの NDIS QoS パラメーターを持つ構造体。 ドライバーには、リモート ピアから送信された DCBX フレームから受信したリモートのパラメーターの完全なセットを指定する必要があります。

    ミニポート ドライバーを初期化します、**ヘッダー**メンバー、設定、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_QOS\_パラメーター。 ミニポート ドライバーのセット、**リビジョン**のメンバー**ヘッダー** NDIS に\_QOS\_パラメーター\_リビジョン\_1 と**サイズ** NDIS メンバー\_SIZEOF\_QOS\_パラメーター\_リビジョン\_1。

    ミニポート ドライバーは、適切な設定**NDIS\_QOS\_パラメーター\_*Xxx*\_CHANGED**フラグの対応するメンバーには、データが含まれている場合ミニポート ドライバーを以前に発行された後に変更された、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態を示す値。

    **注**これらの設定**NDIS\_QOS\_パラメーター\_*Xxx*\_CHANGED**フラグは省略可能です。 NDIS が常に想定するのメンバー、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)前からに変更されていない場合でも指定[ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態を示す値。

    ミニポート ドライバーのセット、**フラグ**に含まれているデータの状態情報を指定するにはメンバー、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)メンバー構造体します。

    たとえば、ミニポート ドライバーは、適切な設定**NDIS\_QOS\_パラメーター\_*Xxx*\_CHANGED**のフラグ、 **フラグ**ミニポート ドライバーを以前に発行された後に変更されたデータが含まれているこれらのメンバーのメンバー、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態を示す値。

    詳細を設定する方法について、**フラグ**、メンバーを参照してください[設定するためのガイドライン、**フラグ**メンバー](#flags)します。

3.  ミニポート ドライバーを初期化します、 [ **NDIS\_QOS\_分類\_要素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)からリモートの NDIS QoS には、各トラフィック種類の構造パラメーター。 ドライバーにより、これらの要素の末尾を越えた、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)バッファー内の構造体。

    **注**ミニポート ドライバーは、NDIS を設定する必要がありますいない\_QOS\_分類\_強制\_BY\_ミニポート フラグ、**フラグ**任意のメンバー[**NDIS\_QOS\_分類\_要素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)構造体。

    ドライバーのセット、 **NumClassificationElements**のメンバー、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体の数配列内の要素を分類します。 ドライバーのセット、 **FirstClassificationElementOffset**バッファーの先頭から最初の要素のバイト オフセットにメンバー。 ドライバーも設定、 **ClassificationElementSize**メンバー配列内の各要素の長さ、(バイト単位)。

    **注意してください**NDIS 6.30 以降、ミニポート ドライバーを設定する必要があります、 **ClassificationElementSize**メンバー `sizeof(NDIS_QOS_CLASSIFICATION_ELEMENT`)。

4.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体の次のように状態の表示。

    -   **StatusCode** NDIS にメンバーを設定する必要があります\_状態\_QOS\_リモート\_パラメーター\_変更します。

    -   **StatusBuffer**メンバーは、リモートの NDIS QoS パラメーターを格納しているバッファーへのポインターを設定する必要があります。

    -   **StatusBufferSize**メンバーは、バッファーの長さ、(バイト単位) を設定する必要があります。

5.  ミニポート ドライバーが呼び出すことによって、状態を示す値を発行[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)します。 ドライバーへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体を*StatusIndication*パラメーター。

## <a name="guidelines-for-setting-the-flags-member"></a>フラグのメンバーを設定するためのガイドライン

ミニポート ドライバー、次のフラグを設定する、**フラグ**のメンバー、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体を指定するには運用上の NDIS QoS パラメーターを構成またはネットワーク アダプター上で変更されました。

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

**注**、 **NDIS\_QOS\_パラメーター\_*Xxx*\_構成済み**場合、フラグを設定する必要があります、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体には、パラメーターの NDIS QoS の設定が含まれています。 ミニポート ドライバーには、設定が変更されたかどうかに関係なく、これらのフラグを設定する必要があります。 ただし、ドライバーを設定する必要がありますのみ、 **NDIS\_QOS\_パラメーター\_*Xxx*\_CHANGED**フラグが変更されたこれらの設定をします。

## <a name="guidelines-for-indicating-invalid-remote-ndis-qos-parameters"></a>無効なリモートの NDIS QoS パラメーターを示すためのガイドライン


ミニポート ドライバーは、次の条件に該当する場合、そのリモートの QoS パラメーターを無効にする必要があります。

-   有効期限 (TTL) 値では、QoS パラメーターをリモートの有効期限が切れます。

    **注**IEEE 802.1AB で指定されているリンク層探索プロトコル (LLDP) プロトコルが引き継がれます DCBX-2005 standard。 LLDP フレームには、常に TTL フィールドが含まれます。

-   TTL の値の有効期限が切れる前に、別のデータ リンク ピアは DCBX フレームを送信します。 このシナリオと呼ばれる、*マルチ ピア*条件。 DCBX では、ミニポート ドライバーが 1 つのデータ リンクのピアから受信したリモートの QoS パラメーターの 1 つだけのセットを維持する必要があります。

    複数のピアの状況が発生したときに TTL 値は、受信 DCBX フレームのすべての有効期限が切れるまで、ミニポート ドライバーが QoS パラメーターをリモートのすべてを無効する必要があります。

発行するときにする必要がありますのミニポート ドライバーには、そのリモートの NDIS QoS パラメーターが無効になります、ときに次の手順に従って、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態を示す値。

1.  入力する必要があります最初、ミニポート ドライバーが、有効なリモートの NDIS QoS パラメーターを報告していないため、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)ゼロの構造体。

    ミニポート ドライバーを初期化すると、**ヘッダー**この構造体のメンバーは、設定、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_QOS\_パラメーター。 ミニポート ドライバーのセット、**リビジョン**のメンバー**ヘッダー** NDIS に\_QOS\_パラメーター\_リビジョン\_1 と**サイズ** NDIS メンバー\_SIZEOF\_QOS\_パラメーター\_リビジョン\_1。

    ミニポート ドライバーは、適切な設定**NDIS\_QOS\_パラメーター\_*Xxx*\_CHANGED**のフラグ、 **フラグ**メンバー。

2.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体の次のように状態の表示。

    -   **StatusCode** NDIS にメンバーを設定する必要があります\_状態\_QOS\_リモート\_パラメーター\_変更します。

    -   **StatusBuffer**メンバーのアドレスに設定する必要があります、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体。

    -   **StatusBufferSize**にメンバーを設定する必要があります`sizeof(NDIS_QOS_PARAMETERS)`します。

3.  ミニポート ドライバーが呼び出すことによって、状態を示す値を発行[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)します。 ドライバーへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体を*StatusIndication*パラメーター。