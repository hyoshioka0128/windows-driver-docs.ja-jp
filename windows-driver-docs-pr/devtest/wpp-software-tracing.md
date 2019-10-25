---
title: WPP ソフトウェアのトレース
description: このセクションでは、Windows software trace プリプロセッサ (WPP) を使用して、ソフトウェアコンポーネントトレースプロバイダーの操作をトレースする方法について説明します。
ms.assetid: dab776b3-bac9-4157-a530-6e48868ba900
keywords:
- Windows ソフトウェアトレースプリプロセッサ WDK
- WPP ソフトウェアトレース WDK
- ソフトウェアトレース WDK、WPP
- カーネルモードの WPP WDK ソフトウェアのトレース
- Windows ソフトウェアトレースプリプロセッサ WDK、WPP について
- WPP ソフトウェアトレース WDK、WPP について
- 既定の WPP ソフトウェアのトレース
- WDK のトレース、WPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c484639102f09bad1aae022f2a1dc801911fac5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839083"
---
# <a name="wpp-software-tracing"></a>WPP ソフトウェアのトレース


このセクションでは、 *Windows software trace プリプロセッサ*(WPP) を使用して、ソフトウェアコンポーネント ([トレースプロバイダー](trace-provider.md)) の操作をトレースする方法について説明します。 トレースプロバイダーは、次のいずれかになります。

-   カーネルモードドライバー。

-   ユーザーモードドライバー、アプリケーション、またはダイナミックリンクライブラリ (DLL)。

WPP ソフトウェアトレースは、トレースプロバイダーの操作のトレースを簡略化する方法を追加することによって、 [WMI イベントのトレース](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-event-tracing)を補足し、拡張します。 これは、トレースプロバイダーがリアルタイムのバイナリメッセージをログに記録するための効率的なメカニズムです。 その後、ログに記録されたメッセージを、ユーザーが判読できるトレースプロバイダーの操作のトレースに変換できます。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP ソフトウェアトレースを使用するタイミング</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WPP ソフトウェアトレースは、主に開発時のコードのデバッグを目的としています。 構造化された ETW イベントに関心のあるアプリケーションで使用できるイベントを発行する場合は、開発中のトレースに加えて、次のようにします。</p>
<ul>
<li>カーネルモードドライバーの場合は、 <a href="event-tracing-for-windows--etw-.md" data-raw-source="[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)">Windows イベントトレーシング (ETW)</a> API を使用します。</li>
<li>ユーザーモードのドライバーまたはアプリケーションの場合は、<a href="https://docs.microsoft.com/windows/desktop/ETW/event-tracing-portal" data-raw-source="[Event Tracing](https://docs.microsoft.com/windows/desktop/ETW/event-tracing-portal)">イベントトレース</a>(Windows デスクトップ) API を使用します。</li>
</ul>
詳細については、「<a href="tools-for-software-tracing.md" data-raw-source="[When should I use WPP Software Tracing or the Event Tracing for Windows (ETW) API?](tools-for-software-tracing.md)">どのような場合に WPP ソフトウェアのトレースまたは Windows イベントトレーシング (ETW) API を使用するか</a>」を参照してください。</td>
</tr>
</tbody>
</table>

 

WPP ソフトウェアトレースを使用したメッセージのログ記録は、Windows イベントログサービスの使用に似ています。 ドライバーは、メッセージ ID と書式設定されていないバイナリデータをログファイルに記録します。 その後、ポストプロセッサは、ログファイル内の情報を人間が判読できる形式に変換します。 ただし、WPP ソフトウェアのトレースでは、イベントログサービスでサポートされているものよりも高い柔軟性と柔軟性を備えたメッセージ形式がサポートされています。 たとえば、WPP ソフトウェアトレースには、IP アドレス、Guid、システム Id、タイムスタンプ、およびその他の便利なデータ型のサポートが組み込まれています。 さらに、ユーザーは、アプリケーションに関連するカスタムデータ型を追加できます。

WPP ソフトウェアトレースは、Microsoft Windows 2000 以降のバージョンの Windows でサポートされています。

