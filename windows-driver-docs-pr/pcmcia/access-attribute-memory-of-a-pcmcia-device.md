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
ms.openlocfilehash: ca963b57979593242ee623ecbfd4e91f701875b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353535"
---
# <a name="access-attribute-memory-of-a-pcmcia-device"></a>PCMCIA デバイスの属性メモリにアクセスする





このセクションでは、Microsoft Windows 2000 以降のオペレーティング システムで PCMCIA デバイス用のドライバーが PCMCIA デバイスの属性のメモリにアクセスする方法について説明します。

-   [PCMCIA デバイスの属性のメモリにアクセスするための要件](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/requirements-for-accessing-attribute-memory-of-a-pcmcia-device)

-   [プラグ アンド プレイの I/O 要求を使用してアクセス PCMCIA 属性メモリ](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-pcmcia-attribute-memory-by-using-a-plug-and-play-i-o-request)

    これは単純なメソッドですが、ほとんどの目的のための十分な IRQL でのみ実行できます&lt;ディスパッチ\_レベル。

-   [PCMCIA 属性のメモリ バスを使用してへのアクセス\_インターフェイス\_標準インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-pcmcia-attribute-memory-by-using-a-bus-interface-standard-inter)

    このメソッドは、I/O 要求のオーバーヘッドを排除し、IRQL で実行できる&lt;= ディスパッチ\_レベル

-   [永続的なメモリ ウィンドウからアクセス PCMCIA 属性メモリ](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-pcmcia-attribute-memory-through-a-permanent-memory-window)

    ドライバーの ISR は、このメソッドを使用して、IRQL DIRQL で実行中にメモリに直接アクセスできます。

-   [PCMCIA 属性のメモリを PCMCIA を使用してアクセス\_インターフェイス\_標準インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-pcmcia-attribute-memory-by-using-a-pcmcia-interface-standard-in)

    メモリ カードのドライバーは、このメソッドを使用して、IRQL で&lt;= ディスパッチ\_レベル。

これらのメソッドでサポートされる*pcmcia.sys*を PCMCIA のシステム ドライバーが Windows 2000 以降のオペレーティング システムでバスします。

 

 





