---
title: 仮想ポートのパラメーターの設定
description: 仮想ポートのパラメーターの設定
ms.assetid: 92CBE5B2-897D-4B34-9AB9-8207C42A72BF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1caf3b48ace1d3db498f05d20a5a94df397fcc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841928"
---
# <a name="setting-the-parameters-of-a-virtual-port"></a>仮想ポートのパラメーターの設定


1つ上のドライバーでは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターで、NIC スイッチの仮想ポート (VPort) のパラメーターを変更できます。 このドライバーは、オブジェクト識別子 (OID) set 要求の[oid\_NIC\_スイッチ\_VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)を発行して、これらのパラメーターを変更します。

それまでのドライバーは、この OID セット要求を発行する前に、vport\_パラメーター構造\_VPORT で変更されるパラメーターを使用して、 [**NDIS\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)を初期化する必要があります。 次に、このドライバーは、OID 要求の[**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を初期化し、 **Informationbuffer**メンバーを**ndis\_NIC\_スイッチへのポインター (vport\_パラメーター** ) に設定します。データ.

VPort の構成パラメーターの一部だけを変更できます。 前のドライバーでは、 [**NDIS\_NIC\_スイッチ\_VPORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体の次のメンバーを設定することによって、変更するパラメーターを指定します。

-   **Switchid**メンバーは、パラメーターが返される NIC スイッチの識別子に設定されている必要があります。

    **注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは、既定の*NIC スイッチ*と呼ばれます。 **Switchid**メンバーを NDIS\_既定\_スイッチ\_ID に設定する必要があります。

     

-   **VPortId**メンバーは、vport に関連付けられた識別子に設定する必要があります。 このドライバーは、次のいずれかの方法で VPort 識別子を取得します。

    -   Oid\_の以前の OID メソッド要求から、 [\_VPORT を作成\_\_スイッチに切り替え](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)ます。

    -   Oid\_NIC の以前の OID メソッド要求から、[列挙型\_VPORTS\_スイッチ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)ます。

-   適切な NDIS\_NIC\_スイッチ\_VPORT\_PARAMS\_*Xxx*\_変更されたフラグを**フラグ**メンバーで設定する必要があります。 [**Ndis\_nic\_スイッチ\_vport\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体のメンバーは、対応する NDIS\_NIC\_スイッチ\_VPORT\_PARAMS\_*Xxx*の場合にのみ変更でき\_CHANGED フラグは Ntddndis で定義されています。

-   [**Ndis\_nic\_スイッチのメンバーは、vport\_パラメーター構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)ます。これは、NDIS\_NIC\_スイッチ\_VPORT\_PARAMS\_*Xxx*\_変更フラグに対応します。**Flags**メンバーに設定すると、変更する vport 構成パラメーターが設定されます。

Windows Server 2012 以降では、 [**NDIS\_nic\_スイッチ\_vport\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体の次のメンバーのみが、 [oid\_nic\_スイッチ\_vport を使用して変更できます。\_のパラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters):

<a href="" id="portname"></a>**PortName**  
このメンバーには、VPort についてのわかりやすい説明が含まれています。

<a href="" id="interruptmoderation"></a>**InterruptModeration**  
このメンバーは、VPort の割り込みモデレーション設定を指定します。

<a href="" id="processoraffinity"></a>**ProcessorAffinity**  
このメンバーは、この VPort が関連付け可能な Cpu のグループ番号とビットマップを指定します。

次のドライバーは、VPort の**Processoraffinity**メンバーを変更するために、次のガイドラインに従う必要があります。

-   このメンバーは、PF に接続されている VPorts に対してのみ有効です。 このフィールドは、VF に接続されている既定以外の VPorts では無効です。

-   PF に接続されている既定以外の VPorts では、Vports の作成時に少なくとも1つのプロセッサを指定する必要があります。 既定以外の VPort に関連付けられているプロセッサ関係は、VPort の作成後に変更できます。

    **注**  既定以外の vports は OID\_NIC のメソッド要求を使用して作成されます。 [\_スイッチ\_\_vports を作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

     

<a href="" id="vportstate"></a>**VPortState**  
このメンバーは、VPort の現在の状態を指定します。

次のドライバーは、VPort の**Vportstate**メンバーを変更するために、次のガイドラインに従う必要があります。

-   VF に接続されている既定以外の VPort の場合、 **Vportstate**メンバーは常に**NdisNicSwitchVPortStateActivated**に設定する必要があります。

-   PF に接続されている既定以外の VPort の場合、VPort が作成されるときに**Vportstate**メンバーを**NdisNicSwitchVPortStateDeactivated**に設定する必要があります。 PF VPort がアクティブ化されるのは、oid [\_NIC\_スイッチ\_vport\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)が、その後のドライバーによって発行され、vportstate がアクティブ化された状態に変更されるためです。

    既定以外の VPort がアクティブになると、PF ミニポートドライバーは、 [**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)を通じて割り当てられた共有メモリなど、vport のリソースを割り当てることができます。 PF ミニポートドライバーは、アクティブになった後、いつでも VPort のリソースを割り当てることができます。この場合、ドライバーは、oid\_NIC\_スイッチの OID セット要求を使用して vport を削除[\_\_VPORT を削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)します。

-   既定の VPort は常にアクティブ化された状態です。 **Vportstate**メンバーの値は、既定の vport の場合は常に**NdisNicSwitchVPortStateActivated**に設定する必要があります。

-   VPort がアクティブ化された状態の場合、非アクティブ化することはできません。 PF ミニポートドライバーは、アクティブな状態の場合にのみ、VPort からパケットを受信して送信することができます。また、対応する MAC フィルターが VPort に設定されている必要があります。 ただし、oid\_\_NIC の oid セット要求を使用して VPort を削除した後[\_VPORT を削除\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)には、ドライバーは vport に割り当てられたリソースを解放する必要があります。 また、ドライバーは、VPort のパケットに対する保留中の送信操作または受信操作をすべてキャンセルする必要があります。

PF ミニポートドライバーが oid\_NIC の OID セット要求を受信した後、 [VPORT\_パラメーター\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)は、構成パラメーターを使用してハードウェアを構成します。 ドライバーは、ndis\_NIC によって識別される構成パラメーターのみを変更できます\_スイッチ\_VPORT\_パラメーター\_*Xxx*\_変更したフラグを NDIS\_Nic の**フラグ**メンバーで[ **@no__t11_ スイッチ\_VPORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体に切り替えます。

 

 





