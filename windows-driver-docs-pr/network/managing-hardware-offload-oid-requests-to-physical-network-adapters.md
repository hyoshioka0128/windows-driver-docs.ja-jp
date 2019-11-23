---
title: 物理ネットワーク アダプターへのハードウェア オフロード OID 要求の管理
description: 物理ネットワーク アダプターへのハードウェア オフロード OID 要求の管理
ms.assetid: A646CBB8-89AD-4C08-BECB-1E54E4D74311
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b8d29d3593ad82218b2e98195dfe26c3b403f0d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844124"
---
# <a name="managing-hardware-offload-oid-requests-to-physical-network-adapters"></a>物理ネットワーク アダプターへのハードウェア オフロード OID 要求の管理


このトピックでは、Hyper-v 拡張可能スイッチ転送拡張機能が、基盤となる物理アダプター上のハードウェアオフロードテクノロジに対するオブジェクト識別子 (OID) 要求を、拡張可能なスイッチ制御パスを介して管理する方法について説明します。

たとえば、外部ネットワークアダプターは、NDIS マルチプレクサー (MUX) 中間ドライバーの仮想ミニポートエッジにバインドできます。 MUX ドライバーは、ホスト上の1つまたは複数の物理ネットワークのチームにバインドされています。 この構成は、*拡張可能なスイッチチーム*と呼ばれています。

この構成では、拡張可能なスイッチ拡張機能がチーム内のすべてのネットワークアダプターに公開されます。 これにより、拡張機能がチーム内の個々のネットワークアダプターの構成と使用を管理できるようになります。 たとえば、転送拡張機能は、送信パケットを個々のアダプターに転送することによって、チームで負荷分散フェールオーバー (LBFO) ソリューションのサポートを提供できます。 拡張可能なスイッチチームを管理する転送拡張機能は、*チーミングプロバイダー*と呼ばれます。 チーミングプロバイダーの詳細については、「[チーミングプロバイダーの拡張機能](teaming-provider-extensions.md)」を参照してください。

次の図は、NDIS 6.40 (Windows Server 2012 R2) 以降の拡張可能なスイッチチームの例を示しています。

![ndis 6.40 の拡張可能なスイッチチームの図](images/vswitch-oid-controlpath2-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の拡張可能なスイッチチームの例を示しています。

![ndis 6.30 の拡張可能なスイッチチームの図](images/vswitch-oid-controlpath2.png)

**注**  拡張可能なスイッチインターフェイスでは、NDIS フィルタードライバーは拡張*可能なスイッチ拡張機能*と呼ばれ、ドライバースタックは*拡張可能なスイッチドライバースタック*と呼ばれます。

 

Oid [\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)の oid 要求を処理することにより、転送拡張機能は、ハードウェアオフロードのために拡張可能なスイッチチームの構成に参加することができ\_ます。 たとえば、拡張可能なスイッチチームの物理ネットワークアダプターを拡張機能が管理している場合、OID\_スイッチ\_NIC\_要求要求を、ハードウェアオフロードをサポートする物理アダプターに転送できます。

NDIS プロトコルとフィルタードライバーは、ハードウェアオフロードテクノロジに対する OID 要求を基になる物理ネットワークアダプターに発行できます。 これらの OID 要求が拡張可能スイッチインターフェイスに到着すると、 [**NDIS\_スイッチ\_NIC\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)の内部で oid 要求がカプセル化されます。 次に、拡張可能スイッチのプロトコルエッジが、この構造体を含む[NIC\_要求\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)の oid 要求を発行します。

拡張可能なスイッチインターフェイスは、次のハードウェアオフロードテクノロジの Oid をカプセル化します。

<a href="" id="internet-protocol-security--ipsec--offload--version-2-"></a>インターネットプロトコルセキュリティ (IPsec) オフロード (バージョン 2)  
次の IPsec OID 要求がカプセル化されます。

-   [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_SA を追加\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa-ex)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_DELETE\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)

-   [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_更新\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa)

転送拡張機能は、これらの OID 要求を失敗または*拒否*することはできません。

IPsec ハードウェアオフロードテクノロジのバージョン2の詳細については、「 [Ipsec オフロードバージョン 2](ipsec-offload-version-2.md)」を参照してください。

<a href="" id="single-root-i-o-virtualization--sr-iov-"></a>シングルルート i/o 仮想化 (SR-IOV)  
次の sr-iov OID 要求がカプセル化されています。

-   [OID\_NIC\_スイッチ\_割り当て\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)

-   [OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)

-   [OID\_NIC\_スイッチ\_削除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)

-   [OID\_NIC\_スイッチ\_空き\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)

-   [OID\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)

-   [OID\_受信\_フィルター\_移動\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)

転送拡張機能は、 [oid\_nic\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)の oid 要求を拒否し、\_VF と[oid\_nic\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)に割り当て\_、NDIS\_status\_SUCCESS 以外のステータスコードで要求を完了することによって\_vport を作成\_ます。 ただし、拡張機能は他の SR-IOV OID 要求を拒否することはできません。

SR-IOV ハードウェアオフロードテクノロジの詳細については、「[シングルルート I/o 仮想化 (sr-iov)](single-root-i-o-virtualization--sr-iov-.md)」を参照してください。

