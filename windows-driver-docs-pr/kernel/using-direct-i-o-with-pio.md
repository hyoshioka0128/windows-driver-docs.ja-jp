---
title: ダイレクト I/O PIO の併用
description: ダイレクト I/O PIO の併用
ms.assetid: 84d36567-c8c6-4576-91a0-829c8819de4d
keywords:
- ダイレクト I/O WDK カーネル
- WDK の I/O バッファーのダイレクト I/O
- データ バッファーの WDK I/O、ダイレクト I/O
- I/O WDK カーネルでは、ダイレクト I/O
- PIO 転送操作の WDK カーネル
- 転送 WDK カーネルの I/O のプログラミング
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e3565137cd214292717595d8d32c5f932648b46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528659"
---
# <a name="using-direct-io-with-pio"></a>ダイレクト I/O PIO の併用





使用するドライバーは、DMA システム領域のアドレス範囲にユーザー スペースのバッファーにマップする必要があります二重ではなく、I/O (PIO) をプログラミングします。 次の図は、I/O マネージャーの設定方法を示しています、 [ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794) pio 転送の要求がダイレクト I/O を使用しています。

![pio を使用するデバイスのダイレクト i/o を示す図](images/3mdlpio.png)

図では、PIO を使用するデバイスが、同じタスクを処理する方法を示します。

1.  ユーザー スペースの仮想アドレスのいくつかの範囲は、現在のスレッドのバッファーを表し、そのバッファーの内容は、いくつかの物理的に隣接していないページで実際に格納される可能性が。 バッファーの長さが 0 以外の場合は、I/O マネージャーは、このバッファーを記述する MDL を作成します。

2.  I/O マネージャー サービスの現在のスレッドの読み取り要求、対象のスレッドに渡しますユーザー領域の範囲、バッファーを表す仮想アドレス。

3.  I/O マネージャーまたは FSD ユーザーが指定したバッファーのアクセシビリティを確認します。 呼び出す場合は、MDL I/O マネージャーが作成[ **MmProbeAndLockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554664) MDL とユーザー バッファーの仮想アドレスの範囲を指定します。 **MmProbeAndLockPages** MDL で対応する物理アドレスの範囲を入力します。

4.  I/O マネージャー MDL へのポインターを提供します (**MdlAddress**) 転送操作を要求する IRP の。 I/O マネージャーまたはファイル システムの呼び出しまで[ **MmUnlockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556381) MDL で説明されている物理ページ ドライバーには、IRP が完了すると、ロックダウンされ、バッファーに割り当てられたままにします。 ただし、このような MDL の仮想アドレスになり、非表示 (無効) も IRP の前に、デバイス ドライバーまたは送信するデバイス ドライバーの上に配置が任意の中間ドライバー。

5.  ドライバーは、システム (仮想) のアドレスを必要とする場合、ドライバーを呼び出す[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)の IRP で**MdlAddress**双方向のマップへのポインター、ユーザー スペースの仮想アドレス システム領域を MDL はアドレス範囲です。 上の図では、AliasBuff は二重にマップされているアドレスを記述する MDL を表します。

6.  ドライバーは、メモリにデータを読み込む二重にマップされた MDL (AliasBuff) からシステム領域仮想アドレスの範囲を使用します。

ドライバーが IRP を呼び出すことによって完了時[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)、ドライバーが呼び出された場合、I/O マネージャーまたはファイル システムが MDL のシステムの双方向のマップ領域の範囲を解放**MmGetSystemAddressForMdlSafe**します。 I/O マネージャーまたはファイル システム MDL、およびドライバーの代わりに、MDL と IRP の破棄で説明したページのロックを解除します。 パフォーマンスの向上のためのドライバーが、二重仮想アドレスを使用する必要がありますしない限り、手順 3. で説明されているようにシステムの領域へ MDL 物理アドレスのマッピングを避ける必要があります。 そうと、不必要にシステム ページ テーブル エントリを使用して、ドライバーのパフォーマンスとスケーラビリティの両方を減らすことができます。 さらに、システムがクラッシュするページ テーブル エントリ不足した場合、ほとんどの古いドライバーは、このような状況を処理できないためです。

現在のユーザー スレッドのバッファーとスレッド自体は、そのスレッドが現在いる間だけ物理メモリに常駐する保証されます。 スレッドが前の図に示すように、そのユーザー バッファーの内容でしたページアウトするセカンダリ ストレージに別のプロセスのスレッドが実行中にできます。 別のプロセスのスレッドを実行すると、メモリ マネージャーがロックされており、元のスレッドのバッファーを含む対応する物理ページを保持しない限り、この要求元のスレッドのバッファーのシステムの物理メモリを上書きできます。

ただし、そのバッファーの仮想アドレスを元のスレッドのままにしない表示メモリ マネージャーは、バッファーの物理的なページを保持する場合でも、別のスレッドは現在、します。 そのため、ドライバーがによって返される仮想アドレスを使用できません[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)メモリにアクセスします。 このルーチンの呼び出し元に結果を渡す必要があります[ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402) (の IRP と共に**MdlAddress**ポインター) をパケットに基づくシステムを使用してデータを転送するために、またはバス マスター DMA します。

 

 




