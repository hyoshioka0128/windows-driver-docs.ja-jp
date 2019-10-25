---
title: DMA での直接 i/o の使用
description: DMA での直接 i/o の使用
ms.assetid: 0e609613-9023-4f35-a9c5-d68c8b676cfe
keywords:
- ダイレクト i/o WDK カーネル
- WDK i/o のバッファー、ダイレクト i/o
- データバッファー WDK i/o、ダイレクト i/o
- I/o WDK カーネル、ダイレクト i/o
- DMA 転送 WDK カーネル、ダイレクト i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b22391e5274569c37adf7be88bb64696b638e50a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838361"
---
# <a name="using-direct-io-with-dma"></a>DMA での直接 i/o の使用





次の図は、i/o マネージャーが、ダイレクト i/o を使用する DMA 転送操作の[**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)要求を設定する方法を示しています。

![dma を使用するデバイスのユーザーバッファーの直接 i/o を示す図](images/3mdldrct.png)

前の図は、ドライバーが IRP の**Mdladdress**を使用して読み取り要求のデータを転送する方法を示しています。 この図のドライバーでは、パケットベースのシステムまたはバスマスタ DMA を使用し、デバイスオブジェクトの**フラグ**を\_DIRECT\_IO によって処理します。

1.  一部のユーザー領域の仮想アドレスは、現在のスレッドのバッファーを表します。また、実際には、バッファーの内容が物理的に連続していない複数のページに格納されている可能性があります (前の図では濃い網掛け)。 I/o マネージャーによって、このバッファーを記述する MDL が作成されます。 MDL は、メモリマネージャーによって定義される不透明なデータ構造で、特定の仮想アドレス範囲を1つ以上のページベースの物理アドレス範囲にマップします。 詳細については、「 [MDLs の使用](using-mdls.md)」を参照してください。

2.  I/o マネージャーは、現在のスレッドの読み取り要求をサービスします。この要求は、バッファーを表すユーザー領域の仮想アドレスの範囲を渡します。

3.  I/o マネージャーまたはファイルシステムドライバー (FSD) は、ユーザーが指定したバッファーにアクセシビリティがあるかどうかを確認し、以前に作成した MDL で[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)を呼び出します。 また、 **MmProbeAndLockPages**は、MDL 内の対応する物理アドレス範囲も入力します。

    前の図に示すように、仮想範囲の MDL は、対応する複数のページベースの物理アドレスエントリを持つことができ、バッファーの仮想範囲は、MDL によって記述された最初と最後のページの先頭からのバイトオフセットで開始および終了する場合があります。

4.  I/o マネージャーは、転送操作を要求する IRP 内の MDL (**Mdladdress**) へのポインターを提供します。 ドライバーが IRP を完了した後、i/o マネージャーまたはファイルシステムによって[**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)が呼び出されるまで、MDL に記述されている物理ページはロックダウンされ、バッファーに割り当てられたままになります。 ただし、このような MDL の仮想アドレスは、IRP がデバイスドライバーに送信される前や、デバイスドライバーの上位にある中間ドライバーに送信される前でも、非表示 (および無効) になることがあります。

5.  ドライバーがパケットベースのシステムまたはバスマスタ DMA を使用する場合、その[*Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンは、IRP の**mdladdress**ポインターを使用して[**mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、MDL のページベースのエントリのベース仮想アドレスを取得します。

6.  次に、 *Adaptercontrol*ルーチンは、 **Mmgetmdlvirtualaddress**から返されたベースアドレスを使用して[**maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)を呼び出し、デバイスから直接物理メモリにデータを読み取ります。 (詳細については、「[アダプタオブジェクトと DMA](adapter-objects-and-dma.md)」を参照してください)。

ドライバーは、常にバッファーの長さを確認する必要があります。 I/o マネージャーでは、長さ0のバッファー用に MDL が作成されないことに注意してください。

 

 




