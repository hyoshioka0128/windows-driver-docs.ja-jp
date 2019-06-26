---
title: UMDF ドライバーでの WPP ソフトウェア トレースの使用
description: UMDF ドライバーでの WPP ソフトウェア トレースの使用
ms.assetid: d8469d29-dfc3-41b9-a72d-9dafb3e70123
keywords:
- トレースの WDK、framework ベースのドライバー ソフトウェア
- WDK の UMDF ドライバーのデバッグ ソフトウェア トレース
- WDK、framework ベースのドライバーのトレース
- WDK、framework ベースのドライバーをトレース WPP ソフトウェア
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e72c83d299be4136ed63ac199e046bac9fc6f06
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372150"
---
# <a name="using-wpp-software-tracing-in-umdf-drivers"></a>UMDF ドライバーでの WPP ソフトウェア トレースの使用


[WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)ドライバーをデバッグする際に役立つトレース メッセージを追加することができます。 さらに、フレームワークの[イベント ロガー](using-the-framework-s-event-logger.md)数百のトレース メッセージを表示することができますを提供します。

使用してトレース メッセージを表示する[traceview で](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)または[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)します。 できます[カーネル デバッガーにトレース メッセージを送信](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-do-i-send-trace-messages-to-a-kernel-debugger-)します。

### <a name="adding-tracing-messages-to-your-driver"></a>ドライバーへのメッセージのトレースの追加

フレームワークに基づくドライバーには、トレース メッセージを追加するには、次の必要があります。

-   追加、 **\#含める**WPP マクロのいずれかを含む、ドライバーのソース ファイルの各ディレクティブ。 このディレクティブを識別する必要があります、[トレース メッセージのヘッダー (TMH) ファイル](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-message-header-file)します。 ファイル名の形式である必要があります&lt;*ドライバー ソース ファイル名*&gt;.tmh します。

    たとえば、ドライバーが 2 つのソース ファイルで構成される場合が呼び出されます*MyDriver1.c*と*MyDriver2.c*、し*MyDriver1.c*含める必要があります。

    `#include "MyDriver1.tmh"`

    *MyDriver2.c*含める必要があります。

    `#include "MyDriver2.tmh"`

    Microsoft Visual Studio で、ドライバーをビルドすると、プリプロセッサ WPP は .tmh ファイルを生成します。

-   定義、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))ヘッダー ファイルでマクロ。 このマクロは定義 GUID と[トレース フラグ](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-flags)ドライバーのトレース メッセージ。 (WDK の UMDF ベースにしたサンプル ドライバーごとに、Internal.h ヘッダー ファイルを含むこのマクロ)

-   含める、 [WPP\_INIT\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))ドライバーの DllMain ルーチンでマクロ。 このマクロには、ソフトウェア トレースは、ドライバーがアクティブにします。 (WDK の UMDF ベースにしたサンプル ドライバーごとに、DllSup.h ヘッダー ファイルを含むこのマクロ)

-   含める、 [WPP\_クリーンアップ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))ドライバーの DllMain ルーチンでマクロ。 このマクロは、ソフトウェア トレースは、ドライバーを無効になります。 (WDK の UMDF ベースにしたサンプル ドライバーごとに、DllSup.h ヘッダー ファイルを含むこのマクロ)

