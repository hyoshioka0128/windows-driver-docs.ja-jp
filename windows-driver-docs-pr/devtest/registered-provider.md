---
title: 登録済みのプロバイダー
description: 登録済みのプロバイダー
ms.assetid: d16e91d7-40ce-4a35-b3a7-f46f26a810bb
keywords:
- 登録されているプロバイダーの WDK ソフトウェア トレース
- トレース プロバイダー WDK
- イベント トレースの Windows WDK、プロバイダー
- WDK ETW プロバイダー
- WDK の ETW プロバイダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c066c16fc7c8ccdfd940f86d8a95ec55b32f23fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532153"
---
# <a name="registered-provider"></a>登録済みのプロバイダー

## <span id="ddk_registered_provider_tools"></span><span id="DDK_REGISTERED_PROVIDER_TOOLS"></span>

A*登録済みのプロバイダー*は、[トレース プロバイダー](trace-provider.md)登録された[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)します。 ユーザーが登録されているプロバイダーを列挙し、名前で参照できます。

開始するときに、ETW を使用したトレース プロバイダーを登録する必要がありますを呼び出すか**EventRegister**マクロまたはなど、トレース フレームワークによって提供される関数の登録を使用して、または、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)WPP によって提供されるマクロです。 か、呼び出すことによって、停止する前に、登録を解除**EventUnregister**またはフレームワークを使用して、マクロ、または関数を登録解除します。 自体にも登録しないでトレース プロバイダーを有効にすることはできません、そこからイベントが収集されなくなります。

登録済みのプロバイダーからのイベントを表示する使用[traceview で](traceview.md)します。 手順については、[登録済みのプロバイダーのトレース セッションを作成する](creating-a-trace-session-for-a-registered-provider.md)を参照してください。

登録されているプロバイダーの詳細については、次を参照してください。[イベント トレーシング](https://msdn.microsoft.com/library/windows/desktop/bb968803)、Microsoft Windows sdk。
