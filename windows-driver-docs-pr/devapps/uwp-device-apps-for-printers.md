---
title: プリンター用の UWP デバイス アプリ
description: このセクションでは、プリンター用の UWP デバイス アプリを紹介します。
ms.assetid: 3325B492-2A70-4EB7-99B0-3FE3E24CE398
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 881528423e31121f8e6705ab7bd2f86ca9a83e9f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359510"
---
# <a name="uwp-device-apps-for-printers"></a>プリンター用の UWP デバイス アプリ


このセクションでは、プリンター用の UWP デバイス アプリを紹介します。 UWP デバイス アプリでの印刷にカスタマイズした設定のフライアウトを使用したプリンター特別な機能を強調表示でき、通知をサポートします。 UWP デバイス アプリことができますもプリンターのステータスを表示、印刷ジョブの管理およびプリンターの保守タスクを実行します。 一般に UWP デバイス アプリの詳細について、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

**重要な**  UWP デバイス アプリの機能を使用するプリンターが v4 印刷ドライバー モデルをサポートする必要があります。 詳細については、次を参照してください。[開発 v4 印刷ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=314231)します。

 

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="how-to-display-printer-status.md" data-raw-source="[How to display printer status](how-to-display-printer-status.md)">プリンターのステータスを表示する方法</a></p></td>
<td align="left"><p>このトピックでは、C#のバージョン、<a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">設定と印刷通知</a>プリンターの状態を照会し、表示する方法を示すサンプル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="how-to-customize-print-settings.md" data-raw-source="[How to customize print settings](how-to-customize-print-settings.md)">印刷設定をカスタマイズする方法</a></p></td>
<td align="left"><p>このトピックでは、高度な印刷設定のフライアウトが導入されていて、表示方法、C#のバージョン、<a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">設定と印刷通知</a>サンプル カスタム ポップアップ付きの既定のフライアウトが置き換えられます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="working-with-print-notifications.md" data-raw-source="[Working with print notifications](working-with-print-notifications.md)">印刷通知の操作</a></p></td>
<td align="left"><p>このトピックでは、印刷の通知が導入されていて、表示方法、C#のバージョン、<a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">設定と印刷通知</a>サンプルでは、バック グラウンド タスクを使用して、印刷通知に応答します。 バック グラウンド タスクでは、ローカルのアプリ データの詳細の保存、トーストを送信、タイルおよびバッジの更新の通知を保存する方法を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="how-to-manage-print-jobs.md" data-raw-source="[How to manage print jobs](how-to-manage-print-jobs.md)">印刷ジョブを管理する方法</a></p></td>
<td align="left"><p>Windows 8.1 では、プリンター用の UWP デバイス アプリは、印刷ジョブを管理できます。 このトピックでは、C#のバージョン、<a href="https://go.microsoft.com/fwlink/p/?LinkID=299829" data-raw-source="[Print job management and printer maintenance](https://go.microsoft.com/fwlink/p/?LinkID=299829)">印刷ジョブの管理とプリンターの保守</a>印刷ジョブのビューを作成、それらのジョブを監視および必要に応じて、ジョブをキャンセルする方法を示すサンプル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="how-to-do-printer-maintenance.md" data-raw-source="[How to do printer maintenance](how-to-do-printer-maintenance.md)">プリンターのメンテナンスを実行する方法</a></p></td>
<td align="left"><p>Windows 8.1 では、UWP デバイス アプリは印刷ヘッドのアラインメントとノズルをクリーニングなどのプリンターのメンテナンスを実行できます。 このトピックでは、C#のバージョン、<a href="https://go.microsoft.com/fwlink/p/?LinkID=299829" data-raw-source="[Print job management and printer maintenance](https://go.microsoft.com/fwlink/p/?LinkID=299829)">印刷ジョブの管理とプリンターの保守</a>双方向通信 (Bidi) を使用して、このようなデバイスのメンテナンスを実行する方法を示すサンプル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="printer-extension-library-overview.md" data-raw-source="[Printer extension library overview](printer-extension-library-overview.md)">プリンター拡張機能ライブラリの概要</a></p></td>
<td align="left"><p>このトピックでは、プリンターの拡張機能ライブラリでは、デバイスの製造元に役立つライブラリは、自社のプリンター用の UWP デバイス アプリを作成します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idshouldicreateawindowsstoredeviceappformyprinterspanspan-idshouldicreateawindowsstoredeviceappformyprinterspanspan-idshouldicreateawindowsstoredeviceappformyprinterspanshould-i-create-a-uwp-device-app-for-my-printer"></a><span id="Should_I_create_a_Windows_Store_device_app_for_my_printer_"></span><span id="should_i_create_a_windows_store_device_app_for_my_printer_"></span><span id="SHOULD_I_CREATE_A_WINDOWS_STORE_DEVICE_APP_FOR_MY_PRINTER_"></span>プリンターの UWP デバイスのアプリを作成する必要がありますか。


