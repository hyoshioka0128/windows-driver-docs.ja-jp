---
title: CustomTimerDpc コンテキスト情報を提供します。
description: CustomTimerDpc コンテキスト情報を提供します。
ms.assetid: b4d711fb-63d4-45c6-8054-f934741ce340
keywords:
- タイマー オブジェクトの WDK カーネル、CustomTimerDpc ルーチン
- CustomTimerDpc
- DeferredContext ルーチン
- WDK の同期のコンテキスト情報
- タイマー オブジェクトの WDK カーネル、コンテキスト情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b616ad73439601e072b8f0238f6b76d5497a73f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556503"
---
# <a name="providing-customtimerdpc-context-information"></a>CustomTimerDpc コンテキスト情報を提供します。





*DeferredContext*にポインターが渡される[ **KeInitializeDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552130)コンテキスト領域を指す、その他のドライバー ルーチンと*CustomTimerDpc*ルーチン自体は、状態を保持できます。 カーネル渡す、 *DeferredContext* DPC ルーチンを呼び出すたびにポインター。

異なり、 *IoTimer*ルーチンを*CustomTimerDpc*デバイスのドライバーが作成したオブジェクトを使用した特定の関連付けがありません。 ただし、ドライバーに関連付けることができます、 *CustomTimerDpc*ルーチン コンテキストにあるデバイスのオブジェクトへのポインターを含めることでデバイスのドライバーが作成したオブジェクトを使用します。

常駐、ドライバーによって割り当てられたメモリにコンテキストの領域がある必要があります。 通常、このコンテキストの領域は、デバイスの拡張機能が非ページ プールのこともできます。 ドライバーは、コント ローラー オブジェクトを使用して、コント ローラーの拡張機能にことができます。 コンテキストの領域の内容は、ドライバーが決定します。

場合、 *CustomTimerDpc*ルーチンは、ドライバーの ISR とコンテキスト情報を共有、 *CustomTimerDpc*ルーチンを使用する必要があります[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)を呼び出す、 *SynchCritSection*共有コンテキストにアクセスするルーチン。 詳細については、次を参照してください。[クリティカル セクションを使用して](using-critical-sections.md)します。

場合、 *CustomTimerDpc*コンテキスト情報を他の ISR 以外のドライバー ルーチンにある領域を共有*DeferredContext* executive スピン ロックで保護する必要があります。 詳細については、次を参照してください。[スピン ロック](spin-locks.md)します。

 

 




