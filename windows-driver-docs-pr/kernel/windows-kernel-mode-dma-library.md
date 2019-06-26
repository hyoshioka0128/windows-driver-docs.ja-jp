---
title: Windows カーネルモード DMA ライブラリ
description: Windows カーネルモード DMA ライブラリ
ms.assetid: db6cc33a-474b-44a2-bd55-769ff31abae7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d0cb3fe82b615a0a10827021ac80e6929173bf90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358051"
---
# <a name="windows-kernel-mode-dma-library"></a>Windows カーネルモード DMA ライブラリ


パフォーマンスを向上させるため、デバイスが中央処理装置 (CPU) をバイパスする方法でメモリに直接アクセスする必要があります。 このテクノロジは、ダイレクト メモリ アクセス (DMA) と呼ばれます。 Windows では、デバイス ドライバー開発者向けの DMA ライブラリを提供します。

ドライバーの DMA の詳細については、次を参照してください。 [DMA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

DMA ルーチンの一覧については、次を参照してください。[ダイレクト メモリ アクセス (DMA) ライブラリ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

DMA をデバイスとメモリの間で直接通信するためのテクノロジと同じではありませんを[デバイス メモリ アクセス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)、読み取りと書き込みの I/O ポートと CPU レジスタに用意されているマクロのセットです。

 

 




