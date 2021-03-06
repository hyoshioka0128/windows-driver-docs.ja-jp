---
title: キュー ペアの対称および非対称割り当て
description: キュー ペアの対称および非対称割り当て
ms.assetid: B4BA1567-D536-4E7D-924C-7476FB82DAEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 746b39becd0ec1f112eb3a1f053fdd4d5de820d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377978"
---
# <a name="symmetric-and-asymmetric-assignment-of-queue-pairs"></a>キュー ペアの対称および非対称割り当て


キュー ペアは、個別の送信で構成され、受信ネットワーク アダプターのキュー。 キュー ペアは、VPort の作成時に仮想ポート (VPort) で構成されます。 VPort がの OID メソッド要求を通じてスイッチの作成時に構成されている既定値に関連付けられているキュー ペア[OID\_NIC\_切り替える\_作成\_切り替える](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)します。 1 つまたは複数のキュー ペアは、既定以外で構成されている OID メソッドを通じて VPort 要求[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

各既定以外の VPort を構成して、キュー ペアの数が異なるすることができます。 これと呼ばれます*非対称割り当て*キュー ペアの。 ミニポート ドライバーが非対称の割り当てをサポートしていない場合は、各既定以外の VPort を構成するキューのペアの数が等しい。 これと呼ばれます*対称割り当て*キュー ペアの。

ミニポート ドライバー アドバタイズ中にその VPort とキューのペア機能[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)を使用して、 [ **NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体。 ドライバーは、NDIS を設定して、キュー ペアの非対称の割り当てのサポートをアドバタイズ\_NIC\_スイッチ\_CAP\_非対称\_キュー\_ペア\_の\_既定以外\_VPORT\_でサポートされているフラグ、 **NicSwitchCapabilities**この構造体のメンバー。

ミニポート ドライバーでは、非対称のキュー ペアの割り当てをサポートする場合、仮想化スタックは、キュー ペアの数が異なる各既定以外の VPort を構成します。 ミニポート ドライバーでは、対称キュー ペアの割り当てをサポートする場合、仮想化スタックは、キュー ペアの同じ番号を持つ各 VPort を構成します。

**注**  拡張を既定以外のいずれかの対称または非対称のキュー ペアの割り当てをサポートしているミニポート ドライバーが既定 VPort に割り当てられるようにキュー ペアの数が異なるをサポートする必要があります。 VPort の既定値は常にネットワーク アダプターの PF. に接続されています。

 

既定以外の VPort を作成または更新の OID 要求とキュー ペアの構成が指定された[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)と[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)します。 構成パラメーターがで指定された、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)両方に関連付けられている構造体OID に要求します。

たとえば、ミニポート ドライバーが次のメンバーを設定して NIC スイッチの拡張とキューのペアの構成をアドバタイズ、 [ **NDIS\_NIC\_切り替える\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体。

-   **MaxNumQueuePairs** 128 に設定されます。

-   **MaxNumVPorts** 64 に設定されます。

-   **MaxNumQueuePairsPerNonDefaultPort** 4 に設定されます。

ミニポート ドライバーでは、既定以外の拡張でキュー ペアの非対称の構成をサポートしません、拡張が作成されたときに、仮想化スタックは、次のキュー ペア構成を指定できます。

-   2 つのキューで既定以外の VF 拡張は 63 のペアごとに 1 つのキューのペアで既定の PF VPort と共に。
-   次の 4 つのキューに既定以外の VF 拡張は 31 のペアごとに 1 つのキューのペアで既定の PF VPort と共に。

**注**  VPort はサポートされているし、は、常に 1 つだけの既定は Windows Server 2012 以降では、ネットワーク アダプターの PF. にアタッチされています。

 

 

 





