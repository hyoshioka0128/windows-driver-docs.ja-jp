---
title: ネットワーク アダプターでの仮想ポートの列挙
description: ネットワーク アダプターでの仮想ポートの列挙
ms.assetid: 437C3356-4CC7-4128-9E61-FD01157F4FD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb889837882d83edc26e7b47fedc3b8e7ed9dd9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834767"
---
# <a name="enumerating-virtual-ports-on-a-network-adapter"></a>ネットワーク アダプターでの仮想ポートの列挙


接続されているドライバーまたはユーザーアプリケーションは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターの NIC スイッチ上にあるすべての仮想ポート (VPorts) の一覧を取得できます。 この一覧を取得するには、ドライバーまたはアプリケーションが[oid\_NIC\_スイッチ\_列挙型\_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)のオブジェクト識別子 (oid) メソッド要求を発行します。

この OID クエリ要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、次を含むバッファーへのポインターが含まれています。

-   [**NDIS\_NIC\_スイッチ\_VPORT\_INFO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)配列内の要素の数を定義する配列構造体です。

-   [**NDIS\_NIC\_スイッチ\_VPORT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)構造体の配列。 これらの各構造体には、ネットワークアダプターの NIC スイッチの VPort に関する情報が含まれています。

    **注**  ネットワークアダプターに vports が作成されていない場合、ドライバーは[**ndis\_NIC\_\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)の**numelements**メンバーを0に設定し、 [**NDIS\_NIC\_スイッチ\_vports\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)構造体が返されます。\_\_

     

前のドライバーまたはユーザーアプリケーションが[OID\_nic\_スイッチ\_列挙\_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)要求を発行する前に、要求と共に渡される[**NDIS\_nic\_スイッチ\_VPORTS\_INFO\_ARRAY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)構造体を初期化する必要があります。 **NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**構造体を初期化するときは、ドライバーまたはアプリケーションが次のガイドラインに従う必要があります。

-   NDIS\_NIC\_スイッチ\_VPORT\_INFO\_ARRAY\_特定の\_スイッチフラグが**Flags**メンバーで設定されている場合は、指定された NIC スイッチで作成されたすべての vport に関する情報が返されます。\_\_ NIC スイッチは、その構造体の**Switchid**メンバーによって指定されます。

    **注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは*既定の NIC スイッチ*と呼ばれ、NDIS\_既定\_スイッチ\_ID 識別子によって参照されます。 **Flags**メンバーで設定されているフラグに関係なく、 **SWITCHID**メンバーを NDIS\_既定\_スイッチ\_ID に設定する必要があります。

     

-   NDIS\_NIC\_スイッチ\_VPORT\_INFO\_ARRAY\_特定の\_関数フラグが**Flags**メンバーで設定されている場合は、ネットワークアダプターの指定された PCI Express (PCIe) 物理機能 (PF) または仮想関数 (VF) に接続されているすべての vport について情報が返されます。\_\_ PF または VF は、その構造体の**AttachedFunctionId**メンバーによって指定されます。

    **AttachedFunctionId**メンバーが NDIS\_PF\_関数\_ID に設定されている場合、すべての vports に関する情報が返されます。 これには、PF に接続されている既定の VPort が含まれます。 **AttachedFunctionId**メンバーが有効な vf 識別子に設定されている場合、指定された vf に接続されているすべての vports に関する情報が返されます。

    **注**  Windows Server 2012 以降では、VF にアタッチできる既定以外の vport は1つだけです。 ただし、複数の VPorts (既定の Vports を含む) を PF に接続することはできます。

     

-   **Flags**メンバーが0に設定されている場合、ネットワークアダプターの PF または VF に接続されているすべての vports に関する情報が返されます。 この場合、 **Switchid**と**AttachedFunctionId**の値は無視されます。

NDIS は、ミニポートドライバーに対する[ENUM\_VPORTS 要求\_、OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)を処理します。 NDIS は、次のソースを検査して、管理するデータの内部キャッシュから情報を返します。

-   Oid\_の oid メソッドの要求[\_スイッチ\_\_VPORT を作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

-   Oid\_の oid セット要求は、 [VPORT\_パラメーター\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)に設定します。

 

 





