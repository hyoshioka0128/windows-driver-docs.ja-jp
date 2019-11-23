---
title: NIC スイッチのパラメーターの設定
description: NIC スイッチのパラメーターの設定
ms.assetid: 79B4B0B7-32AB-4AE4-ACD2-CE17C93573BA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15832bd122143b09587454b51b0a334506c2eda3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841932"
---
# <a name="setting-the-parameters-of-a-nic-switch"></a>NIC スイッチのパラメーターの設定


前のドライバーでは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターで作成された NIC スイッチのパラメーターを変更できます。 このドライバーは、Oid\_のオブジェクト識別子 (OID) セット要求を発行し、 [\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)を変更して、これらのパラメーターを変更\_します。 SR-IOV アダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーのみが、この OID セット要求を処理します。

それより前のドライバーは、この OID セット要求を発行する前に、NIC スイッチで変更されるパラメーターを使用して、 [ **\_parameters 構造\_スイッチの NDIS\_nic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)を初期化する必要があります。 次に、OID 要求の[**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を初期化し、 **Informationbuffer**メンバーを**ndis\_NIC\_スイッチ\_PARAMETERS**構造体のポインターに設定します。

変更できるのは、NIC スイッチの構成パラメーターの一部のみです。 前のドライバーでは、 [**NDIS\_NIC\_スイッチ\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体の次のメンバーを設定することによって、変更するパラメーターを指定します。

-   **Switchid**メンバーは、パラメーターが変更される NIC スイッチの識別子に設定されます。

    **注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは、既定の*NIC スイッチ*と呼ばれます。 **Switchid**メンバーを NDIS\_既定\_スイッチ\_ID に設定する必要があります。

     

-   適切な NDIS\_NIC\_スイッチ\_パラメーター\_*Xxx*\_変更したフラグが**フラグ**メンバーで設定されます。 [**Ndis\_nic\_スイッチ\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体のメンバーは、対応する NDIS\_NIC\_スイッチ\_パラメーター\_*Xxx*\_changed フラグが Ntddndis で定義されている場合にのみ変更できます。

-   Ndis [ **\_nic\_スイッチ\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体は、NDIS\_NIC\_スイッチに対応しています。\_\_*Xxx*\_**フラグ**メンバーで設定されている変更されたフラグは、変更される NIC スイッチの構成パラメーターで設定されます。

    **注**  Windows Server 2012 以降では、 [**NDIS\_nic\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造の**switchname**メンバーのみを変更できます。 oid の Oid セット要求では、 [oid\_nic\_スイッチ\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)を使用して変更できます。

     

PF ミニポートドライバーは、 [oid\_NIC\_スイッチ\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)の oid セット要求を受信するときに、これらのガイドラインに従う必要があります。

-   PF ミニポートドライバーがネットワークアダプターの再初期化を必要とせずに変更を適用できる場合、ドライバーは変更をハードウェアに適用し、NDIS\_STATUS\_SUCCESS による OID 要求を完了します。

    この状態コードが返された場合、NDIS はレジストリ内の NIC スイッチの構成情報を更新します。

-   PF ミニポートドライバーが変更を適用するためにネットワークアダプターを再初期化する必要がある場合、ドライバーは NDIS\_STATUS\_REINIT\_必要な OID 要求を完了します。

    この状態コードが返された場合は、NDIS によって、レジストリ内の NIC スイッチの構成情報も更新されます。 ただし、OID セット要求を発行した後のドライバーは、変更を有効にするためにネットワークアダプターを再初期化する必要があります。

    **注意**  静的 NIC の作成と構成をサポートする PF ミニポートドライバーでは、新しいパラメーターが有効になるようにアダプターが再初期化されるように、NDIS\_STATUS\_REINIT\_必要になる場合があります。

     

-   PF ミニポートドライバーが OID に要求された変更を適用できない場合、OID を失敗させて、適切な NDIS\_状態\_*Xxx*コードを返す必要があります。

    この場合、NDIS はレジストリ内の NIC スイッチの構成情報を更新しません。

 

 





