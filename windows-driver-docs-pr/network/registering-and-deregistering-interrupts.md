---
title: 割り込みの登録および登録解除
description: 割り込みの登録および登録解除
ms.assetid: 222782f3-092e-417d-ab1b-1988a593caa4
keywords:
- ネットワーク、登録に WDK を中断します。
- ネットワーク、登録解除に WDK を中断します。
- NdisMRegisterInterruptEx
- NdisMDeregisterInterruptEx
- 割り込みを登録します。
- 割り込みの登録を解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29b1d747ae387270af0d73aeee2f339b2a6ab31b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359173"
---
# <a name="registering-and-deregistering-interrupts"></a>割り込みの登録および登録解除





ミニポート ドライバーは呼び出し[ **NdisMRegisterInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterinterruptex)割り込みを登録します。 ドライバーは、初期化、 [ **NDIS\_ミニポート\_割り込み\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_interrupt_characteristics)割り込み特性を指定する構造体と関数のエントリ ポイント。 ドライバーは、構造体を渡します**NdisMRegisterInterruptEx**します。

ドライバーの呼び出し、 [ **NdisMDeRegisterInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterinterruptex)関数で以前に割り当てられたリソースを解放する**NdisMRegisterInterruptEx**します。

 

 





