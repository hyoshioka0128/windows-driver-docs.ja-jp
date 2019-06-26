---
title: RCDRKD 拡張機能
description: このセクションでは、RCDRKD デバッガー拡張機能のコマンドについて説明します。 これらのコマンドは、ドライバーによって作成される WPP トレース メッセージを表示します。
ms.assetid: 11CEBCED-2C11-4450-A5FB-BC5B48B1E1A3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6471be26000875fb229e63cab23243cdf7386799
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366430"
---
# <a name="rcdrkd-extensions"></a>RCDRKD 拡張機能


このセクションでは、RCDRKD デバッガー拡張機能のコマンドについて説明します。 これらのコマンドは、ドライバーによって作成される WPP トレース メッセージを表示します。 Windows 8 以降が不要になった WPP メッセージを解析する個別のトレース メッセージの形式 (TMF) ファイル。 TMF 情報は、正規表現のシンボル ファイル (PDB ファイル) に格納されます。

カーネル モードとユーザー モード ドライバーを使用できる Windows 10 以降、[ログ トレースのように、転送トレース レコーダー (IFR)](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-wpp-recorder)します。 カーネル モード ドライバーは、循環バッファーからメッセージを読み取る、メッセージを書式設定、およびデバッガーで、メッセージを表示する RCDRKD コマンドを使用することができます。

**注**  RCDRKD コマンドを使用して、UMDF ドライバーのログ、UMDF フレームワークのログ、および KMDF フレームワークのログを表示することはできません。 これらのログを表示する使用[Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)コマンド。

 

RCDRKD デバッガー拡張機能のコマンドは、Rcdrkd.dll で実装されます。 RCDRKD コマンドを読み込むには、次のように入力します。 **.load rcdrkd.dll**デバッガーでします。

次の 2 つのコマンドは、トレース メッセージを表示するための主要なコマンドです。

-   [ **!rcdrkd.rcdrlogdump**](-rcdrkd-rcdrlogdump.md)
-   [ **!rcdrkd.rcdrcrashdump**](-rcdrkd-rcdrcrashdump.md)

次の補助コマンドでは、表示して、トレース メッセージの保存に関連するサービスを提供します。

-   [ **!rcdrkd.rcdrloglist**](-rcdrkd-rcdrloglist.md)
-   [ **!rcdrkd.rcdrlogsave**](-rcdrkd-rcdrlogsave.md)
-   [ **!rcdrkd.rcdrsearchpath**](-rcdrkd-rcdrsearchpath.md)
-   [ **!rcdrkd.rcdrsettraceprefix**](-rcdrkd-rcdrsettraceprefix.md)
-   [ **!rcdrkd.rcdrtmffile**](-rcdrkd-rcdrtmffile.md)
-   [ **!rcdrkd.rcdrtraceprtdebug**](-rcdrkd-rcdrtraceprtdebug.md)

[ **! Rcdrkd.rcdrhelp** ](-rcdrkd-rcdrhelp.md)デバッガーで RCDRKD コマンドのヘルプを表示します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WPP ソフトウェア トレース](https://go.microsoft.com/fwlink/p?LinkID=251984)

[フレームワークのイベントのロガーを使用します。](https://go.microsoft.com/fwlink/p?LinkID=251985)

[USB 3.0 の拡張機能](usb-3-extensions.md)

 

 






