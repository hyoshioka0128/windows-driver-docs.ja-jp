---
title: 仮想ポート経由のパケット フロー
description: 仮想ポート経由のパケット フロー
ms.assetid: 1E4B1987-3288-4082-B8A8-0F275C61597F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fe218833e36293906e2876a0cfec31c47a2c3e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843717"
---
# <a name="packet-flow-over-a-virtual-port"></a>仮想ポート経由のパケット フロー


既定の NIC スイッチは、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートするネットワークアダプターのコンポーネントです。 スイッチは常に既定の仮想ポート (VPort) を PCI Express (PCIe) 物理機能 (PF) にアタッチします。 スイッチは、1つまたは複数の既定以外の VPorts を PF に接続できます。 詳細については、「[仮想ポートの作成](creating-a-virtual-port.md)」を参照してください。

次の点は、PF に接続されている VPort で送受信されるパケットに適用されます。

-   既定の VPort を介して送受信されたパケットは、vport 識別子の値 **\_vport\_ID**で指定されます。

    既定以外の VPorts 経由で送受信されたパケットは、 [\_vports を作成\_の oid\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)によって、vports が作成されたときに返された vports 識別子と共に指定されます。 ドライバーは、この OID 要求を処理するときに、 [**NDIS\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)の**VPortId**メンバーから vport 識別子を取得します。これは、oid 要求に関連付けられている vport\_PARAMETERS 構造\_ます。

    **注**  vport が削除されると、ミニポートドライバーが、無効な**VPortId**値を含む NBL を受信する可能性があります。 この場合、ミニポートは無効な VPort ID を無視し、代わりに**既定の\_vport\_ID**を使用します。 **VPortId**は NBL の OOB データの**NetBufferListFilteringInfo**部分にあり、NET\_BUFFER\_LIST を使用して取得され[ **\_\_FILTER\_VPORT\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)マクロを受信します。

     

-   PF ミニポートドライバーは、VPort から受信したパケットを示すために[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出します。 PF ミニポートドライバーは、 **NdisMIndicateReceiveNetBufferLists**を呼び出す前に、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造にある帯域外 (OOB) データの vport 識別子を設定する必要があります。 このドライバーは、 [**NET\_BUFFER\_LIST を使用して、VPORT\_ID マクロ\_受信\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)を使用してこれを行います。

-   仮想化スタックは[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)を呼び出して、パケットを vport に送信します。 仮想化スタックは**NdisSendNetBufferLists**を呼び出す前に、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造にある OOB データの vport 識別子を設定します。

    ミニポートドライバーは\_、vport [ **\_id マクロ\_受信\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)を使用して、vport 識別子を取得\_ます。

    ミニポートドライバーは、指定された VPort のハードウェア転送キューで送信パケットをキューに入れます。

  、PCIe 仮想機能 (VF) のミニポートドライバーでは、パケットの[**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の OOB データの vport 識別子が設定または照会されない**ことに注意**してください。 VF ミニポートドライバーは、パケットを送信するときに、VF に接続されている単一の既定以外の VPort について、ハードウェア転送キューのパケットをキューに入れます。

 

 

 





