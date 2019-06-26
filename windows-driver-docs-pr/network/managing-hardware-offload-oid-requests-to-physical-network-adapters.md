---
title: 物理ネットワーク アダプターへのハードウェア オフロード OID 要求の管理
description: 物理ネットワーク アダプターへのハードウェア オフロード OID 要求の管理
ms.assetid: A646CBB8-89AD-4C08-BECB-1E54E4D74311
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68ea7bd874fc506ff77d57a6d82aef7480ea1727
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356182"
---
# <a name="managing-hardware-offload-oid-requests-to-physical-network-adapters"></a>物理ネットワーク アダプターへのハードウェア オフロード OID 要求の管理


このトピックでは、転送拡張機能、HYPER-V 拡張可能スイッチのオブジェクト識別子 (OID) を管理する方法について説明しますハードウェアの要求は、拡張可能スイッチ コントロール パス経由で基になる物理アダプターでのテクノロジをオフロードします。

たとえば、外部ネットワーク アダプターは、NDIS マルチプレクサー (マルチプレクサー) の中間ドライバーの仮想ミニポート端にバインドできます。 MUX driver は、ホスト上の 1 つまたは複数の物理ネットワーク チームにバインドされます。 この構成と呼ばれる、*拡張可能スイッチ チーム*します。

この構成で拡張可能スイッチの拡張機能は、チーム内のすべてのネットワーク アダプターに公開されます。 これにより、拡張機能の構成と、チーム内の個々 のネットワーク アダプターの使用を管理できます。 たとえば、転送拡張機能では、個々 のアダプターに送信されるパケットを転送することによって、over、チーム分散フェールオーバー (LBFO) のソリューション ロードのサポートを提供できます。 拡張可能スイッチ チームを管理する転送拡張機能が呼ばれる、*チーミング プロバイダー*します。 プロバイダーのチーミングの詳細については、次を参照してください。[プロバイダーの拡張機能のチーミング](teaming-provider-extensions.md)します。

次の図は、NDIS 6.40 (Windows Server 2012 R2) と後で拡張可能スイッチ チームの例を示します。

![ndis 6.40 の拡張可能スイッチ チームのダイアグラム](images/vswitch-oid-controlpath2-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の拡張可能スイッチ チームの例を示します。

![ndis 6.30 の拡張可能スイッチ チームのダイアグラム](images/vswitch-oid-controlpath2.png)

**注**  、拡張可能スイッチのインターフェイスで NDIS フィルター ドライバーと呼ばれる*拡張可能スイッチの拡張機能*と呼ばれるドライバー スタック、*拡張可能スイッチ ドライバー スタック*.

 

OID を処理することによって要求[OID\_切り替える\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)、転送拡張機能は、ハードウェアのオフロードの拡張可能スイッチ チームの構成に参加できます。 たとえば、拡張機能は、拡張可能スイッチ チームの物理ネットワーク アダプターを管理している場合に転送できます OID\_スイッチ\_NIC\_ハードウェア オフロードをサポートする物理アダプターに要求します。

NDIS と上位のプロトコルとフィルター ドライバーは、基になる物理ネットワーク アダプターに、ハードウェア オフロード テクノロジの OID 要求を発行することができます。 拡張可能スイッチのインターフェイスでこれらの OID 要求が届いたら、OID 要求内でカプセル化、 [ **NDIS\_切り替える\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request). 拡張可能スイッチのプロトコルのエッジがの OID 要求を発行し、 [OID\_切り替える\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)この構造体を格納しています。

拡張可能スイッチのインターフェイスでは、次のハードウェア オフロード テクノロジの Oid をカプセル化します。

<a href="" id="internet-protocol-security--ipsec--offload--version-2-"></a>インターネット プロトコル セキュリティ (IPsec) オフロード (バージョン 2)  
次の IPsec OID 要求がカプセル化します。

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa-ex)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_DELETE\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_UPDATE\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa)

転送拡張機能は失敗する必要がありますまたは*拒否*、これらの OID 要求。

IPsec のハードウェア オフロード テクノロジのバージョン 2 の詳細については、次を参照してください。 [IPsec オフロード バージョン 2](ipsec-offload-version-2.md)します。

<a href="" id="single-root-i-o-virtualization--sr-iov-"></a>シングル ルート I/O 仮想化 (SR-IOV)  
次の SR-IOV OID 要求がカプセル化します。

-   [OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)

-   [OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)

-   [OID\_NIC\_スイッチ\_削除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)

-   [OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)

-   [OID\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)

-   [OID\_受信\_フィルター\_移動\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)

転送拡張機能の OID 要求を拒否できます[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)と[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport) NDIS 以外の状態コードで要求を完了して\_状態\_成功します。 ただし、拡張する必要があります、他の SR-IOV OID 要求を拒否しては。

