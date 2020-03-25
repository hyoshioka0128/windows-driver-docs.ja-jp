---
title: IRP と高速 I/O のフィルタリング
description: IRP と高速 I/O のフィルタリング
ms.assetid: fad124b0-525d-4ff9-8f2c-3817fc76685c
keywords:
- フィルタードライバー WDK ファイルシステム、IRP フィルター
- ファイルシステムフィルタードライバー WDK、IRP フィルタリング
- Irp WDK ファイルシステム
- Irp WDK ファイルシステムのフィルター処理
- 高速 i/o WDK ファイルシステムのフィルター処理
- 簡易 i/o フィルタリング (WDK ファイルシステム)
- I/o WDK ファイルシステム
- ディスパッチルーチン WDK ファイルシステム
- I/o 要求 (WDK ファイルシステム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7fb38239f20d5bfe66ea14b71d6aadbfd8dbe00
ms.sourcegitcommit: 677a9aeb3fb0c29fd8984f271fd803f15182fdb2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80226521"
---
# <a name="filtering-irps-and-fast-io"></a>IRP と高速 I/O のフィルタリング

> [!NOTE]
> 最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、フィルターマネージャーをサポートする[ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)を使用します。 レガシドライバーをミニフィルタードライバーに移植する方法については、「[レガシフィルタードライバーを移植するためのガイドライン](guidelines-for-porting-legacy-filter-drivers.md)」を参照してください。

ファイルシステムフィルタードライバーは、1つまたは複数のファイルシステムまたはファイルシステムボリュームの i/o 要求をフィルター処理します。 各 i/o 要求は、i/o 要求パケット (IRP) または高速 i/o 要求として表示されます。 Irp は、ドライバーの IRP ディスパッチルーチンによって処理される i/o システム構造です。 高速 i/o 要求は、ドライバーの高速 i/o コールバックルーチンによって処理されます。

フィルタードライバーが初期化されると、その**Driverentry**ルーチンによって、フィルタードライバーの IRP ディスパッチルーチンと高速 i/o コールバックルーチンが登録されます。 これらのルーチンのセットは、フィルタードライバーごとに1つだけ登録できます。

一部の種類の Irp は、高速 i/o に相当します。また、一部の高速 i/o 要求には、対応する IRP があります。 しかし、Irp は、高速 i/o ではできないさまざまな種類の i/o を処理します。 また、特定の特化した高速 i/o ルーチンを使用して、IRP を作成せずに、キャッシュマネージャーまたはメモリマネージャーのファイルシステムリソースを事前に取得します。 そのため、ほとんどの場合、Irp と高速 i/o 要求は i/o 操作で個別のロールを実行します。

このセクションでは、次のトピックについて説明します。

[Irp は、高速 i/o とは異なります。](irps-are-different-from-fast-i-o.md)

[ファイルシステムフィルタードライバーデバイスオブジェクトの種類](types-of-device-objects-used-by-file-system-filter-drivers.md)
