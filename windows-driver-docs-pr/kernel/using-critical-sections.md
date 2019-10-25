---
title: クリティカル セクションの使用
description: クリティカル セクションの使用
ms.assetid: 439ba7ef-6473-40ca-9daa-a8c61d789d97
keywords:
- 割り込みサービスルーチン WDK カーネル、クリティカルセクション
- Isr WDK カーネル、クリティカルセクション
- InterruptService
- 同期 WDK カーネル、割り込み
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 948a83f986373952c698efce0c88dbdadd5cb070
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835995"
---
# <a name="using-critical-sections"></a>クリティカル セクションの使用





[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンが含まれているドライバーでは、多くの場合、ISR とその他のルーチン間でハードウェアリソースまたはドライバーデータへのアクセスを同期するために、1つまたは複数の重要なセクションが必要になります。

ここでは、次のトピックについて説明します。

[SynchCritSection ルーチンの概要](introduction-to-synchcritsection-routines.md)

[SynchCritSection ルーチンの記述](writing-synchcritsection-routines.md)

 

 




