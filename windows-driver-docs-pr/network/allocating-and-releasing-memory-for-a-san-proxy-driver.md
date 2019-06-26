---
title: SAN プロキシ ドライバーのメモリの割り当てと解放
description: SAN プロキシ ドライバーのメモリの割り当てと解放
ms.assetid: c196f202-159c-4296-9888-818eaeaada73
keywords:
- プロキシ ドライバー WDK San、メモリの割り当て
- SAN プロキシ ドライバー WDK、メモリの割り当て
- WDK の San のメモリ割り当て
- SAN プロキシ ドライバーのメモリを解放します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b83da9ffb5ffd48c0a05f3dfa72237f5ba3eed8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382915"
---
# <a name="allocating-and-releasing-memory-for-a-san-proxy-driver"></a>SAN プロキシ ドライバーのメモリの割り当てと解放





プロキシ ドライバーは、Windows Sockets スイッチは、コントロール メッセージを転送して RDMA の操作を実行できるように、ユーザー バッファーへのアクセスを設定する必要があります。 この種類のバッファーのアクセスを要求するプロキシ ドライバーでビットを設定、**フラグ**操作を実行するには、そのデバイス オブジェクトのメンバー\_直接\_IO。 プロキシ ドライバーは、割り当てるか、メッセージの転送、および RDMA 要求されるたびにそのために使用されるメモリを解放する必要がありますもします。 Windows Sockets スイッチは、登録、またはメモリを解放する SAN サービス プロバイダーを要求するときに、SAN サービス プロバイダーは、それぞれの割り当てまたは物理メモリを解放するには、そのプロキシ ドライバーを要求します。 バッファーへのアクセスと割り当てとメモリの解放の設定に関する詳細については、次を参照してください。[メモリ管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-memory-for-drivers)と[バッファー管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

### <a name="allocating-low-memory-for-rdma"></a>RDMA の低いメモリの割り当てください。

プロキシ ドライバーでは、rdma にアクセスできるメモリを割り当てる必要があります。 プロキシ ドライバーでは、以下の 4 GB の物理メモリを割り当てられませんように構成されている、システム上でも rdma のメモリ不足を割り当てることができます。 (これが呼び出されます NOLOWMEM 構成します。)プロキシ ドライバーを呼び出すか、 [ **MmAllocateContiguousMemorySpecifyCache** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)関数または独自の DMA [ **AllocateCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_common_buffer)メモリの下限を取得します。

その DMA へのポインターを取得する**AllocateCommonBuffer**関数の場合、プロキシ ドライバーは、次の手順を実行します。

1.  0 に初期化を[**デバイス\_説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_description)を構造化し、この構造体を SAN の NIC の関連情報を書き込みます。

2.  呼び出し[ **IoGetDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter) SAN NIC の DMA アダプターの構造体へのポインターを取得するには この呼び出しで、ドライバーは、入力デバイスにポインターを渡します\_構造を定義します。 **IoGetDmaAdapter**へのポインターを格納 DMA アダプターの構造体へのポインターを返します、 [ **DMA\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_dma_operations)構造体。 DMA\_操作には、DMA 関数のシステム定義のセットへのポインターが含まれています。 これらの関数の 1 つは**AllocateCommonBuffer**、物理的に連続する DMA バッファーを割り当てることができます。

 

 





