---
title: 64 ビット Windows で DMA を実行します。
description: 64 ビット Windows で DMA を実行します。
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
ms.openlocfilehash: ce93b2f995c56f39514948f59845234c9aee7f97
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558130"
---
# <a name="performing-dma-in-64-bit-windows"></a>64 ビット Windows で DMA を実行します。





64 ビット アドレス指定のサポートには、ドライバーを追加すると、システム全体のパフォーマンスを大幅に向上させることができます。 これは、ダイレクト メモリ アクセス (DMA) を実行するデバイス ドライバーの特に重要です。 Microsoft Windows の 64 ビット、DMA を実行するが、64 ビットのアドレス指定をサポートしているデバイス ドライバーのダブル バッファリングされた相対的なパフォーマンスが低下する結果します。

ダブル バッファリングは、通常は、8 GB のシステムに比較的小さな影響 (1 つのパーセント ポイント) をデータベースの利用状況など、O 消費するタスクに影響するのに十分なは。 物理メモリの増加量として負の値のパフォーマンスに及ぼす影響はも増加します。

64 ビットの DMA をサポートするために、ドライバーは、次のガイドラインを確認する必要があります。

1.  使用**物理\_アドレス**構造体が物理アドレスを計算します。

2.  全体の 64 ビットのアドレスは、有効な物理アドレスとして扱います。 たとえば、ドライバーは呼び出す必要がありますいない[ **MmGetPhysicalAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554547)ロックされているバッファーでは、上位の 32 ビットを破棄し、32 ビット コンポーネントをアダプターに切り捨てられたアドレスを渡します。 これにより、破損したメモリ、ロスト I/O、およびシステム障害が発生します。

3.  高パフォーマンスのスキャッター/ギャザー ルーチンを使用して ([**GetScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff546531)と[ **PutScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff559967)) で追加されました。Windows 2000 です。

4.  値を確認、 [ **Mm64BitPhysicalAddress** ](mm64bitphysicaladdress.md)システムのグローバル変数。 場合は**TRUE**システムが 64 ビットの物理アドレス指定をサポートします。

5.  設定、 **Dma64BitAddresses**のメンバー、 [**デバイス\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff543107)構造体を**TRUE**ことを示すために、ドライバーは、64 ビット DMA のアドレスをサポートします。

32 ビット Windows で DMA ルーチンでは、64 ビットの仕様があります。 デバイス ドライバーでは、これらのルーチンを正しく使用されている場合、DMA コードは 64 ビット Windows で変更しなくても動作します。

 

 




