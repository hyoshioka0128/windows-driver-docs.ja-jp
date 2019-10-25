---
title: SAN プロキシ ドライバーのメモリの割り当てと解放
description: SAN プロキシ ドライバーのメモリの割り当てと解放
ms.assetid: c196f202-159c-4296-9888-818eaeaada73
keywords:
- プロキシドライバー WDK San、メモリ割り当て
- SAN プロキシドライバー WDK、メモリ割り当て
- メモリ割り当て (WDK San)
- SAN プロキシドライバーのメモリの解放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 377cf022ed73ffbae8a4809cbe44457d6dad0d40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838231"
---
# <a name="allocating-and-releasing-memory-for-a-san-proxy-driver"></a>SAN プロキシ ドライバーのメモリの割り当てと解放





プロキシドライバーは、Windows ソケットスイッチが制御メッセージを転送し、RDMA 操作を実行できるように、ユーザーバッファーへのアクセスを設定する必要があります。 この種類のバッファーアクセスを要求するために、プロキシドライバーは、デバイスオブジェクトの**Flags**メンバーにビットを設定して、IO を直接\_\_します。 また、プロキシドライバーは、メッセージの転送に使用されるメモリの割り当てまたは解放を行う必要があります。 Windows ソケットスイッチが SAN サービスプロバイダーに対してメモリの登録または解放を要求すると、SAN サービスプロバイダーは、それぞれのプロキシドライバーに対して、物理メモリの割り当てまたは解放を要求します。 バッファーアクセスの設定およびメモリの割り当てと解放の詳細については、「[メモリ管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-memory-for-drivers)と[バッファー管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

### <a name="allocating-low-memory-for-rdma"></a>RDMA のメモリ不足に割り当てています

プロキシドライバーは、RDMA 操作のためにアクセスできるメモリを割り当てる必要があります。 プロキシドライバーは、4 GB 未満の物理メモリを割り当てることができないように構成されているシステムであっても、RDMA 操作に低メモリを割り当てることができます。 (これを NOLOWMEM 構成と呼びます)。プロキシドライバーは、 [**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)関数またはその独自の DMA [**Allocatecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)関数を呼び出して、メモリ不足を取得します。

DMA **Allocatecommonbuffer**関数へのポインターを取得するために、プロキシドライバーは次の手順を実行します。

1.  [**デバイス\_説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description)の構造をゼロに初期化し、その SAN NIC に関連する情報をこの構造体に書き込みます。

2.  [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)を呼び出して、その SAN NIC の DMA アダプター構造へのポインターを取得します。 この呼び出しでは、ドライバーは、入力されたデバイス\_記述構造体へのポインターを渡します。 **IoGetDmaAdapter**は、DMA [ **\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)構造体へのポインターを含む dma アダプター構造体へのポインターを返します。 DMA\_操作には、システム定義の一連の DMA 関数へのポインターが含まれています。 これらの関数の1つは、物理的に連続する DMA バッファーを割り当てる**Allocatecommonbuffer**です。

 

 





