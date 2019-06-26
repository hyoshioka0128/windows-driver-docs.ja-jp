---
title: PCMCIA_INTERFACE_STANDARD インターフェイスのルーチンを呼び出す
description: PCMCIA_INTERFACE_STANDARD インターフェイスのルーチンを呼び出す
ms.assetid: 468d2037-a7d5-4851-9f41-d1e6c9006750
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7a2ddc569b82b7a6a206c7bd6168e0213eddfe6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386200"
---
# <a name="calling-a-pcmciainterfacestandard-interface-routine"></a>呼び出す、PCMCIA\_インターフェイス\_標準的なインターフェイスのルーチン





このセクションは、PCMCIA を呼び出す方法を説明します\_インターフェイス\_ルーチンの標準的なインターフェイスです。

ドライバーを取得した後、 [PCMCIA\_インターフェイス\_標準のインターフェイスのメモリ カード ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)PCMCIA バス ドライバー、ドライバーからの構造体がインターフェイスのルーチンを呼び出すことができます。

インターフェイスの各ルーチンでは、コンテキスト ポインターが必要です。 ドライバーを使用する必要があります、**コンテキスト**PCMCIA の PCMCIA バス ドライバーによって返されるメンバー値\_インターフェイス\_標準構造体。 コンテキスト ポインターが有効でない場合は、システムの動作が定義されていないと、システムが停止する可能性があります。

PCMCIA\_インターフェイス\_IRQL で標準的なインターフェイスのルーチンを呼び出すことができます&lt;= ディスパッチ\_レベル。 システム全体のパフォーマンスを維持するために強くお勧めのドライバーが IRQL でこれらのルーチンを呼び出す&lt;ディスパッチ\_レベル。 IRQL のディスパッチで、インターフェイスのルーチンを呼び出す\_レベルの時間が長くブロック システム操作を呼び出し元が発生することができます。

 

 





