---
title: 割り込みとの同期
description: 割り込みとの同期
ms.assetid: f201acfa-98e4-4373-ba63-b6c814810f99
keywords:
- WDK のネットワー キング、同期を中断します。
- NdisMSynchronizeWithInterruptEx
- 同期の WDK の割り込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 882679d108e07f7ba1e00a36ffc5e525a57e2921
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531774"
---
# <a name="synchronizing-with-interrupts"></a>割り込みとの同期





ミニポート ドライバーの場合、 [ *MiniportInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559395)関数と他の NIC の登録や状態変数などのリソースを共有する*MiniportXxx*で実行される関数をIRQL を削減する*MiniportXxx*関数を呼び出す必要があります[ **NdisMSynchronizeWithInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563681)します。 この呼び出しにより、ミニポート ドライバーの[ *MiniportSynchronizeInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559454)関数同期とマルチプロセッサの安全な方法で共有リソースにアクセスします。

 

 





