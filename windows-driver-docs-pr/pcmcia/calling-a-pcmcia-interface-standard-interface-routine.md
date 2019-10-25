---
title: PCMCIA_INTERFACE_STANDARD インターフェイスのルーチンを呼び出す
description: PCMCIA_INTERFACE_STANDARD インターフェイスのルーチンを呼び出す
ms.assetid: 468d2037-a7d5-4851-9f41-d1e6c9006750
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a1c5d4f8a58b65c555fc8ea7bd2310badc506f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837731"
---
# <a name="calling-a-pcmcia_interface_standard-interface-routine"></a>標準インターフェイスルーチン\_PCMCIA\_インターフェイスを呼び出す





このセクションでは、標準インターフェイスルーチン\_PCMCIA\_インターフェイスを呼び出す方法について説明します。

ドライバーが pcmcia\_インターフェイスを取得した後、pcmcia バスドライバーから[\_インターフェイスメモリカードルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)の構造を取得した後、ドライバーはインターフェイスルーチンを呼び出すことができます。

各インターフェイスルーチンにはコンテキストポインターが必要です。 ドライバーでは、pcmcia バスドライバーによって返される**コンテキスト**メンバーの値を使用する必要があります\_インターフェイス\_標準の構造です。 コンテキストポインターが有効でない場合は、システムの動作が定義されていないため、システムが停止する可能性があります。

PCMCIA\_インターフェイス\_標準インターフェイスルーチンは、IRQL &lt;= ディスパッチ\_レベルで呼び出すことができます。 システム全体のパフォーマンスを維持するには、ドライバーが IRQL でこれらのルーチンを呼び出し、\_レベルをディスパッチ &lt; ことを強くお勧めします。 IRQL ディスパッチ\_レベルでインターフェイスルーチンを呼び出すと、呼び出し元が長時間にわたってシステム操作をブロックする可能性があります。

 

 





