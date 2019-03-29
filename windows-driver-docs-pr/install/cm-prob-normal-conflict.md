---
title: CM_PROB_NORMAL_CONFLICT
description: CM_PROB_NORMAL_CONFLICT
ms.assetid: 18c5ca02-0a4c-4a0e-8b33-5c685a73d4c8
keywords:
- CM_PROB_NORMAL_CONFLICT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46a8c7c5e4cb40f08e563d03d5570268c96da4a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570976"
---
# <a name="cmprobnormalconflict"></a>CM_PROB_NORMAL_CONFLICT

この関数は、システムの使用に予約されています。

2 つのデバイスは、同じの I/O ポート、同じの割り込みまたは同じ DMA チャネル (BIOS やオペレーティング システムでは、2 つの組み合わせでいずれか) に割り当てられています。

## <a name="error-code"></a>エラー コード

12

### <a name="display-message"></a>メッセージを表示します。

"このデバイスは、使用できる十分な空きリソースを見つけることができません。 (コード 12)

「このデバイスを使用する場合は、必要がありますこのシステムの他のデバイスのいずれかを無効にします。」

### <a name="recommended-resolution"></a>推奨される解決方法

[デバイス マネージャーを使用して](using-device-manager.md)と競合を解決する競合の原因を特定します。 デバイスの競合を解決する方法の詳細については、デバイス マネージャーを使用する方法に関するヘルプ情報を参照してください。

このエラー メッセージは、BIOS がデバイスに十分なリソースを割り当てられなかった場合にも表示できます。 たとえば、BIOS が、無効なマルチプロセッサ仕様 (MP) テーブルのため USB コント ローラーに割り込みを割り当てられません場合にこのメッセージが表示されます。
