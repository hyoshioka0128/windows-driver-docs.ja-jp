---
title: クリティカル セクションの使用
description: クリティカル セクションの使用
ms.assetid: 439ba7ef-6473-40ca-9daa-a8c61d789d97
keywords:
- 割り込みサービス ルーチン WDK カーネル、クリティカル セクション
- Isr WDK カーネルでは、クリティカル セクション
- InterruptService
- 同期の WDK カーネル、割り込み
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02a7ab16c71ba6acc0625d42e128d7017278dcca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381672"
---
# <a name="using-critical-sections"></a>クリティカル セクションの使用





任意のドライバーを含む、 [ *InterruptService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)ルーチンでは 1 つ必要はほとんどの場合または同期するより重要なセクションにハードウェア リソースまたはドライバーに ISR ルーチンとその他のルーチンの間でデータ アクセス.

ここでは、次のトピックについて説明します。

[SynchCritSection ルーチンの概要](introduction-to-synchcritsection-routines.md)

[書き込み SynchCritSection ルーチン](writing-synchcritsection-routines.md)

 

 




