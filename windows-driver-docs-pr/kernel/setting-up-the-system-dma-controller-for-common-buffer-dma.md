---
title: 共通バッファー DMA 用のシステム DMA コントローラーのセットアップ
description: 共通バッファー DMA 用のシステム DMA コントローラーのセットアップ
ms.assetid: 279776e0-dead-4763-9aae-33950837c27c
keywords:
- システム DMA WDK カーネルでは、一般的なバッファー
- 一般的なバッファー DMA WDK カーネル
- DMA は、WDK カーネルでは、一般的なバッファーを転送します。
- AllocateAdapterChannel
- MapTransfer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52173d03b09ab3259c44d6336483a306ea536999
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371244"
---
# <a name="setting-up-the-system-dma-controller-for-common-buffer-dma"></a>共通バッファー DMA 用のシステム DMA コントローラーのセットアップ





ときに**AllocateAdapterChannel**にドライバーの制御を転送[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control) 、日常的なドライバー"所有"するシステム DMA コント ローラーと、マップのレジスタのセット。 次に、ドライバーを呼び出す必要があります[ **MapTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)ドライバーは、転送操作のデバイスを設定する前に、ドライバーに割り当てられた共通バッファーを使用するシステムの DMA コント ローラーを設定します。

ドライバーには、次のパラメーターを提供する**MapTransfer**:

-   によって返されるアダプター オブジェクト ポインター **IoGetDmaAdapter**

-   ドライバーによって割り当てられた一般的なバッファーを記述する MDL へのポインター

-   *MapRegisterBase*にドライバーのハンドルが渡される*AdapterControl*で日常的な**AllocateAdapterChannel**

-   変数へのポインター (*長さ*) ドライバーに割り当てられた一般的なバッファーのバイト サイズを示す

-   転送操作 (デバイスへのシステム メモリから要求された転送 TRUE) の方向を示すブール値

**MapTransfer** DMA を無視する必要がありますどのドライバーがシステムを使用する、論理アドレスを返します。 ときに**MapTransfer**コントロールを返します、ドライバーは、DMA 操作には、そのデバイスを設定する必要があります。 ドライバー呼び出し**MapTransfer** 1 回だけが、要求された転送が完了するまで、一般的なバッファーのロックされたユーザー バッファーとの間でデータをコピーするにが続行されます。

ドライバーが呼び出せる[ **ReadDmaCounter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pread_dma_counter)を決定するバイト数現在されません一般的なバッファーで転送されるユーザー データまたはデータのコピーをその共通のバッファーに入力を続行できますドライバー。DMA 操作の方向に応じて、ユーザーのバッファーに、一般的なバッファーから

転送が完了すると、ドライバーを呼び出す場合は、ドライバーは IRP のエラー状態を返す必要があります、 [ **FlushAdapterBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pflush_adapter_buffers) DMA システムにキャッシュされているすべてのデータを確実に、コント ローラーがシステムに読み込まれるメモリまたはデバイスに書き込まれます。 ドライバーを呼び出す必要がありますし、 [ **FreeAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel) (自体を含む) 任意のドライバーで使用するためのシステム DMA コント ローラーを解放するには、すぐにします。

 

 




