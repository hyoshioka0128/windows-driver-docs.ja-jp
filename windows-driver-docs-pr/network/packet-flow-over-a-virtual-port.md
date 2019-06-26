---
title: 仮想ポート経由のパケット フロー
description: 仮想ポート経由のパケット フロー
ms.assetid: 1E4B1987-3288-4082-B8A8-0F275C61597F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1720d3e243b0fa88adc112d2782509b33969bb85
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376426"
---
# <a name="packet-flow-over-a-virtual-port"></a>仮想ポート経由のパケット フロー


既定の NIC の切り替えは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートするネットワーク アダプターのコンポーネントです。 スイッチに、PCI Express (PCIe) 物理機能 (PF) 既定の仮想ポート (VPort) が常にアタッチします。 スイッチは、PF. に 1 つまたは複数の既定以外拡張をアタッチすることができます。 詳細については、次を参照してください。[仮想ポートを作成する](creating-a-virtual-port.md)します。

次の点は、PF に関連付けられている VPort に送受信パケットに適用されます。

-   パケットが送信または VPort がの VPort 識別子の値で指定された既定の経由で受信した**既定\_VPORT\_ID**します。

    パケットが送信または拡張が、VPort の OID メソッド要求を使用して作成されたときに返された VPort 識別子を持つ指定した既定以外の経由で受信した[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。 ドライバーは、この OID 要求を処理すると、VPort の識別子を取得します、 **VPortId**のメンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_。パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) OID 要求に関連付けられている構造体。

    **注**  ときに、VPort の削除、無効なを含む、NBL を受信するミニポート ドライバーの可能性が**VPortId**値。 このような場合、ミニポートする必要があります VPort ID が無効ですを無視しを使用して、**既定\_VPORT\_ID**代わりにします。 **VPortId**は、 **NetBufferListFilteringInfo** 、NBL の部分の OOB のデータとを使用して取得されて、 [ **NET\_バッファー\_一覧\_受信\_フィルター\_VPORT\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)マクロ。

     

-   PF のミニポート ドライバー呼び出し[ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を VPort から受信したパケットを示します。 PF のミニポート ドライバーの呼び出しの前に**NdisMIndicateReceiveNetBufferLists**、アウト オブ バンド (OOB) のデータの VPort 識別子を設定があります、 [ **NET\_バッファー\_一覧** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)パケットの構造体。 ドライバーはこれを使用して、 [ **NET\_バッファー\_一覧\_受信\_フィルター\_VPORT\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)マクロ。

-   仮想化スタック呼び出し[ **NdisSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissendnetbufferlists) VPort にパケットを送信します。 仮想化スタックの呼び出しの前に**NdisSendNetBufferLists**、OOB 内のデータで VPort 識別子を設定、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)パケットの構造体。

    ミニポート ドライバーを使用して VPort 識別子を取得する、 [ **NET\_バッファー\_一覧\_受信\_フィルター\_VPORT\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)マクロ。

    ミニポート ドライバーでは、指定した VPort のハードウェアの送信キューの送信パケットをキューする必要があります。

**注**  ミニポート ドライバー PCIe 仮想機能 (VF) が設定または VPort 識別子の OOB データにクエリを実行していない、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)パケットの構造体。 VF のミニポート ドライバーでは、パケットを送信するとき、VF に関連付けられている VPort の 1 つ既定以外のハードウェアの送信キューでパケットをキューします。

 

 

 