### <a name="an-overview-of-the-wpp-software-tracing-process"></a>WPP ソフトウェアのトレースプロセスの概要

WPP ソフトウェアトレースをドライバーまたはアプリケーションに追加するための基本的なプロセスには、次の手順が含まれます。 WDF ドライバーを作成するために WDK に用意されているいずれかの Visual Studio テンプレートを使用すると、多くの作業が行われます。

-   [トレースプロバイダー](trace-provider.md)としてドライバーまたはアプリケーションを一意に識別するコントロールの GUID を定義します。 プロバイダーは、 [WPP\_制御\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロの定義、および[tracelog](tracelog.md)や別の[トレースコントローラー](trace-controller.md)によって使用される関連するコントロールファイルにこの GUID を指定します。

-   「Windows ドライバーおよび[Wpp ソフトウェアトレースリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556205(v=vs.85))[への wpp ソフトウェアトレースの追加](adding-wpp-software-tracing-to-a-windows-driver.md)」の説明に従って、必要な wpp 関連の C プリプロセッサディレクティブおよび wpp マクロ呼び出しをプロバイダーのソースファイルに追加します。

-   「Windows ドライバーへの WPP ソフトウェアトレースの追加」の[手順 6](adding-wpp-software-tracing-to-a-windows-driver.md#step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution) . で説明されているように、Visual Studio プロジェクトを変更して、wpp プリプロセッサを実行し、ドライバーをビルドします。 より多くのビルド時間オプションについては、 [WPP プリプロセッサ](wpp-preprocessor.md)を参照できます。

-   ドライバーまたはコンポーネントをインストールします。 トレースセッションを開始し、トレースメッセージを記録します。 [Traceview](traceview.md)、 [traceview](tracelog.md)、 [Tracefmt](tracefmt.md)、 [traceview](tracepdb.md)などのソフトウェアトレース用のツールを使用して、トレースセッションの構成、開始、停止、トレースメッセージの表示とフィルター処理を行います。 これらのツールは、Windows Driver Kit (WDK) に含まれています。

## <a name="in-this-section"></a>このセクションの内容


-   [Windows ドライバーに WPP ソフトウェアトレースを追加する](adding-wpp-software-tracing-to-a-windows-driver.md)
-   [トレースログのトレースレコーダー](using-wpp-recorder.md)
-   [トレースプロバイダーでの WPP ソフトウェアトレースの使用](using-wpp-software-tracing-in-a-trace-provider.md)
-   [トレースプロバイダーへの WPP マクロの追加](adding-wpp-macros-to-a-trace-provider.md)
-   [WPP プリプロセッサ](wpp-preprocessor.md)
-   [WDF ドライバーのトレースと Diagnosability](tracing-and-diagnosability-for-wdf-drivers.md)

**注**   WINDOWS イベントトレーシング (ETW) と WPP では、ほとんどの種類のカーネルモードドライバーとユーザーモードドライバーがサポートされています。 ただし、ETW および WPP は、ミニポートドライバーなど、特定の種類のドライバーで使用できない型を使用します。 特定のドライバーの種類がサポートされているかどうかを判断するには、ドライバーに基本的な WPP マクロを追加します。たとえば、 [wpp\_INIT\_TRACING](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))や[wpp\_クリーンアップ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))などです。 使用されている型が定義されていないためにコードがコンパイルされない場合、ETW および WPP はドライバーの種類をサポートできません。
ETW の詳細については、Windows SDK のドキュメントの「[イベントトレース](https://go.microsoft.com/fwlink/p/?linkid=179202)」を参照してください。

**メモ**WPP トレースプロバイダーは、一度に1つのトレースセッションでのみ有効にすることができます。 詳細については、「 [WPP プロバイダー](https://docs.microsoft.com/windows/desktop/ETW/about-event-tracing#providers) 」を参照してください。

WPP ソフトウェアトレースをサポートする[WMI ライブラリサポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)の詳細については、以下を参照してください。

[**参照 Querytraceinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-wmiquerytraceinformation)

[**WmiTraceMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-wmitracemessage)

[**WmiTraceMessageVa**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-wmitracemessageva)

 

 





