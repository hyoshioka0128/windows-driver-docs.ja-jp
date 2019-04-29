---
title: ネットワーク ドライバーの IRQL
description: ネットワーク ドライバーの IRQL
ms.assetid: d8720084-460e-4b62-90de-abfd96cd6364
keywords:
- ネットワーク ドライバー WDK、Irql
- Irql WDK ネットワーク
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e417d5d605c9de6d97b5bce77120ec8eb550ae9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327676"
---
# <a name="irqls-in-network-drivers"></a>ネットワーク ドライバーの IRQL

システムにより決定された IRQL で NDIS によって呼び出されるすべてのドライバー関数が実行される (パッシブのいずれかの\_レベル&lt;ディスパッチ\_レベル&lt;DIRQL)。 たとえば、ミニポート ドライバーの[初期化](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数、[停止](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数、[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)関数、および[シャット ダウン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)関数頻繁に実行するのには、パッシブ\_レベルには、システムで必要な場合より高い IRQL でリセットとシャット ダウン関数を呼び出すことができます。 NDIS intermediate またはプロトコル ドライバー DIRQL で実行されないように DIRQL、コード実行を中断します。 その他のすべての NDIS ドライバー関数実行の IRQL 以下でディスパッチを =\_レベル。

ドライバー関数が実行される IRQL では、どの NDIS 関数を呼び出すことができますに影響します。 特定の関数は IRQL でのみ呼び出すことができます = パッシブ\_レベル。 他のユーザーは、ディスパッチで呼び出すことができます\_レベルまたは低くします。 IRQL の制限については、各 NDIS 関数を確認する必要があります。

ドライバーの割り込みサービス ルーチン (ISR) とリソースを共有するすべてのドライバー関数は、DIRQL 競合状態を回避するには、その IRQL を生成できる必要があります。 NDIS は、このようなメカニズムを提供します。