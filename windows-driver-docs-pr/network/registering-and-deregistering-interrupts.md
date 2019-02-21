---
title: 登録および登録解除を中断します。
description: 登録および登録解除を中断します。
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
ms.openlocfilehash: 93fd829d70a7e9bf1699319262f6f94141ee8412
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532018"
---
# <a name="registering-and-deregistering-interrupts"></a>登録および登録解除を中断します。





ミニポート ドライバーは呼び出し[ **NdisMRegisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563649)割り込みを登録します。 ドライバーは、初期化、 [ **NDIS\_ミニポート\_割り込み\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566465)割り込み特性を指定する構造体と関数のエントリ ポイント。 ドライバーは、構造体を渡します**NdisMRegisterInterruptEx**します。

ドライバーの呼び出し、 [ **NdisMDeRegisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563575)関数で以前に割り当てられたリソースを解放する**NdisMRegisterInterruptEx**します。

 

 





