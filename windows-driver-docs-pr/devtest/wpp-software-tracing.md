---
title: WPP ソフトウェア トレース
description: このセクションでは、Windows ソフトウェア トレース プリプロセッサ (WPP) を使用して、ソフトウェア コンポーネントのトレース プロバイダーの操作を追跡する方法について説明します。
ms.assetid: dab776b3-bac9-4157-a530-6e48868ba900
keywords:
- Windows ソフトウェア トレース プリプロセッサ WDK
- WDK のトレース WPP ソフトウェア
- WDK、WPP トレース ソフトウェア
- カーネル モードの WDK の WPP ソフトウェア トレース
- Windows ソフトウェア トレース プリプロセッサ WDK、WPP について
- WDK、WPP に関するトレース WPP ソフトウェア
- 既定 WPP ソフトウェア トレース
- トレース WDK、WPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8a8fcb35711278d582f3e917fa3c870904bcb7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377704"
---
# <a name="wpp-software-tracing"></a>WPP ソフトウェア トレース


このセクションを使用する方法を説明します、 *Windows ソフトウェア トレース プリプロセッサ*(WPP) ソフトウェア コンポーネントの操作を追跡する ([トレース プロバイダー](trace-provider.md))。 トレース プロバイダーは、次のいずれかを指定できます。

-   カーネル モード ドライバーです。

-   ユーザー モード ドライバー、アプリケーション、またはダイナミック リンク ライブラリ (DLL) です。

WPP ソフトウェア トレースを補完および強化[WMI イベントのトレース](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-event-tracing)トレース プロバイダーの操作のトレースを簡略化する方法を追加します。 これは、リアルタイムのバイナリ メッセージを記録するトレース プロバイダーの効率的なメカニズムです。 ログに記録されたメッセージは、人間が判読できるトレースのトレース プロバイダーの操作を後で変換できます。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP ソフトウェア トレースを使用する場合</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WPP ソフトウェア トレースは、主に開発中にコードのデバッグです。 アプリケーションの開発中は、トレースに加え、構造化された ETW イベントの目的で使用できるイベントを発行する場合、次の手順に従います。</p>
<ul>
<li>カーネル モード ドライバーでは、使用、 <a href="event-tracing-for-windows--etw-.md" data-raw-source="[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)">Event Tracing for Windows (ETW)</a> API。</li>
<li>ユーザー モード ドライバーやアプリケーションでは、使用して、<a href="https://docs.microsoft.com/windows/desktop/ETW/event-tracing-portal" data-raw-source="[Event Tracing](https://docs.microsoft.com/windows/desktop/ETW/event-tracing-portal)">イベント トレーシング</a>(Windows デスクトップ) API です。</li>
</ul>
詳細については、次を参照してください。 <a href="tools-for-software-tracing.md" data-raw-source="[When should I use WPP Software Tracing or the Event Tracing for Windows (ETW) API?](tools-for-software-tracing.md)">WPP ソフトウェア トレース出力または、Event Tracing for Windows (ETW) API を使用する必要があります場合でしょうか。</a></td>
</tr>
</tbody>
</table>

 

WPP ソフトウェア トレースとメッセージのログ記録は、Windows イベント ログ サービスを使用すると似ています。 ドライバーでは、メッセージ ID と書式設定されていないバイナリ データをログ ファイルに記録します。 その後、ポスト プロセッサは、人間が判読できる形式にログ ファイルの情報を変換します。 ただし、WPP ソフトウェア トレースは、可能で、イベント ログ サービスでサポートされているよりも柔軟なメッセージ形式をサポートします。 たとえば、WPP ソフトウェア トレースでは、IP アドレス、Guid、システム Id、タイムスタンプ、およびその他の有用なデータ型の組み込みサポートがあります。 さらに、ユーザーは、そのアプリケーションに関連するカスタム データ型を追加できます。

WPP ソフトウェア トレースは、Microsoft Windows 2000 および Windows の以降のバージョンでサポートされます。

