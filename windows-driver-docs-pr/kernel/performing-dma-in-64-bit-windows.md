---
title: 64 ビットの Windows での DMA の実行
description: 64 ビットの Windows での DMA の実行
ms.assetid: 3ef00c05-356d-488a-8422-503d8132344d
keywords:
- 64 ビットの WDK カーネル、ドライバーの移植
- 64 ビット Windows に移植ドライバー
- DMA 転送 WDK カーネル、64 ビット Windows
- WDK の 64 ビットのダブル バッファリング
- ダイレクト メモリ アクセスの WDK カーネル
- ポリモーフィズム WDK 64 ビット
- データ構造の WDK 64 ビット
- WDK の 64 ビット符号なしの操作
- WDK の 64 ビット符号付きの操作
- ポインター演算 WDK 64 ビット
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cfd18a1efdfbc9c7d5853d515eff78ae4a98d51
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384739"
---
# <a name="performing-dma-in-64-bit-windows"></a>64 ビットの Windows での DMA の実行





64 ビット アドレス指定のサポートには、ドライバーを追加すると、システム全体のパフォーマンスを大幅に向上させることができます。 これは、ダイレクト メモリ アクセス (DMA) を実行するデバイス ドライバーの特に重要です。 Microsoft Windows の 64 ビット、DMA を実行するが、64 ビットのアドレス指定をサポートしているデバイス ドライバーのダブル バッファリングされた相対的なパフォーマンスが低下する結果します。

ダブル バッファリングは、通常は、8 GB のシステムに比較的小さな影響 (1 つのパーセント ポイント) をデータベースの利用状況など、O 消費するタスクに影響するのに十分なは。 物理メモリの増加量として負の値のパフォーマンスに及ぼす影響はも増加します。

64 ビットの DMA をサポートするために、ドライバーは、次のガイドラインを確認する必要があります。

1.  使用**物理\_アドレス**構造体が物理アドレスを計算します。

2.  全体の 64 ビットのアドレスは、有効な物理アドレスとして扱います。 たとえば、ドライバーは呼び出す必要がありますいない[ **MmGetPhysicalAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmgetphysicaladdress)ロックされているバッファーでは、上位の 32 ビットを破棄し、32 ビット コンポーネントをアダプターに切り捨てられたアドレスを渡します。 これにより、破損したメモリ、ロスト I/O、およびシステム障害が発生します。

3.  高パフォーマンスのスキャッター/ギャザー ルーチンを使用して ([**GetScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pget_scatter_gather_list)と[ **PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pput_scatter_gather_list)) で追加されました。Windows 2000 です。

4.  値を確認、 [ **Mm64BitPhysicalAddress** ](mm64bitphysicaladdress.md)システムのグローバル変数。 場合は**TRUE**システムが 64 ビットの物理アドレス指定をサポートします。

5.  設定、 **Dma64BitAddresses**のメンバー、 [**デバイス\_説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_description)構造体を**TRUE**ことを示すために、ドライバーは、64 ビット DMA のアドレスをサポートします。

32 ビット Windows で DMA ルーチンでは、64 ビットの仕様があります。 デバイス ドライバーでは、これらのルーチンを正しく使用されている場合、DMA コードは 64 ビット Windows で変更しなくても動作します。

 

 




