---
title: 仮想ポートを削除します。
description: 仮想ポートを削除します。
ms.assetid: CBE7AC59-D878-44BA-8FE6-168EC17A2D67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b612265ed2aa877eab4eed80ae6e31cb99c6a0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549277"
---
# <a name="deleting-a-virtual-port"></a>仮想ポートを削除します。


上位のドライバーのオブジェクト識別子 (OID) セット要求を発行する[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)ネットワーク アダプターの既定以外の仮想ポート (VPort) を削除するにはNIC のスイッチです。 上にあるドライバーが削除できるがの OID メソッド要求を発行して以前作成した VPort だけ[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_削除\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451577)構造体。

など、仮想化スタックの上にあるドライバーは、既定以外が以前に作成した VPort を削除できます。 上にあるドライバーの OID メソッド要求を発行して、VPort を作成します[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。

OID のセット要求を発行する前に[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)、上にあるドライバーは、次を実行する必要があります。

-   上にあるドライバーをオフにまたは、すべての受信、ドライバーは以前、VPort 上、VPort の削除する前に設定するフィルターを移動する必要があります。 受信の OID 要求のフィルターが設定[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)が移動の OID 要求を通じて[OID\_受信\_フィルター\_移動\_フィルター](https://msdn.microsoft.com/library/windows/hardware/hh451845)します。

-   上にあるドライバー セット、 **VPortId**のメンバー、 [ **NDIS\_NIC\_スイッチ\_削除\_VPORT\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451577)構造体を削除する VPort 既定以外の識別子。

    **注**  上にあるドライバーを設定する必要がありますいない、 **VPortId**メンバー **NDIS\_既定\_ポート\_数**。 この VPort 識別子は、既定値を PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターに関連付けられている VPort の予約されています。 VPort は常に存在し、OID の要求を設定する場合と明示的に削除されませんが、既定[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)します。

     

上にあるドライバー呼び出し[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)問題を[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)基になる PF ミニポート ドライバーに要求します。 ミニポート ドライバーが、OID を受信すると\_NIC\_スイッチ\_削除\_VPORT 要求と、ドライバーは、次を実行する必要があります。

-   ドライバーは、指定した VPort の割り当てられたハードウェアとソフトウェアのリソースを解放する必要があります。

-   ドライバーは、PF または PCIe 仮想機能 (VF) から指定した VPort をデタッチする必要があります。

    VPort が、VF に接続されている場合、仮想化スタックにより、ゲスト オペレーティング システムで実行されている VF ミニポート ドライバーがされて以前一時停止され (停止)。 その結果、すべて previouslyindicated がパケットを受信、VPort から VF ミニポート ドライバーに返される必要があります。

    VPort が PF に接続されている場合、PF ミニポート ドライバーは、VPort に関連付けられている共有メモリを追加、DMA を停止する必要があります。 PF のミニポート ドライバーがすべて previouslyindicated が、VPort からパケットを受信することを確認してください、ミニポートに返されます。 PF ミニポート ドライバーを追加する必要があります行わない受信パケットの VPort の識別子を指定する NDIS に表示[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 パケットの受信、VPort からすべての後に返されます、PF ミニポート ドライバーでは、呼び出すことによって、VPort に関連付けられている共有メモリを解放する必要があります[ **NdisFreeSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562601)します。

次の点は、拡張の削除に適用されます。

-   上位のプロトコル ドライバーに拡張する前に作成した既定値以外のすべてを削除する必要がありますを呼び出す[ **NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)します。

-   上にあるフィルター ドライバーは、拡張内で作成した既定値以外のすべてを削除する必要があります、 [ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)関数。

-   NDIS のセット要求を発行する前に[OID\_NIC\_切り替える\_削除\_切り替える](https://msdn.microsoft.com/library/windows/hardware/hh451817)ネットワーク アダプターで NIC スイッチを削除するのにはすべて既定以外の拡張が削除されたことを保証そのスイッチ。

-   既定の OID 要求を通じて、拡張を明示的に削除できる以外のみ[OID\_NIC\_スイッチ\_削除\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451817)します。 PF のミニポート ドライバーが既定の NIC スイッチを削除するときに既定 VPort は暗黙的に削除されます。 詳細については、次を参照してください。 [NIC スイッチを削除する](deleting-a-nic-switch.md)します。

 

 