-   使用して、 [ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロ、または[カスタマイズされたバージョン](https://docs.microsoft.com/windows-hardware/drivers/devtest/can-i-customize-dotracemessage-)トレース メッセージを作成するのには、ドライバー、マクロの。 (WDK の UMDF ベースにしたサンプル ドライバーごとに、Internal.h ヘッダー ファイルを含むカスタマイズされたマクロ)

-   ドライバー プロジェクトのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー プロジェクトを右クリックして、 **[プロパティ]** をクリックします。 ドライバーのプロパティ ページで次のようにクリックします。**構成プロパティ**、し**Wpp**します。 下、**全般**] メニューの [設定**WPP トレースの実行**[はい] にします。 下、**ファイル オプション**メニューで、たとえば、フレームワークの WPP テンプレート ファイルを指定することも必要があります。

    ```cpp
    {km-WdfDefault.tpl}*.tmh
    ```

トレース メッセージをドライバーを追加する方法の詳細については、次を参照してください。[ドライバーに WPP マクロを追加する](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-wpp-macros-to-a-trace-provider)します。

### <a name="sample-drivers-that-use-wpp-software-tracing"></a>WPP ソフトウェア トレースを使用しているサンプル ドライバー

すべての WDK で UMDF ベースにしたサンプル ドライバーは、WPP ソフトウェア トレースを有効にする DllSup.h、Internal.h、およびソース ファイルを提供します。 また、これらのサンプル ドライバーのほとんどは、トレース メッセージを作成するのにカスタマイズされたマクロを使用します。

### <a name="viewing-your-drivers-trace-messages"></a>ドライバーのトレース メッセージを表示します。

ドライバーは、トレース メッセージをドライバーを追加した場合、[トレース プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-provider)します。 使用することができます、[トレース コント ローラー](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-controller)など[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)、制御、[トレース セッション](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-session)を作成し、[トレース ログ](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-log)。 使用することができます、[トレース コンシューマー](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-consumer)など[Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt)メッセージを表示します。

ソフトウェア トレース ツールを使用する方法の詳細については、次を参照してください。[ソフトウェア トレース ツールのアンケート](https://docs.microsoft.com/windows-hardware/drivers/devtest/survey-of-software-tracing-tools)します。

### <a name="viewing-the-umdf-trace-log"></a>UMDF トレース ログを表示します。

UMDF のログ ファイルは %windir%\\system32\\LogFiles\\WUDF\\WUDFTrace.etl します。

**注**  ログ ディレクトリは、UMDF 2.15 以降、 *%programdata%* \\Microsoft\\WDF します。

 

UMDF のログ ファイルを表示するにはいずれかを使用して[traceview で](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)または[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)します。 どちらのツールでは、トレース メッセージの形式 (TMF) ファイル、トレース ログのメッセージの形式を指定する必要があります。 TMF ファイルは、下の WDK で使用できる、\\ツール\\トレース サブディレクトリ。 (Traceview で、UMDF として表示されます UMDF バージョンに応じて「UMDF Framework トレース」または「Framework トレース」の名前を持つ名前付きプロバイダー。)

[WDF Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application) UMDF のトレース ログと、カーネル デバッガーの両方にトレース メッセージを送信することができます。 (を使用して、カーネル デバッガーにトレース メッセージを送信する必要がありますいない、 **-kd**オプション[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)ため、 **Tracelog** UMDF 内のトレース ログ記録を中断することができます)。

使用することも、 [ **! wmitrace** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)デバッガー拡張機能を[トレース メッセージを表示](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-do-i-send-trace-messages-to-a-kernel-debugger-)デバッガーで。

1.  、WinDbg でドライバーをホストする WUDFHost のインスタンスにアタッチします。 詳細については、次を参照してください。 [UMDF ドライバーのデバッグを有効にする方法](enabling-a-debugger.md)します。
2.  ドライバー バージョン 1.11 以降を使用して、Windows 8 またはそれ以降、カーネル デバッガーを使用している場合は、この手順をスキップすることができます。 ドライバーは、UMDF 1.11 より前のバージョンを使用している場合を使用して、 [ **! wmitrace.tmffile** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wmitrace-tmffile)または[ **! wmitrace.searchpath** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wmitrace-searchpath)を指定する、プラットフォーム固有のトレース メッセージの形式 (.tmf) ファイル、または .tmf ファイルへのパス。 .Tmf ファイルは、WDK でプラットフォーム固有のサブディレクトリに配置されます。

3.  使用して、 [ **! wmitrace.logdump** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wmitrace-logdump)トレース バッファーの内容を表示するコマンド。

    ```cpp
    !wmitrace.logdump WudfTrace
    ```

### <a name="controlling-trace-messages"></a>トレース メッセージを制御します。

UMDF を制御するトレース メッセージをユーザー インターフェイスを[WDF Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)提供、またはレジストリ値を変更することで。 使用する必要があります、 **WDF Verifier**可能であれば、インターフェイスのレジストリ値が将来のバージョンの UMDF で変わる可能性があります。 さらに、INF ファイルまたはドライバーのコード内でこれらの値にアクセスすることはできません。

現時点では、下にある次のレジストリ値を変更することができます、 **HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**レジストリ キー:

-   **LogEnable** UMDF ドライバーのトレース ログを作成するかどうかのコントロールの値します。 この値が 1 に設定されている場合、UMDF には、トレース ログが作成されます。

-   **LogLevel** UMDF トレース メッセージが含まれている情報の量を制御する値。 既定値**LogLevel** UMDF トレース メッセージのエラーを含むメッセージと警告メッセージが 3 では、します。 7 エラーと警告メッセージ、およびエラーのない情報メッセージを含めるには、この値を設定します。 UMDF が提供することのできる、トレース情報をすべて含める 15 に設定します。

-   **LogKd** UMDF、カーネル デバッガーにトレース メッセージを送信するかどうかのコントロールの値します。 場合**LogKd** 1、UMDF 送信しますが、カーネル デバッガーにメッセージをトレースに設定されます。

-   **LogFlushPeriodSeconds**値では、どのくらいの頻度 (秒単位) トレースに書き込まれたトレース ログを指定します。

-   **LogMinidumpType**値には、ミニ ダンプ ファイルが生成された場合に格納する情報の種類を指定するフラグが含まれています。 これらのフラグの詳細については、次を参照してください。、[ミニダンプ\_型](https://go.microsoft.com/fwlink/p/?linkid=160310)列挙体。

下の追加のレジストリ値を見つけることがあります、 **HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**レジストリ キー。 これらの値を変更する必要があります。

 

 





