---
title: NIC スイッチの動的作成
description: NIC スイッチの動的作成
ms.assetid: 16B2D94A-AF30-434F-8F14-2F535501A52F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d0678d441e6e43670ebfcba70f1772cd9bc0f13
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834809"
---
# <a name="dynamic-creation-of-a-nic-switch"></a>NIC スイッチの動的作成


シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターでは、NIC スイッチを作成できる必要があります。 一部のアダプターでは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)への呼び出しからミニポートドライバーが返された後に、NIC スイッチを動的に作成できます。

アダプターに NIC スイッチを作成できるのは、SR-IOV アダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーだけです。

**注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは*既定の NIC スイッチ*と呼ばれ、NDIS\_既定\_スイッチ\_ID 識別子によって参照されます。

 

NDIS は、Oid のオブジェクト識別子 (OID) メソッド要求を発行[\_nic\_スイッチ\_作成\_スイッチを作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)して、sr-iov ネットワークアダプターに nic スイッチを作成します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、スイッチのパラメーターを含む[**NDIS\_NIC\_\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)へのポインターが含まれています。

PF ミニポートドライバーで動的な NIC スイッチの作成がサポートされている場合は、次の手順に従って、この OID 要求を処理する必要があります。

1.  PF ミニポートドライバーは、これらのパラメーターに基づいて、NIC スイッチに必要なハードウェアおよびソフトウェアリソースを割り当てます。 また、ドライバーは、これらのパラメーターを使用してネットワークアダプターを構成します。

    **注**  動的な NIC スイッチの作成をサポートする PF ミニポートドライバーでは、レジストリの標準化された sr-iov キーワード設定を使用してスイッチパラメーターを読み取る必要はありません。 NDIS は、これらのキーワードを読み取って、 [**ndis\_nic\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造を初期化します。これにより、\_スイッチ要求の作成\_、 [OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)が発行されます。 これらのキーワードの詳細については、「sr-iov[用の標準化](standardized-inf-keywords-for-sr-iov.md)された INF キーワード」を参照してください。

     

2.  ミニポートドライバーは、 [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出して sr-iov を有効にし、ネットワークアダプターの VFs の数を設定します。 この関数は、アダプターの PCI 構成領域で sr-iov 拡張機能を構成します。 この関数が NDIS\_STATUS\_SUCCESS を返した場合、SR-IOV が有効になり、VFs が PCIe インターフェイスを介して公開されます。

[Oid\_nic\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)を処理する方法の詳細については\_\_スイッチ要求の作成に関する詳細については、「 [oid\_Nic\_を処理](handling-the-oid-nic-switch-create-switch-request.md)する\_スイッチ要求を作成する」を参照してください。\_

 

 





