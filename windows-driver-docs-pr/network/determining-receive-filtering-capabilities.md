---
title: 受信フィルター機能の判断
description: 受信フィルター機能の判断
ms.assetid: 11EE5987-A2DE-4388-86D0-77285453E80A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba9ee2381a71c34cfb91a5ed34deac818c31033e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838144"
---
# <a name="determining-receive-filtering-capabilities"></a>受信フィルター機能の判断


このトピックでは、NDIS およびそれ以降のドライバーが、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターの受信フィルター処理機能をどのように決定するかについて説明します。 このトピックの内容は次のとおりです。

[*MiniportInitializeEx*中の受信フィルター機能の報告](#reporting-receive-filtering-capabilities-during-miniportinitializeex)

[別のドライバーによる受信フィルター処理機能のクエリ](#querying-receive-filtering-capabilities-by-overlying-drivers)

**注**  は、sr-iov ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーだけが受信フィルター機能を報告できます。 PCIe 仮想機能 (VFs) のミニポートドライバーは、SR-IOV アダプターの受信フィルター処理機能を報告しないようにする必要があります。

 

## <a name="reporting-receive-filtering-capabilities-during-miniportinitializeex"></a>*MiniportInitializeEx*中の受信フィルター機能の報告


NDIS が PF ミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ドライバーは次の受信フィルター機能を提供します。

-   ネットワークアダプターがサポートできる完全なハードウェア受信フィルター機能。

-   ネットワークアダプターで現在有効になっているインターフェイスの受信フィルター処理機能。

ミニポートドライバーは、基になるネットワークアダプターの完全なハードウェア受信フィルター機能を、次のように初期化された[ **\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を持つ NDIS\_受信します。

1.  ミニポートドライバーは、**ヘッダー**メンバーを初期化します。 ドライバーは、**ヘッダー**の**type**メンバーを、既定\_\_型の NDIS\_OBJECT に設定します。

    NDIS 6.30 以降では、ミニポートドライバーは**ヘッダー**の**リビジョン**メンバーを NDIS\_受信\_フィルター\_機能\_リビジョン\_2 および**SIZE**メンバーを ndis\_SIZEOF に設定\_\_リビジョン\_2\_機能を受信\_フィルター処理します。

2.  ミニポートドライバーは、NDIS の他のメンバー [ **\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を、sr-iov ネットワークアダプターの受信フィルター機能の値の範囲に設定します。 たとえば、ミニポートドライバーは、対応するフラグを**Supportedfiltertests**に設定して、ミニポートドライバーがサポートするフィルターテスト操作を指定します。

3.  Sr-iov 以外にも、受信フィルター処理は次のインターフェイスで使用されます。

    -   [NDIS パケット合体](ndis-packet-coalescing.md)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[パケット合体受信フィルターの管理](managing-packet-coalescing-receive-filters.md)」を参照してください。

    -   [仮想マシン キュー (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「 [VMQ フィルターの設定とクリア](setting-and-clearing-vmq-filters.md)」を参照してください。

    ミニポートドライバーがこれらのインターフェイスのいずれかをサポートしている場合は、 [**NDIS\_receive\_FILTER\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造体のメンバーに、インターフェイスに固有の受信フィルター機能の値の範囲を設定する必要があります。 たとえば、ドライバーが NDIS パケット合体と sr-iov をサポートしている場合は、次のように、 **\_既定の\_キューフラグに\_サポートされている\_を\_フィルター\_パケット\_合体するように ndis\_受信するように設定する必要があります。SupportedQueueProperties**メンバー。

ミニポートドライバーは、基になるネットワークアダプターの現在有効な受信フィルター機能を、次の方法で初期化される[**NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を通じて報告します。

1.  ミニポートドライバーは、**ヘッダー**メンバーを初期化します。 ドライバーは、**ヘッダー**の**type**メンバーを、既定\_\_型の NDIS\_OBJECT に設定します。

    NDIS 6.30 以降では、ミニポートドライバーは**ヘッダー**の**リビジョン**メンバーを NDIS\_受信\_フィルター\_機能\_リビジョン\_2 および**SIZE**メンバーを ndis\_SIZEOF に設定\_\_リビジョン\_2\_機能を受信\_フィルター処理します。

2.  ミニポートドライバーは、NDIS の他のメンバー [ **\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を、現在有効になっているインターフェイスの受信フィルター処理機能の値の範囲に設定します。 たとえば、NDIS パケット合体が有効になっている場合、ドライバーは、このテクノロジに固有のメンバーのみを設定する必要があります。

    受信フィルター処理を使用するインターフェイスは、標準化された INF キーワードによって有効または無効になります。 NDIS パケット合体を有効にする方法の詳細については、「[パケット合体用の標準化](standardized-inf-keywords-for-packet-coalescing.md)された INF キーワード」を参照してください。 Sr-iov と VMQ を有効にする方法の詳細については、「sr-iov [、vmq、RSS の標準化](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)された INF キーワードの処理」を参照してください。

NDIS がミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ドライバーは次の手順に従ってネットワークアダプターの受信フィルター処理機能を登録します。

1.  ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の構造を初期化します。

    ミニポートドライバーは、 **HardwareReceiveFilterCapabilities**メンバーを、[**受信\_フィルター\_機能の構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)のアドレスに設定します。 この構造体は、ネットワークアダプターの完全なハードウェア受信フィルター機能を使用して以前に初期化されています。

2.  VMQ、SR-IOV、および NDIS パケット合体がすべて、ネットワークアダプターで現在無効になっている場合、ミニポートドライバーは**Currentreceivefiltercapabilities**メンバーを NULL に設定します。

3.  VMQ、SR-IOV、または NDIS パケット合体がネットワークアダプターで現在有効になっている場合、ミニポートドライバーは次の操作を行う必要があります。

    -   ミニポートドライバーは、ネットワークアダプターで現在有効になっているインターフェイスの現在の受信フィルター処理機能を使用して、別の[**NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を初期化する必要があります。

        SR-IOV インターフェイスが有効になっている場合は、ミニポートドライバーが、 [ **\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造を同じまたは別の値に受信するために、NDIS\_のメンバーを設定する必要がある場合があります。 SR-IOV インターフェイスは、VMQ と同様のキューメカニズムを提供しますが、VM 受信キューではなく仮想ポート (VPorts) を使用するためです。

        たとえば、VMQ または sr-iov のいずれかのインターフェイスが有効になっている場合は、のミニポートドライバーによって、 **Enabledfiltertypes**メンバーの\_受信\_フィルター\_VMQ\_フィルター\_enabled フラグが設定されている必要があります。 ただし、SR-IOV インターフェイスが有効になっている場合は、ミニポートドライバーで**Numqueues**メンバーを0に設定する必要があります。 VMQ インターフェイスが有効になっている場合は、0以外の値を設定する必要があります。

    -   ミニポートドライバーは、 **Currentreceivefiltercapabilities**メンバーを[**NDIS\_receive\_FILTER\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)のアドレスに設定します。これには、の現在の受信フィルター機能が含まれています。現在有効なインターフェイス。

4.  VMQ、SR-IOV、または NDIS パケット合体がネットワークアダプターで現在有効になっている場合、ミニポートドライバーは、 **HardwareReceiveFilterCapabilities**メンバーを、[**受信\_フィルターを受け取る NDIS\_のアドレスに設定し\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造。 この構造体は、ネットワークアダプターの現在有効な受信フィルター処理機能を使用して以前に初期化されています。

5.  ドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出し、 *miniportattributes*パラメーターを[**NDIS\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)へのポインターに設定します。\_ハードウェア\_\_属性の構造をサポートします。

アダプター初期化プロセスの詳細については、「[ミニポートアダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

## <a name="querying-receive-filtering-capabilities-by-overlying-drivers"></a>別のドライバーによる受信フィルター処理機能のクエリ


NDIS は、ネットワークアダプターの現在有効な受信フィルター処理機能を、次の方法でネットワークアダプターにバインドするドライバーに渡します。

-   NDIS が後続のフィルタードライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出すと、Ndis は*attachparameters*パラメーターを使用してネットワークアダプターの NIC スイッチ機能を渡します。 このパラメーターには、\_PARAMETERS 構造体を[**アタッチ\_ための NDIS\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)へのポインターが含まれています。 この構造体の**Receivefiltercapabilities**メンバーには、 [**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体へのポインターが含まれています。

-   NDIS がプロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すと、Ndis は*bindparameters*パラメーターを使用してネットワークアダプターの NIC スイッチ機能を渡します。 このパラメーターには、\_PARAMETERS 構造体を[**アタッチ\_ための NDIS\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)へのポインターが含まれています。 この構造体の**Receivefiltercapabilities**メンバーには、 [**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体へのポインターが含まれています。

また、NDIS は、[現在の\_の機能\_フィルター\_フィルター処理する\_oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)のオブジェクト識別子 (oid) クエリ要求を処理するときに、 [**ndis\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を返します。OID\_、プロトコルまたはフィルタードライバーによって発行された[ハードウェア\_機能\_を受信\_フィルター処理](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)します。

 

 





