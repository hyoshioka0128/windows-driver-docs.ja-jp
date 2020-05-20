---
title: Windows ドライバーのデバッグ
ms.assetid: d2d168fe-8be2-4a3d-bc29-4ab3a306296e
description: Windows ドライバーで使用できるデバッグ手法、特にインフライト トレース レコーダーについて説明します。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 32f0376da3cc6efd330a15fe68b7a04b58616d43
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270461"
---
# <a name="debugging-a-windows-driver"></a>Windows ドライバーのデバッグ 

デバッガー ドライバーについて詳しくは、「[Windows のデバッグの概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windows-debugging)」をご覧ください。

## <a name="inflight-trace-recorder"></a>インフライト トレース レコーダー

Windows 10 以降では、KMDF または UMDF ドライバー バイナリをビルドするときに、[インフライト トレース レコーダー](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-wpp-recorder)を通じて追加のドライバー デバッグ情報を取得するように設定できます。 この機能を Windows ドライバーで利用できます。

さらに、Visual Studio の KMDF テンプレートを使用すると、ドライバーは Windows ソフトウェア トレース プリプロセッサ (WPP) を使ってトレース メッセージを書き込みます。 ドライバー バイナリは、プロバイダー GUID を持つ ETW プロバイダーです。

ドライバー バイナリからトレース メッセージを送信するには、次のコードを使用します。

   ```cpp
   TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");
   ```

デバッガー セッション内で [!wmitrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-) を使うことで、Tracelog を使用して ETW ログにアクセスできます。

