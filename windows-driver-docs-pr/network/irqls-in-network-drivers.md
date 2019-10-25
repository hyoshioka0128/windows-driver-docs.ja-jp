---
title: ネットワーク ドライバーの IRQL
description: ネットワーク ドライバーの IRQL
ms.assetid: d8720084-460e-4b62-90de-abfd96cd6364
keywords:
- ネットワークドライバー WDK、IRQLs
- IRQLs WDK ネットワーク
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: fb7042b4f1f60b50f014ece6d4ba295d1dc239ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844157"
---
# <a name="irqls-in-network-drivers"></a>ネットワーク ドライバーの IRQL

NDIS によって呼び出されるすべてのドライバー関数は、システムによって決定される IRQL (パッシブ\_レベル &lt; ディスパッチ\_レベル &lt; DIRQL) のいずれかで実行されます。 たとえば、ミニポートドライバーの[初期化](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数、 [halt](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数、 [reset](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数、および[SHUTDOWN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)関数は、一般的にはパッシブ\_レベルで実行されますが、reset 関数と shutdown 関数は上位で呼び出すことができます。システムで必要な場合は IRQL。 割り込みコードは DIRQL で実行されるため、NDIS 中間またはプロトコルドライバーが DIRQL で実行されることはありません。 他のすべての NDIS ドライバー関数は、IRQL = ディスパッチ\_レベル以下で実行します。

ドライバー関数が実行される IRQL は、そのドライバーが呼び出すことができる NDIS 関数に影響します。 特定の関数は、IRQL = パッシブ\_レベルでのみ呼び出すことができます。 他のユーザーはディスパッチ\_レベル以下で呼び出すことができます。 すべての NDIS 関数で IRQL の制限を確認する必要があります。

ドライバーの interrupt service ルーチン (ISR) とリソースを共有するドライバー関数は、競合状態を防ぐために、DIRQL に対して IRQL を上げることができる必要があります。 NDIS にはこのようなメカニズムが用意されています。