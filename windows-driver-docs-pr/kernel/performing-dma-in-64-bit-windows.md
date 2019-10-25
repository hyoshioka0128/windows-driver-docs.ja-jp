---
title: 64 ビットの Windows での DMA の実行
description: 64 ビットの Windows での DMA の実行
ms.assetid: 3ef00c05-356d-488a-8422-503d8132344d
keywords:
- 64-bit WDK カーネル、移植 (ドライバーを)
- 64ビット版 Windows へのドライバーの移植
- DMA 転送 WDK カーネル、64ビット Windows
- WDK 64 ビットのダブルバッファリング
- ダイレクトメモリアクセス WDK カーネル
- ポリモーフィズム (WDK 64 ビット)
- データ構造 WDK 64 ビット
- 署名されていない操作 WDK 64 ビット
- 署名された操作 (WDK 64 ビット)
- ポインター演算 WDK 64 ビット
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f9799487705dce1f7ac1d0354179197bcdf5499
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827712"
---
# <a name="performing-dma-in-64-bit-windows"></a>64 ビットの Windows での DMA の実行





64ビットのアドレス指定サポートをドライバーに追加すると、システム全体のパフォーマンスを大幅に向上させることができます。 これは、ダイレクトメモリアクセス (DMA) を実行するデバイスドライバーに特に重要です。 64ビットの Microsoft Windows では、DMA を実行するが64ビットのアドレス指定をサポートしないデバイスドライバーはダブルバッファーされるため、パフォーマンスが低下します。

通常、ダブルバッファリングは 8 GB システムでは比較的小さな影響 (単一の割合のポイント) を持ちますが、これはデータベースの利用状況など、i/o 集中型のタスクに影響を与えるのに十分です。 物理メモリの量が増えるにつれて、このようなパフォーマンスへの悪影響も大きくなります。

64ビット DMA をサポートするために、ドライバーは次のガイドラインに従う必要があります。

1.  物理アドレスの計算には、**物理\_アドレス**構造を使用します。

2.  64ビットアドレス全体を有効な物理アドレスとして扱います。 たとえば、ドライバーは、ロックされたバッファーで[**MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmgetphysicaladdress)を呼び出さずに、上位32ビットを破棄し、切り捨てられたアドレスを32ビットコンポーネントアダプターに渡す必要があります。 その結果、メモリが破損し、i/o が失われ、システム障害が発生します。

3.  Windows 2000 で追加された高パフォーマンスのスキャッター/ギャザールーチン ([**GetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list)および[**PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list)) を使用します。

4.  [**Mm64BitPhysicalAddress**](mm64bitphysicaladdress.md)グローバルシステム変数の値を確認します。 **TRUE**の場合、システムは64ビットの物理アドレス指定をサポートします。

5.  [**デバイス\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description)構造体の**Dma64BitAddresses**メンバーを**TRUE**に設定して、ドライバーが64ビットの DMA アドレスをサポートしていることを示します。

32ビット Windows の DMA ルーチンは、64ビット対応です。 デバイスドライバーでこれらのルーチンが正しく使用されている場合、DMA コードは64ビットの Windows で変更を加えることなく動作します。

 

 