### <a name="an-overview-of-the-wpp-software-tracing-process"></a>WPP ソフトウェア トレース プロセスの概要

WPP ソフトウェア トレースをドライバーまたはアプリケーションに追加するための基本的なプロセスには、次の手順が含まれています。 WDF のドライバーを作成するために、WDK で提供される Visual Studio テンプレートのいずれかを使用する場合、作業の多くが行われます。

-   コントロール、ドライバーまたはとしてアプリケーションを一意に識別する GUID を定義、[トレース プロバイダー](trace-provider.md)します。 プロバイダーの定義にこの GUID を指定する、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロや関連するコントロール ファイルで使用される[Tracelog](tracelog.md)別または[トレースコント ローラー](trace-controller.md)します。

-   必要な追加 WPP に関連する C プリプロセッサ ディレクティブと WPP マクロの呼び出しをプロバイダーのソース、ファイル、」の説明に従って[Windows ドライバーに WPP ソフトウェア トレースを追加する](adding-wpp-software-tracing-to-a-windows-driver.md)し[WPPソフトウェアトレースリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556205(v=vs.85)).

-   説明に従って、WPP プリプロセッサを実行し、ドライバーをビルドする Visual Studio プロジェクトを変更[手順 6](adding-wpp-software-tracing-to-a-windows-driver.md#step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution)の Windows ドライバーに WPP ソフトウェア トレースを追加します。 参照することができます、 [WPP プリプロセッサ](wpp-preprocessor.md)のビルド時のオプションの詳細。

-   ドライバーまたはコンポーネントをインストールします。 トレース セッションを開始し、トレース メッセージを記録します。 などのソフトウェアのトレース ツールを使用して[traceview で](traceview.md)、 [Tracelog](tracelog.md)、 [Tracefmt](tracefmt.md)、および[Tracepdb](tracepdb.md)構成、起動、および停止するにはセッションのトレースを表示し、トレース メッセージをフィルター処理するとします。 これらのツールは、Windows Driver Kit (WDK) で含まれています。

## <a name="in-this-section"></a>このセクションの内容


-   [Windows Driver のトレース WPP ソフトウェアを追加します。](adding-wpp-software-tracing-to-a-windows-driver.md)
-   [ログ トレースの実行中のトレース レコーダー](using-wpp-recorder.md)
-   [トレース プロバイダーのトレース WPP ソフトウェアを使用します。](using-wpp-software-tracing-in-a-trace-provider.md)
-   [トレース プロバイダーへの WPP マクロの追加](adding-wpp-macros-to-a-trace-provider.md)
-   [WPP プリプロセッサ](wpp-preprocessor.md)
-   [トレースと診断の WDF ドライバー](tracing-and-diagnosability-for-wdf-drivers.md)

**注**   Event Tracing for Windows (ETW) と WPP カーネル モードとユーザー モード ドライバーのほとんどの種類をサポートします。 ただし、ETW と WPP は、ドライバー、ミニポート ドライバーなどの特定の種類では使用する型を使用します。 特定のドライバーの種類がサポートされているかどうかを判断する基本的な WPP にマクロを追加、ドライバーなど[WPP\_INIT\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))と[WPP\_クリーンアップ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))します。 使用される型が定義されていないために、コードはコンパイルされません、ETW、WPP はドライバーの種類をサポートできません。
ETW の詳細については、次を参照してください。[イベント トレーシング](https://go.microsoft.com/fwlink/p/?linkid=179202)Windows SDK のドキュメント。

**注**WPP トレース プロバイダーは、一度に 1 つのトレース セッションでのみ有効にできます。 参照してください[WPP プロバイダー](https://docs.microsoft.com/windows/desktop/ETW/about-event-tracing#providers)詳細についてはします。

については、 [WMI ライブラリ サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)WPP ソフトウェア トレースをサポートするを参照してください。

[**WmiQueryTraceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-wmiquerytraceinformation)

[**WmiTraceMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-wmitracemessage)

[**WmiTraceMessageVa**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-wmitracemessageva)

 

 





