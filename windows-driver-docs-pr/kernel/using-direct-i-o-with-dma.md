---
title: DMA でのダイレクト I/O の使用
description: DMA でのダイレクト I/O の使用
ms.assetid: 0e609613-9023-4f35-a9c5-d68c8b676cfe
keywords:
- ダイレクト I/O WDK カーネル
- WDK の I/O バッファーのダイレクト I/O
- データ バッファーの WDK I/O、ダイレクト I/O
- I/O WDK カーネルでは、ダイレクト I/O
- DMA 転送 WDK カーネル、ダイレクト I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c056950901a2ee049eedc7e59a0a1c8993c54666
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580183"
---
# <a name="using-direct-io-with-dma"></a>DMA でのダイレクト I/O の使用





次の図は、I/O マネージャーの設定方法を示しています、 [ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794) DMA の転送操作の要求がダイレクト I/O を使用しています。

![ユーザー バッファー dma を使用するデバイスでダイレクト i/o を示す図](images/3mdldrct.png)

前の図は、ドライバーが IRP を使用する方法を示します**MdlAddress**読み取り要求のデータを転送します。 図にドライバーがパケットに基づくシステムまたはバス マスターの DMA を使用し、デバイス オブジェクトの論理和が**フラグ**か\_直接\_IO。

1.  ユーザー スペースの仮想アドレスのいくつかの範囲は、現在のスレッドのバッファーを表し、そのバッファーの内容は、いくつかの物理的に隣接していないページ (前の図では濃い網掛け) を実際に格納される可能性が。 I/O マネージャーは、このバッファーを記述する MDL を作成します。 MDL は、特定の仮想アドレスの範囲を 1 つまたは複数のページ ベースの物理アドレスの範囲にマップされる、メモリ マネージャーによって定義されている、非透過データ構造です。 詳細については、次を参照してください。[を使用して MDLs](using-mdls.md)します。

2.  I/O マネージャー サービスの現在のスレッドの読み取り要求、対象のスレッドに渡しますユーザー領域の範囲のバッファーを表す仮想アドレス。

3.  I/O マネージャーまたはファイル システム ドライバー (FSD) は、ユーザーが指定したバッファーのアクセシビリティと呼び出しを確認します。 [ **MmProbeAndLockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554664) MDL を以前に作成したとします。 **MmProbeAndLockPages** MDL で対応する物理アドレスの範囲を入力します。

    前の図に示すよう仮想アドレスの範囲の MDL がいくつかの対応するページ ベースの物理アドレス エントリがあることができ、バッファーの仮想アドレスの範囲が開始して、終了、MDL で説明されている最初と最後のページの先頭からのオフセットのバイト可能性があります。

4.  I/O マネージャー MDL へのポインターを提供します (**MdlAddress**) 転送操作を要求する IRP の。 I/O マネージャーまたはファイル システムの呼び出しまで[ **MmUnlockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556381) MDL で説明されている物理ページ ドライバーには、IRP が完了すると、ロックダウンされ、バッファーに割り当てられたままにします。 ただし、このような MDL の仮想アドレスになり、非表示 (無効) も IRP の前に、デバイス ドライバーまたは送信するデバイス ドライバーの上に配置が任意の中間ドライバー。

5.  ドライバーは、パケットに基づくシステムまたはバス マスターの DMA を使用する場合、 [ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチンの呼び出し[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)でIRP の**MdlAddress** MDL のページ ベースのエントリの基本の仮想アドレスを取得へのポインター。

6.  *AdapterControl*ルーチンを呼び出して[ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)によって返されるベース アドレスで**MmGetMdlVirtualAddress**」を読んで、物理メモリに直接デバイスからのデータ。 (詳細については、次を参照してください[アダプター オブジェクトと DMA](adapter-objects-and-dma.md)。)。

ドライバーでは、バッファー長を常に確認する必要があります。 I/O マネージャーに長さ 0 のバッファーの MDL 作成されないことに注意してください。

 

 




