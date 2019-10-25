---
title: PCMCIA_INTERFACE_STANDARD インターフェイスの機能
description: PCMCIA_INTERFACE_STANDARD インターフェイスの機能
ms.assetid: 301b4165-4753-4d55-9760-17628174c043
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a117be23c9f5122f713a3c992a5f75f21afaded
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837729"
---
# <a name="functionality-of-the-pcmcia_interface_standard-interface"></a>PCMCIA\_インターフェイス\_標準インターフェイスの機能





このセクションでは、Windows 2000 以降のオペレーティングシステムで PCMCIA バスドライバーがサポートする PCMCIA\_インターフェイス\_標準インターフェイスの機能について説明します。 PCMCIA\_INTERFACE\_STANDARD インターフェイスには、PCMCIA ドライバーによって直接呼び出すことができる一連のルーチンが用意されています。 これらのインターフェイスルーチンは、次の操作をサポートします。

-   PCMCIA バスドライバーによってマップされている [メモリ] ウィンドウの属性を変更する

-   デバイスの*Vpp* (2 次電源) レベルを設定する

-   カードメモリが書き込み禁止になっているかどうかを判断する

PCMCIA\_INTERFACE\_STANDARD インターフェイスによって提供されるルーチンの詳細については、「 [pcmcia\_interface\_Standard Interface Memory Card ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

 





