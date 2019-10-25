---
title: Windows カーネルモード DMA ライブラリ
description: Windows カーネルモード DMA ライブラリ
ms.assetid: db6cc33a-474b-44a2-bd55-769ff31abae7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 280e06ea682e54e42982fbade9e3b502b7fae22d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835723"
---
# <a name="windows-kernel-mode-dma-library"></a>Windows カーネルモード DMA ライブラリ


パフォーマンスを向上させるために、デバイスは、中央処理装置 (CPU) をバイパスする方法でメモリに直接アクセスする必要がある場合があります。 このテクノロジはダイレクトメモリアクセス (DMA) と呼ばれます。 Windows には、デバイスドライバー開発者用の DMA ライブラリが用意されています。

ドライバーの DMA の詳細については、「 [dma](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

DMA ルーチンの一覧については、[ダイレクトメモリアクセス (dma) ライブラリルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に関する記述を参照してください。

DMA はデバイスとメモリの間で直接通信するためのテクノロジであり、デバイスの[メモリアクセス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)とは異なります。これは、i/o ポートと CPU レジスタに対して読み書きを行うために用意されている一連のマクロです。

 

 




