---
title: Windows カーネル モードの DMA ライブラリ
description: Windows カーネル モードの DMA ライブラリ
ms.assetid: db6cc33a-474b-44a2-bd55-769ff31abae7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4679032d823e128628071ace53f635c877c3fe1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556796"
---
# <a name="windows-kernel-mode-dma-library"></a>Windows カーネル モードの DMA ライブラリ


パフォーマンスを向上させるため、デバイスが中央処理装置 (CPU) をバイパスする方法でメモリに直接アクセスする必要があります。 このテクノロジは、ダイレクト メモリ アクセス (DMA) と呼ばれます。 Windows では、デバイス ドライバー開発者向けの DMA ライブラリを提供します。

ドライバーの DMA の詳細については、次を参照してください。 [DMA](https://msdn.microsoft.com/library/windows/hardware/ff544058)します。

DMA ルーチンの一覧については、次を参照してください。[ダイレクト メモリ アクセス (DMA) ライブラリ ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff544068)します。

DMA をデバイスとメモリの間で直接通信するためのテクノロジと同じではありませんを[デバイス メモリ アクセス](https://msdn.microsoft.com/library/windows/hardware/ff543138)、読み取りと書き込みの I/O ポートと CPU レジスタに用意されているマクロのセットです。

 

 




