---
title: RCDRKD 拡張機能
description: ここでは、RCDRKD デバッガー拡張コマンドについて説明します。 これらのコマンドは、ドライバーによって作成された WPP トレースメッセージを表示します。
ms.assetid: 11CEBCED-2C11-4450-A5FB-BC5B48B1E1A3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df26d9961bf1d0e969d95adc2372efa7519a1143
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534313"
---
# <a name="rcdrkd-extensions"></a>RCDRKD 拡張機能


ここでは、RCDRKD デバッガー拡張コマンドについて説明します。 これらのコマンドは、ドライバーによって作成された WPP トレースメッセージを表示します。 Windows 8 以降では、WPP メッセージを解析するために、別のトレースメッセージ形式 (TMF) ファイルは必要なくなりました。 TMF 情報は、通常のシンボルファイル (PDB ファイル) に格納されます。

Windows 10 以降では、カーネルモードドライバーとユーザーモードドライバーは、[トレースのログ記録に Inflight トレースレコーダー (IFR)](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-wpp-recorder)を使用できます。 カーネルモードドライバーは、RCDRKD コマンドを使用して、循環バッファーからメッセージを読み取り、メッセージを書式設定し、メッセージをデバッガーに表示できます。

**メモ**   RCDRKD コマンドを使用して、UMDF ドライバーログ、UMDF フレームワークログ、KMDF フレームワークログを表示することはできません。 これらのログを表示するには、 [Windows Driver Framework Extensions (Wdfkd .dll)](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)コマンドを使用します。

 

RCDRKD デバッガー拡張コマンドは、Rcdrkd .dll に実装されています。 RCDRKD コマンドを読み込むには、デバッガーで「」と入力します **。**

次の2つのコマンドは、トレースメッセージを表示するための主なコマンドです。

-   [**!rcdrkd.rcdrlogdump**](-rcdrkd-rcdrlogdump.md)
-   [**!rcdrkd.rcdrcrashdump**](-rcdrkd-rcdrcrashdump.md)

次の補助コマンドは、トレースメッセージの表示と保存に関連するサービスを提供します。

-   [**!rcdrkd.rcdrloglist**](-rcdrkd-rcdrloglist.md)
-   [**!rcdrkd.rcdrlogsave**](-rcdrkd-rcdrlogsave.md)
-   [**!rcdrkd.rcdrsearchpath**](-rcdrkd-rcdrsearchpath.md)
-   [**!rcdrkd.rcdrsettraceprefix**](-rcdrkd-rcdrsettraceprefix.md)
-   [**!rcdrkd.rcdrtmffile**](-rcdrkd-rcdrtmffile.md)
-   [**!rcdrkd.rcdrtraceprtdebug**](-rcdrkd-rcdrtraceprtdebug.md)

[**! Rcdrkd. rcdrkd**](-rcdrkd-rcdrhelp.md)は、デバッガーの rcdrkd コマンドのヘルプを表示します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)

[フレームワークのイベント ロガーの使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-s-event-logger)

[USB 3.0 拡張機能](usb-3-extensions.md)

 

 






