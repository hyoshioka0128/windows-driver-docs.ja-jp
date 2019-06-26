---
title: 仮想ポートのパラメーターのクエリ
description: 仮想ポートのパラメーターのクエリ
ms.assetid: 482DA041-2C70-438A-8D29-0F338CDCF935
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cec4cfcfa45094f724e5fdeb7a6fedc36ef21937
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379178"
---
# <a name="querying-the-parameters-of-a-virtual-port"></a>仮想ポートのパラメーターのクエリ


上にある、ドライバーは、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの NIC スイッチの仮想ポート (VPort) のパラメーターを取得できます。 ドライバーの問題のオブジェクト識別子 (OID) メソッド要求[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)これらのパラメーターを取得します。

上にあるドライバーはこの OID メソッド要求を発行前に初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体。 ドライバーは、次のようにこの構造体のメンバーを設定する必要があります。

-   **SwitchId**メンバーは、パラメーターが返されるには、NIC のスイッチの識別子を設定する必要があります。

    **注**  以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、*既定 NIC スイッチ*します。 **SwitchId** NDIS にメンバーを設定する必要があります\_既定\_スイッチ\_id。

     

-   **VPortId** VPort に関連付けられている識別子にメンバーを設定する必要があります。 上にあるドライバーは、次の方法のいずれかで VPort 識別子を取得します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_ENUM\_拡張](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)します。

この OID メソッド要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体ポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体。 この構造体には、指定した VPort のパラメーターが含まれています。

NDIS ハンドル、 [OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)ミニポート ドライバーに要求します。 NDIS は、次のソースを調べることから保持されているデータの内部キャッシュから情報を返します。

-   OID メソッド要求[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

-   OID の要求を設定する[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)します。

 

 





