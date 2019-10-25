---
title: 仮想ポート (VPort)
description: 仮想ポート (VPort)
ms.assetid: FCE0B5F5-5E2E-493A-BE25-57FB2C8B0389
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18a6422f02ff8b8a78b33de69cb03cdf3b90b2e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842950"
---
# <a name="virtual-ports-vports"></a>仮想ポート (VPort)


仮想ポート (VPort) は、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターの NIC スイッチの内部ポートを表すデータオブジェクトです。 各 NIC スイッチには、ネットワーク接続用に次のポートがあります。

-   外部物理ネットワークに接続するための1つの外部物理ポート。

-   PCI Express 物理機能 (PF) または仮想関数 (VFs) に接続されている1つ以上の内部 VPorts。

    PF は、Hyper-v の親パーティションにアタッチされ、そのパーティションで実行されている管理オペレーティングシステムの仮想ネットワークアダプターとして公開されます。

    VF は、Hyper-v 子パーティションにアタッチされ、そのパーティションで実行されるゲストオペレーティングシステムの仮想ネットワークアダプターとして公開されます。

NIC スイッチは、物理ポートから1つまたは複数の VPorts にネットワークトラフィックをブリッジします。 これにより、基になる物理ネットワークインターフェイスへの仮想アクセスが提供されます。

各 VPort には、ネットワークアダプターの NIC スイッチに固有の一意の識別子 (*VPortId*) があります。 既定の VPort は常に既定の NIC スイッチに存在するため、削除することはできません。 既定の VPort には、NDIS\_既定\_VPORT\_ID の VPortId があります。

PF ミニポートドライバーが Oid\_\_のオブジェクト識別子 (OID) メソッドの要求を処理するときに[\_スイッチ\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)、スイッチの nic スイッチと既定の vport が作成されます。 既定の VPort は常に PF にアタッチされ、常に動作状態になります。

既定以外の VPorts は oid\_NIC\_スイッチの OID メソッド要求を使用して作成され、 [\_vports\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)ます。 VF にアタッチできる既定以外の VPort は1つだけです。 アタッチされると、既定値は動作状態になります。 1つまたは複数の既定以外の VPorts を作成し、PF に接続することもできます。 これらの VPorts は作成時に nonoperational され、 [oid\_NIC\_スイッチ\_vports\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)を使用して操作できるようになります。

**メモ** VPort が操作可能になると、oid [\_\_\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)の oid 要求によって削除された場合にのみ、nonoperational になります。



各 VPort には、パケットの受信と送信のために1つ以上のハードウェアキューペアが関連付けられています。 ネットワークアダプターの既定のキューペアは、既定の VPort で使用するために予約されています。 [OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)を使用して vports が作成されたときに、既定以外の vports のキューペアが割り当てられて割り当てられ、\_vports 要求を作成\_ます。

既定以外の VPorts は oid\_NIC\_スイッチの OID メソッド要求を使用して作成および構成され[\_vports\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。 既定の VPort と既定以外の Vport は、oid [\_NIC\_スイッチ\_vport\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)を使用して再構成されます。 各 OID 要求には、次の構成パラメーターを指定する[**NDIS\_NIC\_スイッチ\_VPORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造が含まれています。

-   VPort がアタッチされている PCIe 関数。

    各 VPort は、任意の時点で PF に接続するか、または VF に接続することができます。 VPort が作成され、PCIe 関数にアタッチされた後、添付ファイルを別の PCIe 関数に動的に変更することはできません。

    **メモ** 既定の VPort は、ネットワークアダプター上の PF に常に接続されています。




Windows Server 2012 の NDIS 6.30 以降では、VF にアタッチできる既定以外の VPort は1つだけです。 ただし、既定の Vports と共に複数の既定以外の VPorts を PF に接続することができます。


-   VPort に割り当てられているハードウェアキューペアの数。

    各 VPort には、使用可能なハードウェアキューペアのセットがあります。 各キューペアは、ネットワークアダプター上の個別の送信キューと受信キューで構成されます。

    キューペアは、ネットワークアダプター上のリソースに制限があります。 既定値および既定以外の VPorts で使用するために予約されているキューペアの合計数は、NIC スイッチを作成するときに指定します。 これにより、既定の VPort に割り当てられているキューペアの数を既定以外の Vport と異なるものにすることができます。

    既定以外の各 VPort は、異なる数のキューペアを持つように構成できます。 これは、キューペアの*非対称割り当て*と呼ばれます。 NIC でこのような非対称割り当てが許可されていない場合、各既定以外の VPort は、同じ数のキューペアを持つように構成されます。 これは、キューペアの*対称割り当て*と呼ばれます。 詳細については、「[キューペアの対称および非対称割り当て](symmetric-and-asymmetric-assignment-of-queue-pairs.md)」を参照してください。

    **メモ** PF ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)中にキューペアの非対称割り当てをサポートするかどうかを報告します。 詳細については、「 [PF ミニポートドライバーの初期化](initializing-a-pf-miniport-driver.md)」を参照してください。




各 VPort に割り当てられたキューペアの数は動的に変更されません。 Vport が作成された後に、VPort に割り当てられたキューペアの数を変更することはできません。

**メモ** 既定以外の VPorts に割り当てられた1つ以上のキューペアは、ゲストオペレーティングシステムで実行されている VF ミニポートドライバーによる receive side scaling (RSS) に使用できます。




-   VPort の割り込みモデレーションパラメーター。

    異なる VPorts に対して異なる割り込みモデレーションの種類を指定できます。 これにより、仮想化スタックは、特定の VPort によって生成される割り込みの数を制御できます。

構成パラメーターに加えて、追加のドライバーでは、\_Oid の OID メソッド要求を発行することによって、各 VPort の受信フィルターを構成できます。 [\_フィルター\_設定\_フィルターを設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)します。 NIC スイッチは、VPort に対して指定された受信フィルター処理を実行します。

VPorts の受信フィルターパラメーターには、メディアアクセス制御 (MAC) アドレスの一覧や、仮想 LAN (VLAN) 識別子などのパケットフィルター条件が含まれます。 MAC アドレスと VLAN 識別子用のフィルターは、常に[**NDIS\_受信\_フィルター\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 、\_OID に関連付けられているパラメーターを受信[\_フィルター\_設定\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)フィルター申請. NIC スイッチでは、宛先 MAC アドレスと VLAN 識別子が VPort で設定された受信フィルター条件と一致するスイッチに、着信パケットをフィルター処理する必要があります。 NIC スイッチは、別の VPort または外部の物理ポートから受信したパケットをフィルター処理します。 パケットがフィルターに一致する場合、NIC スイッチはそれを VPort に転送する必要があります。

VPort では、複数の MAC アドレスと VLAN 識別子のペアを設定できます。 MAC アドレスのみが設定されている場合、受信フィルターは、VPort が次の条件に一致するパケットを受信するように指定します。

-   パケットの宛先 MAC アドレスは、フィルターの MAC アドレスと一致します。

-   パケットに vlan タグがあるか (VLAN タグが存在する場合)、VLAN 識別子が0になっています。

Oid\_NIC\_スイッチの OID セット要求を使用して、既定以外の VPorts が削除され[\_vports\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)されます。 既定の VPort が削除されるのは、oid セットの oid 設定要求を使用して NIC スイッチが削除された場合のみです[\_nic\_スイッチ\_削除\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)です。









