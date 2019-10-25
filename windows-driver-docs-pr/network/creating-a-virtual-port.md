---
title: 仮想ポートの作成
description: 仮想ポートの作成
ms.assetid: 6102576D-3236-4FDD-8963-83A9E90FF7F0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e1ff8fedc40772c12b391c94137644874c7131b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838163"
---
# <a name="creating-a-virtual-port"></a>仮想ポートの作成


仮想ポート (VPort) は、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターの NIC スイッチの内部ポートを表すデータオブジェクトです。 各 NIC スイッチには、ネットワーク接続用に次のポートがあります。

-   外部物理ネットワークに接続するための1つの外部物理ポート。

-   PCI Express (PCIe) 物理機能 (PF) または仮想関数 (VFs) に接続されている1つ以上の内部 VPorts。

    PF は、Hyper-v の親パーティションにアタッチされ、そのパーティションで実行されている管理オペレーティングシステムの仮想ネットワークアダプターとして公開されます。

    VF は、Hyper-v 子パーティションにアタッチされ、そのパーティションで実行されるゲストオペレーティングシステムの仮想ネットワークアダプターとして公開されます。

VPorts には、次の2種類があります。

<a href="" id="default-vport"></a>既定の VPort  
既定の VPort は、管理オペレーティングシステムで実行されるネットワークコンポーネントへのネットワーク接続を提供します。 既定の VPort には、NDIS\_既定\_VPORT\_ID の識別子が設定されています。

PF ミニポートドライバーが既定の NIC スイッチを作成して構成すると、ドライバーは既定の VPort を暗黙的に作成し、それを PF に接続します。 既定の VPort を VF に接続することはできません。

既定の VPort は常にアクティブ化された状態であり、明示的に削除することはできません。 PF ミニポートドライバーは、既定の NIC スイッチを削除するときにのみ、既定の VPort を暗黙的に削除します。

スイッチに NIC スイッチおよび既定の VPort を作成する方法の詳細については、「 [Nic スイッチの作成](creating-a-nic-switch.md)」を参照してください。

