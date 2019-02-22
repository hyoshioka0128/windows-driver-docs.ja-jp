---
title: 非 PnP ドライバーのアンロード ルーチン
description: 非 PnP ドライバーのアンロード ルーチン
ms.assetid: 5917648f-1e7e-4b39-9aa6-d6cdaac7a2cd
keywords:
- ルーチン WDK カーネルでは、非 PnP ドライバーをアンロードします。
- WDK カーネルの日常的な非 PnP アンロード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6902f2954c18ee15da35ddd6f392714ff7a03507
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557727"
---
# <a name="non-pnp-drivers-unload-routine"></a>非 PnP ドライバーのアンロード ルーチン





以前のドライバーと高度なファイル システム ドライバー、PnP デバイス削除要求を処理しない必要がありますリソースを解放、デバイス オブジェクトを削除およびデバイス スタックからデタッチ、 [*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチン。

これが行われていない場合、レガシ デバイス ドライバーがで行う必要がありますまずその*アンロード*ルーチンは、デバイスからの割り込みを無効にします。 それ以外の場合、その ISR を中にデバイスの割り込みを処理するために呼び出される可能性が、*アンロード*ルーチンが ISR が割り込みを処理する必要があるデバイスの拡張機能内のリソースを解放します。 このような場合は、その ISR が正常に実行される場合でも、 [ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)または[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチンを ISR キュー、およびIRQL で実行されるその他のドライバー ルーチン可能性があります&gt;= ディスパッチ\_レベルが実行する前に、*アンロード*ルーチンが発生する可能性が高くなりますコントロールを再度獲得を*アンロード*ルーチンが他のドライバー ルーチンを参照するリソースを削除します。 参照してください[を管理するハードウェアの優先順位](managing-hardware-priorities.md)詳細についてはします。

ファイル システムとレガシ ドライバーには、割り込みを無効にした後、リソースとオブジェクトを解放する必要があります。 詳細については、次の 2 つのセクションを参照してください。

[ドライバーによって割り当てられたリソースを解放します。](releasing-driver-allocated-resources.md)

[デバイスとコント ローラーのオブジェクトを解放します。](releasing-device-and-controller-objects.md)

 

 




