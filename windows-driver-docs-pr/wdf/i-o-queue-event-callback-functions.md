---
title: I/O キュー イベントのコールバック関数
description: I/O キュー イベントのコールバック関数
ms.assetid: 5aa63c47-493d-4583-9eaa-1e50fdc089dd
keywords:
- WDK UMDF の I/O キュー
- WDK UMDF キュー
- WDK UMDF のコールバック関数
- WDK UMDF のイベントのコールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 652201844dbe6a7035125b3126f6454a144d4205
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532628"
---
# <a name="io-queue-event-callback-functions"></a>I/O キュー イベントのコールバック関数


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、の I/O キューを作成または既定の I/O キューの構成、フレームワークは、インターフェイスに関連するイベントが発生したときに、--インターフェイスに関連付けられているメソッドを呼び出すことによって、ドライバーを通知するため、次のインターフェイスを登録することができます。 I/O キューの作成と構成の I/O キューの詳細については、次を参照してください。 [Framework I/O キュー オブジェクト](framework-i-o-queue-object.md)します。

[IQueueCallbackCreate](https://msdn.microsoft.com/library/windows/hardware/ff556837)

[IQueueCallbackDeviceIoControl](https://msdn.microsoft.com/library/windows/hardware/ff556852)

[IQueueCallbackRead](https://msdn.microsoft.com/library/windows/hardware/ff556872)

[IQueueCallbackWrite](https://msdn.microsoft.com/library/windows/hardware/ff556882)

[IQueueCallbackDefaultIoHandler](https://msdn.microsoft.com/library/windows/hardware/ff556843)

 

 





