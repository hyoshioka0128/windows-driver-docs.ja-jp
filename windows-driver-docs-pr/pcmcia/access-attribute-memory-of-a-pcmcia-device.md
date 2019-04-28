---
title: PCMCIA デバイスの属性メモリにアクセスする
description: PCMCIA デバイスの属性メモリにアクセスする
ms.assetid: 270b8821-6322-4694-83eb-de319197dd6a
keywords:
- PCMCIA WDK バス、属性のメモリ
- 属性のメモリ バスの WDK PCMCIA
- 属性のメモリ属性メモリについての WDK PCMCIA バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b083c2ef3c163e78b74e1e83705a4ec2d43c6d65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362474"
---
# <a name="access-attribute-memory-of-a-pcmcia-device"></a>PCMCIA デバイスの属性メモリにアクセスする





このセクションでは、Microsoft Windows 2000 以降のオペレーティング システムで PCMCIA デバイス用のドライバーが PCMCIA デバイスの属性のメモリにアクセスする方法について説明します。

-   [PCMCIA デバイスの属性のメモリにアクセスするための要件](https://msdn.microsoft.com/library/windows/hardware/ff537665)

-   [プラグ アンド プレイの I/O 要求を使用してアクセス PCMCIA 属性メモリ](https://msdn.microsoft.com/library/windows/hardware/ff536898)

    これは単純なメソッドですが、ほとんどの目的のための十分な IRQL でのみ実行できます&lt;ディスパッチ\_レベル。

-   [PCMCIA 属性のメモリ バスを使用してへのアクセス\_インターフェイス\_標準インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff536894)

    このメソッドは、I/O 要求のオーバーヘッドを排除し、IRQL で実行できる&lt;= ディスパッチ\_レベル

-   [永続的なメモリ ウィンドウからアクセス PCMCIA 属性メモリ](https://msdn.microsoft.com/library/windows/hardware/ff536901)

    ドライバーの ISR は、このメソッドを使用して、IRQL DIRQL で実行中にメモリに直接アクセスできます。

-   [PCMCIA 属性のメモリを PCMCIA を使用してアクセス\_インターフェイス\_標準インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff536897)

    メモリ カードのドライバーは、このメソッドを使用して、IRQL で&lt;= ディスパッチ\_レベル。

これらのメソッドでサポートされる*pcmcia.sys*を PCMCIA のシステム ドライバーが Windows 2000 以降のオペレーティング システムでバスします。

 

 





