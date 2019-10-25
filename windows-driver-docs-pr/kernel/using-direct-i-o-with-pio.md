---
title: Direct i/o と PIO の使用
description: Direct i/o と PIO の使用
ms.assetid: 84d36567-c8c6-4576-91a0-829c8819de4d
keywords:
- ダイレクト i/o WDK カーネル
- WDK i/o のバッファー、ダイレクト i/o
- データバッファー WDK i/o、ダイレクト i/o
- I/o WDK カーネル、ダイレクト i/o
- PIO 転送操作 (WDK カーネル)
- プログラムによる i/o 転送 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bab1c82565ac6bbc4c502feb97411ed2bd92fe36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838366"
---
# <a name="using-direct-io-with-pio"></a>Direct i/o と PIO の使用





DMA ではなく、プログラミングされた i/o (PIO) を使用するドライバーは、ユーザー空間のバッファーをシステム領域のアドレス範囲に二重にマップする必要があります。 次の図は、i/o マネージャーが、direct i/o を使用する PIO 転送操作のために、 [**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)要求を設定する方法を示しています。

![pio を使用するデバイスの直接 i/o を示す図](images/3mdlpio.png)

この図は、PIO を使用するデバイスが同じタスクを処理する方法を示しています。

1.  一部のユーザー領域の仮想アドレスは、現在のスレッドのバッファーを表します。また、バッファーの内容は、物理的に連続していない複数のページに実際に格納される可能性があります。 バッファー長が0以外の場合、このバッファーを記述する MDL が i/o マネージャーによって作成されます。

2.  I/o マネージャーは、現在のスレッドの読み取り要求をサービスします。この要求は、スレッドがバッファーを表すユーザー空間の仮想アドレスの範囲を渡します。

3.  I/o マネージャーまたは FSD は、ユーザーが指定したバッファーにアクセシビリティがあるかどうかを確認します。 I/o マネージャーが MDL を作成した場合は、ユーザーバッファーの仮想アドレスの範囲を指定する MDL を使用して[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)を呼び出します。 また、 **MmProbeAndLockPages**は、MDL 内の対応する物理アドレス範囲も入力します。

4.  I/o マネージャーは、転送操作を要求する IRP 内の MDL (**Mdladdress**) へのポインターを提供します。 ドライバーが IRP を完了した後、i/o マネージャーまたはファイルシステムによって[**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)が呼び出されるまで、MDL に記述されている物理ページはロックダウンされ、バッファーに割り当てられたままになります。 ただし、このような MDL の仮想アドレスは、IRP がデバイスドライバーに送信される前や、デバイスドライバーの上位にある中間ドライバーに送信される前でも、非表示 (および無効) になることがあります。

5.  ドライバーがシステム (仮想) アドレスを必要とする場合、ドライバーは IRP の**Mdladdress**ポインターを使用して[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、MDL 内のユーザー領域の仮想アドレスをシステム領域のアドレス範囲にダブルマップします。 上の図では、エイリアス Buff は、二重にマップされたアドレスを記述する MDL を表しています。

6.  ドライバーは、ダブルマップされた MDL (エイリアス Buff) からのシステム領域の仮想アドレス範囲を使用して、データをメモリに読み込みます。

[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出すことによってドライバーが IRP を完了すると、ドライバーが**MmGetSystemAddressForMdlSafe**を呼び出した場合、i/o マネージャーまたはファイルシステムによって、MDL の二重マップされたシステム領域の範囲が解放されます。 I/o マネージャーまたはファイルシステムは、MDL に記述されているページのロックを解除し、ドライバーの代わりに MDL と IRP を破棄します。 パフォーマンスを向上させるために、ドライバーでは、仮想アドレスを使用する必要がある場合を除いて、手順 3. で説明したように、MDL の物理アドレスをシステム領域に二重マップする必要はありません。 これにより、システムページテーブルエントリが不必要に使用され、ドライバーのパフォーマンスとスケーラビリティの両方が低下する可能性があります。 また、ページテーブルエントリが不足していると、システムがクラッシュする可能性があります。これは、ほとんどの古いドライバーがこの状況に対処できないためです。

現在のユーザースレッドのバッファーとスレッド自体は、そのスレッドが最新の状態であることが保証されます。 前の図に示したスレッドでは、別のプロセスのスレッドが実行されている間に、そのユーザーバッファーの内容がセカンダリストレージにページアウトされる可能性があります。 別のプロセスのスレッドが実行されると、メモリマネージャーがロックダウンされていて、元のスレッドのバッファーを含む対応する物理ページが保持されていない限り、要求元のスレッドのバッファーのシステム物理メモリを上書きできます。

ただし、メモリマネージャーによってバッファーの物理ページが保持されている場合でも、他のスレッドが最新の状態であっても、そのバッファーの元のスレッドの仮想アドレスは表示されたままになりません。 そのため、ドライバーは、 [**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)から返された仮想アドレスを使用してメモリにアクセスすることはできません。 このルーチンの呼び出し元は、パケットベースのシステムまたはバスマスタ DMA を使用してデータを転送するために、結果を[**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer) (IRP の**mdladdress**ポインターと共に) に渡す必要があります。

 

 