SR-IOV 対応のハードウェア オフロード テクノロジの詳細については、次を参照してください。 [Single Root I/O Virtualization (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)します。

<a href="" id="virtualized-machine-queue--vmq-"></a>仮想マシン キュー (VMQ)  
次の VMQ OID 要求がカプセル化します。

-   [OID\_受信\_フィルター\_ALLOCATE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)

-   [OID\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)

-   [OID\_受信\_フィルター\_FREE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)

-   [OID\_受信\_フィルター\_キュー\_割り当て\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)

-   [OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)

転送拡張機能の OID 要求を拒否できます[OID\_受信\_フィルター\_ALLOCATE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)と[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter) NDIS 以外の状態コードで要求を完了して\_状態\_成功します。 ただし、拡張する必要があります他 VMQ OID 要求を拒否しては。

VMQ のハードウェア オフロード テクノロジの詳細については、次を参照してください。[仮想マシン キュー (VMQ)](virtual-machine-queue--vmq-.md)します。

転送拡張機能は、ハードウェア オフロード OID 要求を処理するための次のガイドラインに従う必要があります。

-   IM の Microsoft プラットフォームでは、全体的なチームの共通のオフロード機能のみをアドバタイズします。 ただし、拡張機能では、チームの各アダプターの機能を照会する OID 要求を生成できます。

    拡張機能では、チーム内の物理アダプターのハードウェア機能を特定した後、オフロード用に最適であるアダプターをハードウェア オフロードの OID のセット要求を転送できます。

-   プロトコルまたはフィルター ドライバーに関連して発生したすべてのハードウェア オフロード OID 要求が内部にカプセル化、 [ **NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造体。 転送拡張機能によって発信されたすべてのハードウェア オフロード OID 要求する必要がありますにカプセル化することも、 **NDIS\_スイッチ\_NIC\_OID\_要求**構造体。

    拡張機能の OID セットの要求を通じて基になる物理ネットワーク アダプターをカプセル化された OID 要求を転送する[OID\_スイッチ\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)します。 この手順の詳細については、次を参照してください。[物理ネットワーク アダプターへの OID 要求の転送](forwarding-oid-requests-to-physical-network-adapters.md)します。

-   拡張機能またはことはできませんを変更またはを無料でクリアするハードウェア オフロード OID 要求を失敗オフロード リソースの割り当てを完了します。 たとえば、拡張機能にする必要がありますの OID 要求失敗しない[OID\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)または[OID\_NIC\_スイッチ\_削除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)します。 拡張可能スイッチのインターフェイスには、これらのリソースの状態情報をクリーンアップするこれらの OID 要求を処理する必要があります。

    拡張機能が変更または割り当てる、移動、ハードウェアのオフロード OID 要求を失敗またはセットのリソースの負荷を軽減します。 拡張機能が失敗やの OID 要求の変更などの[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)または[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)します。

-   拡張機能は、基になる物理ネットワーク アダプターにハードウェア オフロード Oid を取得できます。 ただし、拡張機能では、OID をクリアまたは解放を割り当てられなかった、拡張機能リソースをオフロードするハードウェア オフロードが取得する必要があります。

    たとえば、拡張機能がのハードウェア オフロード OID 要求を取得する必要があります[OID\_受信\_フィルター\_FREE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)取得されなかった場合、 [OID\_受信\_フィルター\_ALLOCATE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)が同一のキューに要求します。

    **注**  重なってドライバーによって発行された同じ OID 要求のフィルタ リングは、その場合、拡張機能は独自のカプセル化されたハードウェア オフロード OID 要求を発信のみことができます。 ここでは、拡張する必要があります、OID の元の要求を転送しません。 代わりに、拡張機能を呼び出す必要があります[ **NdisFOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequestcomplete) NDIS を呼び出すと、この要求を完了するその[ *FilterOidRequestComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request_complete)から配信された OID 要求を完了します。

     

-   拡張機能が、基になる物理ネットワーク アダプターにハードウェアのオフロード OID 要求を転送する場合、 **DestinationNicIndex**のメンバー、 [ **NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造体は、アダプターのインデックスが 0 以外の値に設定する必要があります。 これらのインデックス値の詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](network-adapter-index-values.md)します。

    また、 **DestinationPortId**メンバーは、外部ネットワーク アダプターが接続されている拡張可能スイッチ ポートの識別子を設定する必要があります。

-   拡張機能が HYPER-V 子パーティションでは、リソースを割り当てるには、ハードウェア オフロード OID 要求を発信する場合、 **SourcePortId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造体は、パーティションが接続されている拡張可能スイッチ ポートの識別子を設定する必要があります。

    **SourceNicIndex**にメンバーを設定する必要があります**NDIS\_スイッチ\_既定\_NIC\_インデックス**します。

-   拡張機能を呼び出すと[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)に OID 要求を転送するように設定する必要があります、 *OidRequest*パラメーターへのポインターを[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)用の構造、 [OID\_スイッチ\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)OID 要求。

拡張機能が OID 要求をフィルター処理する方法の詳細については、次を参照してください。 [NDIS フィルター ドライバーでの OID 要求のフィルタ リング](filtering-oid-requests-in-an-ndis-filter-driver.md)します。

MUX ドライバーの詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](ndis-mux-intermediate-drivers.md)します。

 

 





