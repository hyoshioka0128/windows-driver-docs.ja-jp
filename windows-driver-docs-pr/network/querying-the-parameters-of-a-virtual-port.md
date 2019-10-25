---
title: 仮想ポートのパラメーターのクエリ
description: 仮想ポートのパラメーターのクエリ
ms.assetid: 482DA041-2C70-438A-8D29-0F338CDCF935
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78e37bc1d220a3bcf044345759e986db7f12f8c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844873"
---
# <a name="querying-the-parameters-of-a-virtual-port"></a>仮想ポートのパラメーターのクエリ


1つ前のドライバーは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターで、NIC スイッチの仮想ポート (VPort) のパラメーターを取得できます。 このドライバーは、これらのパラメーターを取得するために、オブジェクト識別子 (OID) のメソッド要求[oid\_NIC\_スイッチ\_VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)を発行します。

それまでのドライバーは、この OID メソッド要求を発行する前に、 [**NDIS\_NIC\_スイッチ\_VPORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体を初期化する必要があります。 ドライバーは、この構造体のメンバーを次のように設定する必要があります。

-   **Switchid**メンバーは、パラメーターが返される NIC スイッチの識別子に設定されている必要があります。

    **注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは、既定の*NIC スイッチ*と呼ばれます。 **Switchid**メンバーを NDIS\_既定\_スイッチ\_ID に設定する必要があります。

     

-   **VPortId**メンバーは、vport に関連付けられた識別子に設定する必要があります。 このドライバーは、次のいずれかの方法で VPort 識別子を取得します。

    -   Oid\_の以前の OID メソッド要求から、 [\_VPORT を作成\_\_スイッチに切り替え](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)ます。

    -   Oid\_NIC の以前の OID メソッド要求から、[列挙型\_VPORTS\_スイッチ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)ます。

この OID メソッド要求から正常に戻った後、 [**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ\_vport へのポインターが含まれ\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体。 この構造体には、指定した VPort のパラメーターが含まれます。

NDIS は、ミニポートドライバーに対する[VPORT\_PARAMETERS 要求\_、OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)を処理します。 NDIS は、次のソースを検査して、管理するデータの内部キャッシュから情報を返します。

-   Oid\_の oid メソッドの要求[\_スイッチ\_\_VPORT を作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

-   Oid\_の oid セット要求は、 [VPORT\_パラメーター\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)に設定します。

 

 





