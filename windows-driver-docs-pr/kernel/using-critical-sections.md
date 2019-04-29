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
ms.openlocfilehash: f7c92791abf47c6b267f6a5f2e2f5719c50d77aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387411"
---
# <a name="using-critical-sections"></a>クリティカル セクションの使用





任意のドライバーを含む、 [ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)ルーチンでは 1 つ必要はほとんどの場合または同期するより重要なセクションにハードウェア リソースまたはドライバーに ISR ルーチンとその他のルーチンの間でデータ アクセス.

ここでは、次のトピックについて説明します。

[SynchCritSection ルーチンの概要](introduction-to-synchcritsection-routines.md)

[書き込み SynchCritSection ルーチン](writing-synchcritsection-routines.md)

 

 




