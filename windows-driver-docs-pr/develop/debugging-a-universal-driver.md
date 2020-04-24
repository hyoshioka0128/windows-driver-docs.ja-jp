---
title: ユニバーサル Windows ドライバーのデバッグ
description: ユニバーサル Windows ドライバーで使用できるデバッグ手法、特にインフライト トレース レコーダーについて説明します。
ms.date: 08/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 863cd334378d325f815e7704bd9078e2b53357cc
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "70020679"
---
# <a name="debugging-a-universal-windows-driver"></a>ユニバーサル Windows ドライバーのデバッグ 

ユニバーサル ドライバーのデバッグに関する全般情報については、「[Windows のデバッグの概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windows-debugging)」をご覧ください。

## <a name="inflight-trace-recorder"></a>インフライト トレース レコーダー

Windows 10 以降では、KMDF または UMDF ドライバー バイナリをビルドするときに、[インフライト トレース レコーダー](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-wpp-recorder)を通じて追加のドライバー デバッグ情報を取得するように設定できます。 この機能をユニバーサル Windows ドライバーで利用できます。

さらに、Visual Studio の KMDF テンプレートを使用すると、ドライバーは Windows ソフトウェア トレース プリプロセッサ (WPP) を使ってトレース メッセージを書き込みます。 ドライバー バイナリは、プロバイダー GUID を持つ ETW プロバイダーです。

ドライバー バイナリからトレース メッセージを送信するには、次のコードを使用します。

   ```cpp
   TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");
   ```

デバッガー セッション内で [!wmitrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-) を使うことで、Tracelog を使用して ETW ログにアクセスできます。

