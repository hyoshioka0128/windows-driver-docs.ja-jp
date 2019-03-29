---
title: ハードウェア割り込みの処理
description: WDF ドライバーでのサービスのハードウェア割り込みを割り込みオブジェクトの作成方法と、ドライバーが割り込みデータ バッファーへのアクセスを同期する方法について説明します。
ms.assetid: 08460510-6e5f-4c02-8086-9caa9b4b4c2d
keywords:
- ハードウェアの割り込み WDK KMDF
- WDK KMDF を中断します。
- フレームワーク ベースのドライバー WDK KMDF、ハードウェアの割り込み
- カーネル モード ドライバー WDK KMDF、ハードウェアの割り込み
- KMDF WDK、ハードウェアの割り込み
- カーネル モード ドライバー フレームワーク WDK、ハードウェアの割り込み
- framework オブジェクト WDK KMDF、割り込みオブジェクト
- 割り込みオブジェクト WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fff84de5b481d95c621001b1bb695340a51b9f7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580789"
---
# <a name="handling-hardware-interrupts"></a>ハードウェア割り込みの処理


このセクションのトピックでは、Windows Driver Frameworks (WDF) ドライバーでのサービスのハードウェア割り込みを framework 割り込みオブジェクトの作成方法と、ドライバーが割り込みデータ バッファーへのアクセスを同期する方法について説明します。




## <a name="in-this-section"></a>このセクションの内容


-   [割り込みオブジェクトを作成します。](creating-an-interrupt-object.md)
-   [有効にして、割り込みを無効化](enabling-and-disabling-interrupts.md)
-   [割り込みを処理します。](servicing-an-interrupt.md)
-   [割り込みのコードを同期します。](synchronizing-interrupt-code.md)
-   [割り込みパッシブ レベルをサポートしています。](supporting-passive-level-interrupts.md)
-   [割り込みを使用して、デバイスのスリープを解除するには](using-an-interrupt-to-wake-a-device.md)
-   [アクティブな両方の割り込みを処理](handling-active-both-interrupts.md)

 

 





