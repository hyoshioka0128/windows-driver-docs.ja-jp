---
title: OID_NIC_SWITCH_CREATE_SWITCH 要求の処理
description: OID_NIC_SWITCH_CREATE_SWITCH 要求の処理
ms.assetid: 5C0BC300-8904-483A-A66B-8F5CFE0829B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cfb723ba54a3fe109b1a2c45ab4c0072834f8ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842554"
---
# <a name="handling-the-oid_nic_switch_create_switch-request"></a>OID\_NIC の処理\_スイッチ\_\_スイッチ要求の作成


NDIS は、Oid\_\_のオブジェクト識別子 (OID) メソッドの要求を発行します。 [\_スイッチ\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)して、次の操作を行います。

-   PCI Express (PCIe) 物理機能 (PF) 用のミニポートドライバーによって静的に作成されたネットワークアダプターで、NIC スイッチを有効にします。 PF は、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターのハードウェアコンポーネントです。

    NIC スイッチは、コンテキスト内から[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)の呼び出しまで、PF ミニポートドライバーによって静的に作成されます。 ドライバーは、レジストリ設定から読み取られたパラメーターに基づいて、リソースを割り当て、スイッチを作成します。

-   ネットワークアダプターに NIC スイッチを動的に作成します。

    PF ミニポートドライバーが静的 NIC スイッチの作成をサポートしていない場合、ミニポートドライバーはリソースを割り当て、OID 要求で指定されたパラメーターに基づいてスイッチを作成します。

PF ミニポートドライバーは、NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すときに、sr-iov インターフェイスのサポートをアドバタイズします。 PF ミニポートドライバーが sr-iov をサポートしている場合、NDIS はレジストリから NIC スイッチの構成を読み取ります。 NDIS が oid を発行する前に、oid の OID メソッド要求[\_NIC\_スイッチ\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)して、PF ミニポートドライバーへのスイッチを\_作成します。次のように、ndis は、 [**ndis\_NIC\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)\_のパラメーター構造をレジストリ情報に設定します。

-   NDIS は、 **switchtype**メンバーを NIC スイッチの種類に設定します。

    Windows Server 2012 以降では、 **NdisNicSwitchTypeExternal**のスイッチの種類のみがサポートされています。 外部スイッチは、この種類のスイッチに接続されている仮想ポート (VPorts) が、ネットワークアダプターの物理ポートを介して外部ネットワークにアクセスできることを指定します。

    NIC スイッチの詳細については、「 [Sr-iov アーキテクチャ](sr-iov-architecture.md)」を参照してください。

-   NDIS では、 **Switchid**メンバーが NIC スイッチの識別子の値に設定されます。 スイッチ識別子は、0から、ネットワークアダプターがサポートするスイッチの数までの整数です。 NDIS\_DEFAULT\_スイッチ\_ID 値は、既定の NIC スイッチを示します。

    **注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプターの既定の NIC スイッチのみをサポートしています。

     

-   NDIS は、NIC スイッチで割り当てることができる PCIe 仮想関数 (VFs) の数を指定する**Numvfs**メンバーを設定します。

Oid\_\_スイッチの oid メソッド要求を受信すると[\_スイッチ\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)されますが、PF ミニポートドライバーは次の操作を行う必要があります。

1.  PF ミニポートドライバーが静的スイッチの作成と構成をサポートしている場合は、NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)を呼び出したときに NIC スイッチが作成されます。 ドライバーは、この OID 要求を処理するときに、 [**NDIS\_NIC\_スイッチ\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体の構成パラメーターを確認する必要があります。 パラメーターは、 *MiniportInitializeEx*の呼び出し中にスイッチを作成するためにドライバーによって使用されるものと同じである必要があります。 これが true でない場合、ドライバーは OID 要求を失敗させる必要があります。

    詳細については、「 [NIC スイッチの静的作成](static-creation-of-a-nic-switch.md)」を参照してください。

2.  PF ミニポートドライバーで動的スイッチの作成と構成がサポートされている場合、ドライバーは、NDIS\_NIC の構成値を検証し、 [ **\_PARAMETERS 構造\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)を設定して、これらの値に基づいて nic スイッチを作成する必要があります。

    詳細については、「 [NIC スイッチの動的作成](dynamic-creation-of-a-nic-switch.md)」を参照してください。

3.  PF ミニポートドライバーは、NIC スイッチの既定の VPort に必要なハードウェアおよびソフトウェアリソースを割り当てる必要があります。

    既定の VPort は常に oid 要求 oid\_NIC の要求を使用して作成され**ます  ** [\_スイッチ\_作成\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch) 、oid\_の oid 要求を使用して\_スイッチ\_削除\_スイッチ[削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)します。 Oid\_の OID 要求、 [nic\_スイッチ\_\_vport](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)と[oid\_nic\_\_の削除\_vport](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)を使用して、nic スイッチで既定以外の vport を作成および削除します。

     

4.  ダイナミックスイッチの作成と構成をサポートする PF ミニポートドライバーでは、 [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出すことによって、スイッチで sr-iov の仮想化を有効にする必要があります。 この呼び出しにより、アダプターの PCI Express (PCIe) 構成領域の SR-IOV 拡張機能構造で**Numvfs**メンバーと**VF Enable** bit が構成されます。

    SR-IOV 構成領域の詳細については、「PCI SIG の[シングルルート I/o 仮想化と共有 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)の仕様」を参照してください。

    **注**  PF ミニポートドライバーが静的スイッチの作成をサポートしている場合は、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)が呼び出されたときにスイッチを作成した後に sr-iov の仮想化が有効になります。

     

PF ミニポートドライバーが oid\_\_NIC の oid メソッド要求を正常に終了した場合、\_スイッチ\_作成、次のことが可能になります。

-   Oid の OID メソッド要求を使用して、VFs を NIC スイッチに割り当てることができます。 [\_nic\_スイッチ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)によって\_VF が割り当てられます。

-   Oid\_\_NIC の oid メソッド要求を使用して NIC スイッチに既定以外の VPorts を作成することができます。これには、 [\_vports\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)ます。

    ミニポートドライバーは、既定以外の VPorts のプールを管理します。 ドライバーは、 [**NDIS\_NIC\_スイッチ\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)構造体の**numvports**メンバーを介して、プール内の既定以外の vports の数を指定します。 このドライバーは、oid [\_NIC\_スイッチ\_列挙型\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)の oid クエリ要求によって、この構造体を返します。

    ネットワークアダプターは、常に、PF のプールから既定の VPort を作成する必要がある  に**注意**してください。

     

 

 