<a href="" id="virtualized-machine-queue--vmq-"></a>仮想マシンキュー (VMQ)  
次の VMQ OID 要求がカプセル化されています。

-   [OID\_受信\_フィルター\_割り当て\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)

-   [OID\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)

-   [OID\_受信\_フィルター\_空き\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)

-   [OID\_受信\_フィルター\_キュー\_割り当て\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)

-   [OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)

転送拡張機能は、Oid の OID 要求を拒否することができます[\_\_フィルターを受信し\_\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)および OID を割り当てることができます\_フィルター\_[設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)\_、NDIS\_status\_SUCCESS 以外のステータスコードで要求を完了します。\_ ただし、拡張機能は他の VMQ OID 要求を拒否することはできません。

VMQ ハードウェアオフロードテクノロジの詳細については、「[仮想マシンキュー (vmq)](virtual-machine-queue--vmq-.md)」を参照してください。

転送拡張機能は、次のガイドラインに従ってハードウェアオフロード OID 要求を処理する必要があります。

-   Microsoft IM プラットフォームは、チーム全体に共通のオフロード機能のみをアドバタイズします。 ただし、拡張機能は、チーム内の各アダプターの機能に対してクエリを実行するための OID 要求を生成できます。

    拡張機能によって、チーム内の物理アダプターのハードウェア機能が決定された後、ハードウェアオフロードの OID セット要求をオフロードに最適なアダプターに転送できます。

-   プロトコルまたはフィルタードライバーによって送信されるすべてのハードウェアオフロード OID 要求は、 [**NDIS\_スイッチ\_NIC\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造内にカプセル化されます。 また、転送拡張機能によって送信されるすべてのハードウェアオフロード OID 要求は、 **NIC\_OID\_要求構造\_、NDIS\_スイッチ**にカプセル化する必要があります。

    拡張機能は、カプセル化された OID 要求を、 [oid\_スイッチ\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)を介して、基になる物理ネットワークアダプターに転送します。 この手順の詳細については、「[物理ネットワークアダプターへの OID 要求の転送](forwarding-oid-requests-to-physical-network-adapters.md)」を参照してください。

-   拡張機能は、オフロードリソースの割り当てをクリア、解放、または完了するために、ハードウェアオフロード OID 要求を変更または失敗させないようにする必要があります。 たとえば、拡張機能は oid 要求の OID 要求に失敗しないようにする必要があります。 [\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)または[oid\_NIC\_スイッチ\_\_VPORT を削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)します。 拡張可能なスイッチインターフェイスは、これらのリソースの状態情報をクリーンアップするために、これらの OID 要求を処理する必要があります。

    拡張機能は、ハードウェアオフロードの OID 要求を変更または失敗させて、オフロードリソースの割り当て、移動、または設定を行うことができます。 たとえば、拡張機能は[oid\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)の oid 要求を失敗または変更することができます。\_\_VF または[oid\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA を追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)します。

-   拡張機能は、ハードウェアオフロード Oid を基になる物理ネットワークアダプターに送信できます。 ただし、拡張機能が割り当てられなかったオフロードリソースをクリアまたは解放するハードウェアオフロード OID を生成することはできません。

    たとえば、拡張機能は、ハードウェアオフロード OID 要求の\_Oid を生成しないようにする必要があります。この場合、 [\_キュー\_\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)を受け取ると、同じキューの[\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)要求\_割り当て\_ます。\_

    拡張機能は、それまでのドライバーによって発行されたものと同じ OID 要求をフィルター処理している場合にのみ、独自のカプセル化されたハードウェアオフロード OID 要求を生成**する  ます**。 この場合、拡張機能は元の OID 要求を転送することはできません。 代わりに、この要求を完了するために、この拡張機能は[**NdisFOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete)を呼び出す必要があります。 NDIS が[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)を呼び出して、生成された OID 要求を完了します。

     

-   拡張機能がハードウェアオフロード OID 要求を基になる物理ネットワークアダプターに転送している場合は、 [**NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造体の**DestinationNicIndex**メンバーが、アダプターの0以外のインデックス値に設定されている必要があります。 これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](network-adapter-index-values.md)」を参照してください。

    また、 **DestinationPortId**メンバーは、外部ネットワークアダプターが接続される拡張可能なスイッチポートの識別子に設定されている必要があります。

-   拡張機能が、Hyper-v 子パーティションのリソースを割り当てるハードウェアオフロード OID 要求の発行元である場合、 [**NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造の**SourcePortId**メンバーは、パーティションが接続される拡張可能なスイッチポートの識別子に設定する必要があります。

    **Sourcenicindex**メンバーは、**既定\_\_NIC\_インデックス**に設定する必要があります\_に設定する必要があります。

-   拡張機能が OID 要求を転送するために[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出す場合は、 *OidRequest*パラメーターを、 [oid\_SWITCH\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)oid 要求の[ **\_要求構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)へのポインターに設定する必要があります。

拡張機能が OID 要求をフィルター処理する方法の詳細については、「 [NDIS フィルタードライバーでの Oid 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)」を参照してください。

MUX ドライバーの詳細については、「 [NDIS MUX 中間ドライバー](ndis-mux-intermediate-drivers.md)」を参照してください。

 

 