たい場合は、プリンターの UWP デバイスのアプリを使用します。

-   1 ページあたり複数の写真の印刷などの高度なデバイス機能を強調表示します。
-   デバイス固有の推奨事項を作成します。 たとえば、イメージの管理オプションを表示または設定し、プリンターに固有の既定値を保存するメソッドを提供するデバイス アプリを使用できます。

## <a name="span-idgeneralrecommendationsspanspan-idgeneralrecommendationsspanspan-idgeneralrecommendationsspangeneral-recommendations"></a><span id="General_recommendations"></span><span id="general_recommendations"></span><span id="GENERAL_RECOMMENDATIONS"></span>一般的な推奨事項


-   Window.print() を呼び出した後、確認し、アプリの [印刷] ボタンの onClick イベント ハンドラー内からのエラー メッセージを処理します。 これにより、アプリをたとえば、プリンターが使用できない場合は、印刷要求を中止できます。
-   印刷できない場合にユーザーに通知し、可能であれば、失敗の理由を説明します。
-   印刷時の動作をカスタマイズする場合は、このコードを印刷コンパニオン アプリに分けます。 これを使用すると、コードをクラスし、テストおよびデバッグ プロセスを容易になります。
-   V3 プリンター ドライバーを使用するには、印刷時の動作をカスタマイズしないでください。
-   カスタマイズされた印刷の UI に、印刷デバイスには、[アクセサリ] をアドバタイズしません。
-   Microsoft Store のデバイス アプリが呼び出された理由に関連していない販売の項目を表示しません。 たとえば、インクが不足していることを示す通知をクリックすると、購入カートリッジを表示する関連するは。 ただし、印刷コードを販売または写真の印刷キットでは、この同じシナリオを試すこともに適したはありません。
-   複数の製品売上に関する会社の web サイトにユーザーをリダイレクトしません。
-   以外の印刷設定のタスクに関連する情報を表示しません。 たとえば、印刷ヘッドをクリーニングする方法、または配置して、ノズルをテストする方法についての情報を指定しません。

## <a name="span-idsamplesspanspan-idsamplesspanspan-idsamplesspansamples"></a><span id="Samples"></span><span id="samples"></span><span id="SAMPLES"></span>サンプル


プリンターの UWP デバイス アプリのサンプルは、UWP デバイス アプリで実装できるプリンターに関連する機能を示しています。 各サンプルにも含まれています、`PrinterExtensionLibrary`プロジェクトは、プリンターの拡張機能を支援するアプリで再利用できます。 プリンターの拡張機能ライブラリの COM の実装をラップする、[プリンター拡張機能インターフェイス](https://go.microsoft.com/fwlink/p/?LinkID=299887)v4 印刷ドライバーから。

-   [印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプルは、印刷ジョブを管理し、双方向通信 (Bidi) を使用してプリンターのメンテナンス タスクを実行する方法を示します。

-   [設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプルは、カスタマイズされたフライアウトの印刷設定は、高度なプリンターのステータスを表示でき、タイルでプリンターの通知を表示することができますを提供する UWP デバイス アプリを作成する方法を示していますまたは。トースト通知します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[V4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[プリンター拡張機能インターフェイス (v4 印刷ドライバー)](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP アプリの概要](getting-started.md)

[アプリを作成する UWP デバイス (ステップ バイ ステップ ガイド)](step-1--create-a-uwp-device-app.md)

[UWP デバイスのアプリ (ステップ バイ ステップ ガイド) のデバイス メタデータを作成します。](step-2--create-device-metadata.md)

 

 






