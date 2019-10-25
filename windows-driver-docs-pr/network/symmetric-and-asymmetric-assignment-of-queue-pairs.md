---
title: キュー ペアの対称および非対称割り当て
description: キュー ペアの対称および非対称割り当て
ms.assetid: B4BA1567-D536-4E7D-924C-7476FB82DAEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b10f4a40f3dd5038630f859f39c8b4038a2c5480
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841788"
---
# <a name="symmetric-and-asymmetric-assignment-of-queue-pairs"></a>キュー ペアの対称および非対称割り当て


キューのペアは、ネットワークアダプター上の個別の送信キューと受信キューで構成されます。 キューペアは、VPort が作成されるときに仮想ポート (VPort) で構成されます。 既定の VPort に関連付けられているキューのペアは、スイッチ作成時に、oid [\_NIC\_スイッチ\_作成\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)の oid メソッド要求によって構成されます。 Oid\_NIC\_スイッチの OID メソッド要求を使用して、既定以外の VPort で1つ以上のキューペアが構成され、 [\_vport\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)されます。

既定以外の各 VPort は、異なる数のキューペアを持つように構成できます。 これは、キューペアの*非対称割り当て*と呼ばれます。 ミニポートドライバーで非対称割り当てがサポートされていない場合、既定以外の各 VPort は、同じ数のキューペアを持つように構成されます。 これは、キューペアの*対称割り当て*と呼ばれます。

ミニポートドライバーは、 [**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の構造を使用して、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)中に vport とキューのペア機能をアドバタイズします。 ドライバーは、\_の既定以外の\_VPORT に対して、NDIS\_NIC\_スイッチ\_CAP\_非対称\_キュー\_のペアを設定することによって、キューペアの非対称割り当てのサポートをアドバタイズ\_この構造体の**NicSwitchCapabilities**メンバーでサポートされているフラグ。

ミニポートドライバーで非対称キューペアの割り当てがサポートされている場合、仮想化スタックによって、異なる数のキューペアを持つ既定以外の各 VPort が構成されます。 ミニポートドライバーで対称キューペアの割り当てがサポートされている場合、仮想化スタックは、同じ数のキューペアを使用して各 VPort を構成します。

  既定以外の VPorts で対称または非対称のキューペアの割り当てをサポートするミニポートドライバーでは、既定の Vports で異なる数のキューペアを割り当てる必要がある**ことに注意**してください。 既定の VPort は、常にネットワークアダプターの PF に接続されます。

 

キューのペアの構成は、Oid 要求の oid 要求を使用して既定以外の VPort を作成または更新するときに指定されます[\_nic\_スイッチ\_\_vport](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)と[oid\_nic\_スイッチ\_vport\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)。 構成パラメーターは、両方の OID 要求に関連付けられた[**VPORT\_parameters 構造\_、NDIS\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)で指定されます。

たとえば、次のように、 [**NDIS\_nic\_スイッチ\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体の次のメンバーを設定することによって、nic スイッチで vports とキューペアの構成をアドバタイズするとします。

-   **Maxnumqueuepairs**は128に設定されています。

-   **Maxnumvports**は64に設定されています。

-   **MaxNumQueuePairsPerNonDefaultPort**は4に設定されています。

ミニポートドライバーで、既定以外の VPorts におけるキューペアの非対称構成がサポートされていない場合、仮想化スタックは、VPorts の作成時に次のキューペア構成を指定できます。

-   63 2 つのキューペアを持つ既定以外の VF VPorts と、1つのキューペアを持つ既定の PF Vports。
-   それぞれが1つのキューペアを持つ既定の PF Vports と共に4つのキューペアを持つ既定以外の VF VPorts。

**注**  Windows Server 2012 以降では、既定の vport が1つだけサポートされており、常にネットワークアダプターの PF に接続されています。

 

 

 





