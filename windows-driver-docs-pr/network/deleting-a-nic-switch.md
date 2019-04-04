---
title: NIC のスイッチを削除します。
description: NIC のスイッチを削除します。
ms.assetid: BCC6A38B-F25B-483A-B9FF-D6FF73F9B2F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d35b1913ce7845cdf9d89aff75b55340721e2a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536710"
---
# <a name="deleting-a-nic-switch"></a>NIC のスイッチを削除します。


シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターは、NIC のスイッチを削除できる必要があります。 ミニポート ドライバーを PCI Express (PCIe) 物理機能 (PF) の SR-IOV 対応アダプターだけでは、アダプターで NIC スイッチを削除できます。

**注**  Windows Server 2012 で NDIS 6.30 以降、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、 *NIC スイッチの既定*、NDIS によって参照されている\_既定\_スイッチ\_ID です。

 

NDIS PF ミニポート ドライバーを停止するには前のオブジェクト識別子 (OID) セット要求を発行して、NIC のスイッチを削除します[OID\_NIC\_切り替える\_削除\_切り替える](https://msdn.microsoft.com/library/windows/hardware/hh451817)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_切り替える\_削除\_切り替える\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451575)削除されているスイッチの識別子を指定する構造体。

要求の設定、OID を発行する前に、NDIS が次のポリシーを強制[OID\_NIC\_スイッチ\_削除\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451817)PF ミニポート ドライバーに。

-   NDIS フィルターが、すべての保証がクリアされている、既定値と既定以外の NIC スイッチ上のバーチャル ポート (拡張)。 受信フィルターの OID セット要求をクリア[OID\_受信\_フィルター\_クリア\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569785)します。

-   NDIS は、すべて既定以外のバーチャル ポート (拡張) スイッチの作成が既に削除されていることを保証します。 OID セットの要求を通じて拡張を削除[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)します。

-   NDIS は、すべてのリソース PCIe 仮想機能 (Vf) の NIC のスイッチに接続されているが以前に解放されたことを保証します。 VFs の OID セットの要求を通じて解放[OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)します。

OID メソッド要求を受け取ったとき[OID\_NIC\_スイッチ\_削除\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451817)、PF ミニポート ドライバーは、次を実行する必要があります。

1.  PF のミニポート ドライバーでは、静的な作成と NIC のスイッチの構成をサポートする場合は、指定した NIC スイッチに関連付けられているソフトウェア リソースを解放にする必要があります。 ただし、ドライバーのみを解放できますハードウェア リソースの NIC を切り替えるときに[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)が呼び出されます。

    静的な NIC スイッチの作成の詳細については、[NIC スイッチの作成を静的](static-creation-of-a-nic-switch.md)を参照してください。

2.  PF ミニポート ドライバーでは、動的な作成と NIC のスイッチの構成をサポートする場合、指定した NIC スイッチに関連付けられているハードウェアおよびソフトウェア リソースを無料する必要があります。

    動的な NIC スイッチの作成の詳細については、[NIC スイッチの動的な作成](dynamic-creation-of-a-nic-switch.md)を参照してください。

3.  ドライバーが呼び出すことによってに、アダプターで仮想化を無効にする必要があります、PF ミニポート ドライバーでは、ネットワーク アダプターで NIC スイッチおよび NIC スイッチが削除されているすべての動的作成をサポートする場合[ **NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481). ネットワーク アダプターの設定を仮想化を無効にする必要があります、 *EnableVirtualization*パラメーターを FALSE と*NumVFs*パラメーターを 0 にします。

    [**NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)クリア、 **NumVFs**メンバーと**VF 有効**の PCIe 構成領域で SR-IOV 拡張機能の構造内のビット、ネットワーク アダプターの PF.

    **注**  PF ミニポート ドライバーでは、静的な作成と NIC のスイッチの構成をサポートする場合のみ呼び出す必要があります[ **NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)とき[*MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)が呼び出されます。

     

 

 





