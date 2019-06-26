---
title: NIC スイッチの削除
description: NIC スイッチの削除
ms.assetid: BCC6A38B-F25B-483A-B9FF-D6FF73F9B2F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 680344aa43298ddb203945eb3f5133ebe77466b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354585"
---
# <a name="deleting-a-nic-switch"></a>NIC スイッチの削除


シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターは、NIC のスイッチを削除できる必要があります。 ミニポート ドライバーを PCI Express (PCIe) 物理機能 (PF) の SR-IOV 対応アダプターだけでは、アダプターで NIC スイッチを削除できます。

**注**  Windows Server 2012 で NDIS 6.30 以降、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、 *NIC スイッチの既定*、NDIS によって参照されている\_既定\_スイッチ\_ID です。

 

NDIS PF ミニポート ドライバーを停止するには前のオブジェクト識別子 (OID) セット要求を発行して、NIC のスイッチを削除します[OID\_NIC\_切り替える\_削除\_切り替える](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_切り替える\_削除\_切り替える\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)削除されているスイッチの識別子を指定する構造体。

要求の設定、OID を発行する前に、NDIS が次のポリシーを強制[OID\_NIC\_スイッチ\_削除\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)PF ミニポート ドライバーに。

-   NDIS フィルターが、すべての保証がクリアされている、既定値と既定以外の NIC スイッチ上のバーチャル ポート (拡張)。 受信フィルターの OID セット要求をクリア[OID\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)します。

-   NDIS は、すべて既定以外のバーチャル ポート (拡張) スイッチの作成が既に削除されていることを保証します。 OID セットの要求を通じて拡張を削除[OID\_NIC\_スイッチ\_削除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)します。

-   NDIS は、すべてのリソース PCIe 仮想機能 (Vf) の NIC のスイッチに接続されているが以前に解放されたことを保証します。 VFs の OID セットの要求を通じて解放[OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)します。

OID メソッド要求を受け取ったとき[OID\_NIC\_スイッチ\_削除\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)、PF ミニポート ドライバーは、次を実行する必要があります。

1.  PF のミニポート ドライバーでは、静的な作成と NIC のスイッチの構成をサポートする場合は、指定した NIC スイッチに関連付けられているソフトウェア リソースを解放にする必要があります。 ただし、ドライバーのみを解放できますハードウェア リソースの NIC を切り替えるときに[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)が呼び出されます。

    静的な NIC スイッチの作成の詳細については、次を参照してください。 [NIC スイッチの作成を静的](static-creation-of-a-nic-switch.md)します。

2.  PF ミニポート ドライバーでは、動的な作成と NIC のスイッチの構成をサポートする場合、指定した NIC スイッチに関連付けられているハードウェアおよびソフトウェア リソースを無料する必要があります。

    動的な NIC スイッチの作成の詳細については、次を参照してください。 [NIC スイッチの動的な作成](dynamic-creation-of-a-nic-switch.md)です。

3.  ドライバーが呼び出すことによってに、アダプターで仮想化を無効にする必要があります、PF ミニポート ドライバーでは、ネットワーク アダプターで NIC スイッチおよび NIC スイッチが削除されているすべての動的作成をサポートする場合[ **NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization). ネットワーク アダプターの設定を仮想化を無効にする必要があります、 *EnableVirtualization*パラメーターを FALSE と*NumVFs*パラメーターを 0 にします。

    [**NdisMEnableVirtualization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)クリア、 **NumVFs**メンバーと**VF 有効**の PCIe 構成領域で SR-IOV 拡張機能の構造内のビット、ネットワーク アダプターの PF.

    **注**  PF ミニポート ドライバーでは、静的な作成と NIC のスイッチの構成をサポートする場合のみ呼び出す必要があります[ **NdisMEnableVirtualization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)とき[*MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)が呼び出されます。

     

 

 





