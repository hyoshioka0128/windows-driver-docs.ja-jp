---
Description: This topic provides information for client driver developers about the tracing and logging features for Universal Serial Bus (USB).
title: Windows のイベント トレースは USB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcdf5d475339f928e83557fc36d42793e4ceb878
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553009"
---
# <a name="usb-event-tracing-for-windows"></a>Windows のイベント トレースは USB


このトピックでは、ユニバーサル シリアル バス (USB) 用に、トレースとログ記録機能についてドライバー開発者をクライアントの情報に示します。 この情報は、ユーザーの開発し、デバッグの USB デバイスに提供されます。 ツールをインストールし、トレース ファイルを作成し、USB のトレース ファイル内のイベントを分析する方法に関する情報が含まれます。 トピックでは、USB のエコシステムと USB のトレースとログ機能を使用して、正常に必要なハードウェアの包括的な知識があることを前提としています。

イベント トレースの解釈、Windows を理解する必要がありますも[Windows での USB ホスト側ドライバー](usb-3-0-driver-stack-architecture.md)、[公式の USB 仕様、およびデバイスの USB クラス仕様](http://www.usb.org/developers/docs/)します。

-   [Event Tracing for Windows について](#about-event-tracing-for-windows)
-   [ETW のログ記録の USB サポート](#usb-support-for-etw-logging)
-   [Windows 7 での USB ETW のサポート](#usb-etw-support-in-windows-7)
-   [Windows 8 における USB ETW のサポート](#usb-etw-support-in-windows-8)

## <a name="about-event-tracing-for-windows"></a>Event Tracing for Windows について


Event Tracing for Windows (ETW) は、オペレーティング システムによって提供される高速な汎用トレース機能です。 バッファリングとユーザー モード アプリケーションとカーネル モード デバイス ドライバーの両方で発生するイベントのトレース メカニズムを提供する、カーネルに実装されているログ メカニズムを使用します。 ETW は、動的に有効にする機能を提供します。 さらに、無効にするログ記録を必要とせず、運用環境で詳細なトレースを実行するが簡単に再起動してまたはアプリケーションを再起動します。 ログ記録メカニズムでは、非同期ライター スレッドがディスクに書き込まれるプロセッサごとのバッファを使用します。 最小国内騒乱状態でイベントを書き込むの大規模なサーバー アプリケーションは、このバッファー処理できます。

ETW は、Windows 2000 で導入されました。 その後、さまざまなコア オペレーティング システムとサーバー コンポーネントは、そのアクティビティをインストルメント化する ETW を採用しています。 ETW は、Windows プラットフォームの主要なインストルメンテーション テクノロジの 1 つではようになりました。 サード パーティ製のアプリケーション数が増加しても、インストルメンテーションに ETW を使用して、Windows が提供するイベントの一部を利用します。 ETW は、Windows プリプロセッサ (WPP) ソフトウェア トレース テクノロジにトレースする使いやすいマクロのセットを提供するに抽象化されても**printf**-開発中のデバッグ メッセージのスタイルを設定します。

ETW は、Windows Vista および Windows 7 が大幅にアップグレードされました。 最も重要な新機能の 1 つは、統一イベント プロバイダ モデルおよび Api です。 簡単に言えば、新しい統一 Api は、トレースのログとイベント プロバイダーの 1 つの一貫性があり、使いやすいメカニズムに書き込み、イベント ビューアーを結合します。 同時に、開発者を向上させるために ETW に追加されたいくつかの新機能およびエンドユーザーのエクスペリエンスします。

ETW と WPP の詳細については、イベントのトレースを参照してくださいと[Event Tracing for Windows (ETW)](https://msdn.microsoft.com/library/windows/hardware/ff545699)します。

## <a name="usb-support-for-etw-logging"></a>ETW のログ記録の USB サポート


USB では、Pc に、常に高まり続けるさまざまな周辺機器を接続する最も一般的な手段の 1 つです。 USB ホスト Pc と USB 周辺機器、およびシステム ベンダーでは、デバイスのベンダーの場合は、非常に大きなインストールされているベースがあると、エンドユーザーが期待して、システムおよびデバイス レベルで USB デバイスが問題なく動作する要求。

USB デバイスの急増によって、大規模なインストール ベースで、Windows USB ソフトウェア スタックと、USB ホスト コント ローラーと USB デバイスの間の互換性の問題が検出されました。 これらの互換性の問題では、デバイス操作の失敗、システム ハングの場合は、システムのクラッシュなどの顧客の問題が発生します。

困難または不可能な調査、USB デバイスの問題、システムやデバイス、または場合によっては、直接アクセスしないシステムのクラッシュ ダンプのデバッグとなっています。 ハードウェア、およびクラッシュ ダンプにフル アクセスを使用しても、関連する情報を抽出されましたが、いくつかの中核となる USB ドライバー開発者だけが知っているは時間がかかる手法。 ハードウェアまたはソフトウェアのアナライザーを使用して USB に関する問題をデバッグできますが、非常に高価なプロフェッショナルのごく一部のみを利用できます。

## <a name="usb-etw-support-in-windows-7"></a>Windows 7 での USB ETW のサポート


Windows 7 では、ETW は、USB ドライバー スタックは、調査、診断、および USB 関連の問題のデバッグを支援するために利用できるイベントのログ メカニズムを提供します。 USB ドライバー スタック ETW イベントのサポートを最もログ記録、またはすべての USB ドライバー スタックの制限事項が発生することがなく既存のアドホック ログ メカニズムによって提供される機能をデバッグします。 これは、長期間のより堅牢な USB ドライバー スタックを提供する必要があります USB 関連の問題のデバッグの容易さに変換します。

USB ホスト コント ローラーのドライバーを Windows 7 の USB ハブのドライバーを ETW のログ記録を追加しました。 USB ホスト コント ローラー ドライバー レイヤーには、ホスト コント ローラー ポート ドライバー (usbport.sys) と (usbehci.sys、usbohci.sys、および usbuhci.sys) のミニポート ドライバーが含まれています。 USB ハブのドライバーの層は、USB ハブのドライバー (usbhub.sys) で構成されます。 USB ドライバーの ETW イベント プロバイダーは、すべてのエディションと Windows 7 の Sku に含まれます。

-   USB ハブのイベント

    USB イベントの収集が有効になっている USB ハブのイベント プロバイダーは、加算と USB ハブの削除、ハブ、およびポートの状態の変更をすべてのデバイスの概要イベントを報告します。 これらのイベントを使用すると、ほとんどのデバイス列挙の障害の根本原因を特定します。

-   USB ポート イベント

    USB イベントの収集が有効になっている USB ポート イベント プロバイダーでは、I/O をレポート、デバイスのエンドポイントの開閉、クライアント ドライバーからとミニポートなどミニポート状態遷移を開始および停止します。 ログに記録された I/O には、物理の USB ポートの状態の要求が含まれています。 物理の USB ポートに状態遷移は、キー コアの USB ドライバー スタック内のアクティビティのイニシエーターの 1 つです。

## <a name="usb-etw-support-in-windows-8"></a>Windows 8 における USB ETW のサポート


Windows 8 では、USB 3.0 デバイスをサポートするために USB ドライバー スタックを提供します。 Microsoft 提供の USB 3.0 ドライバー スタックは、次の 3 つのドライバーで構成されます。Usbxhci.sys、Ucx01000.sys、および Usbhub3.sys です。 次の 3 つすべてのドライバーが連携してほとんどの USB 3.0 ホスト コント ローラーの Windows にネイティブにサポートを追加します。 新しいドライバー スタックは、SuperSpeed、高速な完全な高速および低速のデバイスをサポートします。 USB 2.0 ドライバー スタックは、Windows 8 でサポートされます。 イベントのトレースは、USB 3.0 ドライバー スタックは、ホスト コント ローラーとそれに接続されているすべてのデバイスの詳細なアクティビティのビューを提供します。

-   USB Hub3 イベント

    USB イベントの収集が有効になっていると、USB Hub3 イベント プロバイダーは、加算と USB ハブの削除、すべてのハブ、ポートの状態の変更、および USB デバイスとハブの電源状態のデバイスの概要イベントを報告します。 ポートの状態の変更は、物理の USB ポートに状態遷移ではキー コアの USB ドライバー スタック内のアクティビティのイニシエーターの 1 つ。 Hub3 では、ほとんどのデバイス列挙のエラーが発生するルートが、列挙処理の段階を報告します。 **StateMachine**キーワードを有効にすると、Hub3 ソフトウェア デバイス、ハブ、および詳細な可視ドライバーのロジックを提供するポート オブジェクトの内部のステート マシン アクティビティを報告します。

-   USB UCX イベント

    USB イベントの収集が有効になっていると、USB UCX イベント プロバイダーは、クライアント ドライバーとの開閉のデバイス エンドポイントとエンドポイント ストリームから I/O を報告します。 **StateMachine**キーワードを有効にすると、UCX ホスト コント ローラーとエンドポイント オブジェクトの場合、ドライバーのロジックの詳細な可視を提供する内部のステート マシン アクティビティを報告します。

-   USB xHCI イベント

    USB イベントの収集が有効になっていると、USB xHCI のイベント プロバイダーは、システムの xHCI コント ローラーのプロパティと xHCI 操作の低レベルの詳細を報告します。 xHCI では、コマンドの要求に送信され、完了の xHCI に固有のコードを含む、xHCI ハードウェアによって完了を報告します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="capture-and-view-ing-usb-traces-with-microsoft-message-analyzer-.md" data-raw-source="[Capture and view USB traces with Microsoft Message Analyzer](capture-and-view-ing-usb-traces-with-microsoft-message-analyzer-.md)">Microsoft Message Analyzer を使用した USB トレースのキャプチャとビュー</a></p></td>
<td><p>Microsoft メッセージ アナライザー (MMA) を使用して、キャプチャし、ライブの USB トレースを表示または既存のトレースを表示することができます。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-capture-a-usb-event-trace.md" data-raw-source="[How to capture a USB event trace with Logman](how-to-capture-a-usb-event-trace.md)">Logman の USB イベント トレースをキャプチャする方法</a></p></td>
<td><p>このトピックの使用に関する情報を提供する、 <a href="https://go.microsoft.com/fwlink/p/?linkid=617153" data-raw-source="[Logman](https://go.microsoft.com/fwlink/p/?linkid=617153)">Logman</a> USB ETW イベントのトレースをキャプチャするツール。 Logman は、Windows に組み込まれているトレース ツールです。 Logman を使用して、イベント トレース ログ ファイルにイベントをキャプチャすることができます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="using-usb-etw.md" data-raw-source="[Using activity ID GUIDs in USB ETW traces](using-usb-etw.md)">USB の ETW トレースでアクティビティ ID の Guid の使用</a></p></td>
<td><p>このトピックでは、情報を提供します。 イベントのこれらの Guid を追加する方法については、アクティビティ ID の Guid トレース プロバイダー、と Netmon で表示します。</p></td>
</tr>
<tr class="even">
<td><p><a href="viewing-etw-traces-in-netmon.md" data-raw-source="[USB ETW traces in Netmon](viewing-etw-traces-in-netmon.md)">Netmon で USB の ETW トレース</a></p></td>
<td><p>Netmon とも呼ばれます、Microsoft ネットワーク モニターを使用して USB ETW イベントのトレースを表示することができます。 ネットワーク モニターでは、トレースを自動的に解析しません。 USB ETW パーサーが必要です。 USB ETW パーサーはテキスト ファイル、ネットワーク モニター パーサーの言語 (NPL) で記述された USB ETW イベントのトレースの構造を記述します。 また、パーサーは、USB に固有の列とフィルターを定義します。 これらのパーサーは、Netmon USB ETW トレースを分析するための最適なツールを作成します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="using-xperf-with-usb-etw.md" data-raw-source="[Using Xperf with USB ETW](using-xperf-with-usb-etw.md)">Xperf を使用して USB ETW を使用しました。</a></p></td>
<td><p>このトピックでは、Netmon を Xperf を使用して、USB トレース データを分析する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-etw-and-power-management.md" data-raw-source="[USB ETW and Power Management](usb-etw-and-power-management.md)">USB ETW および電源管理</a></p></td>
<td><p>このトピックでは、簡単な ETW を使用して、USB のセレクティブを確認する方法の概要は中断状態と Windows PowerCfg ユーティリティを使用してシステムのエネルギー効率の問題を識別します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB の ETW を使用してください。](using-usb-etw.md)  
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  