<a href="" id="nondefault-vport"></a>既定以外の VPort  
既定以外の VPorts は、NIC スイッチの作成時には暗黙的に作成されません。 仮想化スタックなどの前のドライバーは、Oid\_NIC\_スイッチの OID メソッド要求を発行することによって、これらのポートを明示的に作成[\_VPORT\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。 既定以外の VPorts は、PF または VF に接続することができ、NIC スイッチが作成された後でのみ作成できます。

VF に接続されている既定以外の VPort は、ゲストオペレーティングシステムで実行されるネットワークコンポーネントへのネットワーク接続を提供します。 作成され、VF にアタッチされると、既定以外の VPort はアクティブ化された状態になります。

PF に接続されている既定以外の VPort を使用すると、管理オペレーティングシステムで実行されるネットワークコンポーネントにネットワークオフロード機能を追加できます。 たとえば、PF の既定以外の VPorts を使用して、バーチャルマシンキュー (VMQ) インターフェイスと同様のオフロード機能を提供できます。

**メモ** 既定以外の VPorts は、NIC スイッチが作成された後でのみ作成できます。



その後のドライバーは、Oid\_\_のオブジェクト識別子 (OID) メソッド要求を発行します。 [\_VPORT を作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)し、指定した nic スイッチに既定以外の vport を作成\_ます。 この OID 要求では、作成された VPort がネットワークアダプターの PF または以前に割り当てられた VF にもアタッチされます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、[**ndis\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)へのポインターが含まれています。 vport\_PARAMETERS 構造体\_ます。 [OID\_\_nic](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)から正常に返された後\_vport 要求を作成\_、 **NDIS\_nic\_スイッチ**の**VPortId**メンバーは、vport\_パラメーター構造にNIC スイッチの Vport で一意な VPort 識別子。\_

このドライバーは、 [**NDIS\_NIC\_スイッチ\_vport\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体を初期化して、作成する既定以外の vport に関する構成情報を指定します。 構成情報には、既定以外の VPort が接続されている PCIe 関数と、既定以外の VPort のキューペアの数が含まれます。

[**NDIS\_NIC\_スイッチ\_VPORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体を初期化すると、それ以降のドライバーは次の操作を行う必要があります。

-   **Switchid**メンバーは、以前にネットワークアダプターで作成された nic スイッチの識別子に設定する必要があります。これには、OID [\_nic\_スイッチ\_作成\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)の oid メソッド要求を使用します。

    **メモ** Windows Server 2012 以降では、SR-IOV インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは、既定の*NIC スイッチ*と呼ばれます。 既定以外の VPort を作成する場合は、前のドライバーで**Switchid**メンバーを NDIS\_の既定の\_スイッチ\_id 識別子に設定する必要があります。



-   **VPortId**メンバーを NDIS\_既定\_vport\_ID に設定する必要があります。

-   **AttachedFunctionId**メンバーは、既定以外の vport が接続される VF または PF の識別子に設定されている必要があります。

    NDIS\_PF\_関数\_ID の値によって、PF が指定されます。 それ以外の場合は、値を設定する必要があります VF の識別子にリソースが以前に割り当てられている、Oid\_の oid の\_スイッチによって[\_vf\_割り当て](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)ます。

    **メモ** 既定以外の vport から VF または PF への接続は、既定以外の VPort が作成された後には変更できません。



また、このドライバーは、VPort に割り当てられたキューペアの数も指定できます。 キューペアは、VPort に割り当てられているネットワークアダプターの送信キューと受信キューです。 ネットワークアダプターが既定以外の VPorts に対して非対称キューペアをサポートしている場合、そのドライバーは、ドライバーが作成する各 Vports に対して異なる数のキューペアを指定することがあります。 詳細については、「[キューペアの対称および非対称割り当て](symmetric-and-asymmetric-assignment-of-queue-pairs.md)」を参照してください。

この後のドライバーは、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出して、基になる PF ミニポートドライバーに[\_VPORT 要求を作成\_ために、OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)を発行します。 NDIS が OID メソッド要求をミニポートドライバーに転送する前に、次のことを行います。

1.  NDIS は、 [**ndis\_NIC\_スイッチ\_VPORT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体内のパラメーターを検証します。 パラメーターがエラーの場合、NDIS は OID メソッド要求を失敗とし、PF ミニポートドライバーに要求を渡しません。

2.  NDIS は、1から (**numvports**– 1) までの既定以外の vport の識別子を割り当てます。ここで、 **numvports**は、ミニポートドライバーがネットワークアダプター上で構成した vport の数です。 この番号は、 [**NDIS\_NIC\_スイッチ\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)構造体の**numvports**メンバーに指定されています。 このドライバーは、oid [\_NIC\_スイッチ\_列挙型\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)の oid クエリ要求によって、この構造体を返します。

    **メモ** NDIS\_既定の VPort 識別子\_VPORT\_ID は、既定の NIC スイッチの PF に接続されている既定の VPort 用に予約されています。




割り当てられた VPort 識別子は、ネットワークアダプターの NIC スイッチの既定以外の VPort を一意に識別します。


3.  NDIS は、割り当てられた VPort 識別子を使用して、NDIS\_NIC\_スイッチ\_VPORT\_PARAMETERS 構造体の**VPortId**メンバーを設定します。

PF ミニポートドライバーが OID 要求を発行すると、ドライバーは、指定された既定以外の VPort に関連付けられているハードウェアとソフトウェアのリソースを割り当てます。 すべてのリソースが正常に割り当てられると、PF ミニポートドライバーは、 [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)から NDIS\_STATUS\_SUCCESS を返すことによって OID を正常に完了します。

[OID\_NIC\_スイッチ\_作成\_vport](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)要求が正常に完了した場合、PF ミニポートドライバーとそれ以降のドライバーは、後続の操作のために既定以外の Vport の**VPortId**値を保持する必要があります。 **VPortId**の値は、次の操作中に使用されます。

-   NDIS およびそれ以降のドライバーでは、 **VPortId**値を使用して、この vport に関連する oid 要求 ( [oid\_nic\_スイッチ\_VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)および[oid\_NIC など) で、既定以外の vport を識別します。\_スイッチ\_\_VPORT を削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)します。

-   送信操作中、NDIS は、パケットの送信元の VPort を識別する**VPortId**値を指定します。 この値は、帯域外 (OOB) [**NDIS\_net\_buffer\_\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)に指定されており、 [net\_buffer\_list](net-buffer-list-structure.md)構造体の\_情報データをフィルター処理しています。

-   受信操作中、PF ミニポートドライバーは、パケットを転送する**VPortId**値を指定します。 この値は、OOB [**NDIS\_net\_buffer\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)でも指定されており、 [net\_buffer\_list](net-buffer-list-structure.md)構造体の\_情報データをフィルター処理\_ます。

既定以外の VPorts の作成には、次の点が適用されます。

-   メディアアクセス制御 (MAC) 識別子および仮想 LAN (VLAN) id の受信フィルターは、作成後に VPort で構成されます。 このようなドライバーは、Oid の OID メソッド要求を発行することによって、これらの受信フィルターを動的に設定[\_フィルター\_設定された\_フィルターを\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)します。 また、受信フィルターは、oid の OID セット要求を使用して、1つの VPort から別の VPort に移動することもできます。この場合、フィルター [\_フィルター\_移動する\_フィルターを\_受信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)します

-   VF に接続されている既定以外の VPort は、作成時にアクティブ化された状態になります。 VPort が VF にアタッチされている場合、この VPort を非アクティブ化することはできません。

    PF に接続されている既定以外の VPort は、作成時に非アクティブ状態になります。 Hyper-v 拡張可能スイッチモジュールなどの前のドライバーは、VPort が正常に作成された後に、PF に接続されている既定以外の VPort を明示的にアクティブ化します。 これを行うには、oid\_NIC の OID メソッド要求を発行して、 [VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)を PF ミニポートドライバーに\_\_します。

    この OID 要求が発行されると、そのドライバーは、 **Vportstate**メンバーを**NdisNicSwitchVPortStateActivated**に設定して、 [**NDIS\_NIC\_スイッチ\_vport\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造に渡します。

    既定以外の VPort がアクティブ化された状態になると、PF ミニポートドライバーは[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)を呼び出すことによって、vport の共有メモリを割り当てることができます。 ドライバーは、 [**NDIS\_SHARED\_MEMORY\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)構造体の**VPortId**メンバーを、vport の識別子の値に設定する必要があります。

**メモ** 既定以外の VPort がアクティブ化された状態になっている場合、oid [\_NIC\_\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)によって削除されると、非アクティブ状態に設定されます。











