---
title: プリンター用の UWP デバイス アプリ
description: このセクションでは、プリンター用の UWP デバイス アプリを紹介します。
ms.assetid: 3325B492-2A70-4EB7-99B0-3FE3E24CE398
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f55cfaae1b8494278830a3ae2f45a289fe13c0b
ms.sourcegitcommit: 6997fcbd0ad57e189c4b7c6b490632d1d53b6b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822816"
---
# <a name="uwp-device-apps-for-printers"></a>プリンター用の UWP デバイス アプリ


このセクションでは、プリンター用の UWP デバイス アプリを紹介します。 UWP デバイスアプリは、カスタマイズされた印刷設定 flyouts と通知のサポートによって、プリンターの特別な機能を強調することができます。 UWP デバイスアプリは、プリンターの状態を表示したり、印刷ジョブを管理したり、プリンターの保守タスクを実行したりすることもできます。 UWP デバイスアプリ全般の詳細については、 [uwp デバイスアプリの準拠](meet-uwp-device-apps.md)に関するページを参照してください。

**重要**  UWP デバイスアプリの機能を使用するには、プリンターで v4 印刷ドライバーモデルがサポートされている必要があります。 詳細については、「 [v4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)」を参照してください。

 

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


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
<td align="left"><p>このトピックではC# 、<a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">印刷設定と印刷通知</a>のサンプルのバージョンを使用して、プリンターの状態を照会して表示する方法を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="how-to-customize-print-settings.md" data-raw-source="[How to customize print settings](how-to-customize-print-settings.md)">印刷設定をカスタマイズする方法</a></p></td>
<td align="left"><p>このトピックでは、[印刷の詳細設定] ポップアップをC#紹介し、既定のポップアップをカスタムポップアップに置き換える、<a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">印刷設定と印刷通知</a>のサンプルのバージョンを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="working-with-print-notifications.md" data-raw-source="[Working with print notifications](working-with-print-notifications.md)">印刷通知の操作</a></p></td>
<td align="left"><p>このトピックでは、印刷通知についてC#説明します。また、印刷<a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">設定と印刷通知</a>のサンプルでは、バックグラウンドタスクを使用して印刷通知に応答する方法を示します。 バックグラウンドタスクでは、通知の詳細をローカルアプリデータストアに保存し、送信してタイルとバッジを更新する方法を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="how-to-manage-print-jobs.md" data-raw-source="[How to manage print jobs](how-to-manage-print-jobs.md)">印刷ジョブを管理する方法</a></p></td>
<td align="left"><p>Windows 8.1 では、プリンター用の UWP デバイスアプリで印刷ジョブを管理できます。 このトピックではC# 、<a href="https://go.microsoft.com/fwlink/p/?LinkID=299829" data-raw-source="[Print job management and printer maintenance](https://go.microsoft.com/fwlink/p/?LinkID=299829)">印刷ジョブの管理とプリンターのメンテナンス</a>のサンプルのバージョンを使用して、印刷ジョブのビューを作成し、それらのジョブを監視し、必要に応じてジョブをキャンセルする方法を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="how-to-do-printer-maintenance.md" data-raw-source="[How to do printer maintenance](how-to-do-printer-maintenance.md)">プリンターのメンテナンスを行う方法</a></p></td>
<td align="left"><p>Windows 8.1 では、UWP デバイスアプリは、印刷ヘッドの調整やノズルのクリーニングなど、プリンターのメンテナンスを実行できます。 このトピックではC# 、<a href="https://go.microsoft.com/fwlink/p/?LinkID=299829" data-raw-source="[Print job management and printer maintenance](https://go.microsoft.com/fwlink/p/?LinkID=299829)">印刷ジョブの管理とプリンターの保守</a>のサンプルのバージョンを使用して、双方向通信 (Bidi) を使用してこのようなデバイスのメンテナンスを実行する方法を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="printer-extension-library-overview.md" data-raw-source="[Printer extension library overview](printer-extension-library-overview.md)">プリンター拡張ライブラリの概要</a></p></td>
<td align="left"><p>このトピックでは、デバイスの製造元がプリンター用の UWP デバイスアプリを作成するのに役立つ、プリンター拡張ライブラリについて説明します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idshould_i_create_a_windows_store_device_app_for_my_printer_spanspan-idshould_i_create_a_windows_store_device_app_for_my_printer_spanspan-idshould_i_create_a_windows_store_device_app_for_my_printer_spanshould-i-create-a-uwp-device-app-for-my-printer"></a><span id="Should_I_create_a_Windows_Store_device_app_for_my_printer_"></span><span id="should_i_create_a_windows_store_device_app_for_my_printer_"></span><span id="SHOULD_I_CREATE_A_WINDOWS_STORE_DEVICE_APP_FOR_MY_PRINTER_"></span>プリンター用の UWP デバイスアプリを作成する必要がありますか。


次のような場合に、プリンターに UWP デバイスアプリを使用します。

-   ページごとに複数の写真を印刷するなど、高度なデバイス機能を強調表示します。
-   デバイス固有の推奨事項を作成します。 たとえば、デバイスアプリを使用してイメージ管理オプションを表示したり、プリンター固有の既定値を設定および保存するためのメソッドを提供したりすることができます。

## <a name="span-idgeneral_recommendationsspanspan-idgeneral_recommendationsspanspan-idgeneral_recommendationsspangeneral-recommendations"></a><span id="General_recommendations"></span><span id="general_recommendations"></span><span id="GENERAL_RECOMMENDATIONS"></span>一般的な推奨事項


-   Window. print () を呼び出した後、アプリの [印刷] ボタンの onClick イベントハンドラー内からエラーメッセージを確認し、処理します。 これにより、プリンターが使用できなくなった場合などに、アプリで印刷要求を中止できます。
-   印刷が失敗した場合にユーザーに通知し、可能であれば、エラーの原因を説明します。
-   印刷エクスペリエンスをカスタマイズする場合は、このコードを印刷コンパニオンアプリに分割します。 これにより、コードをクラスライブラリ立つし、テストとデバッグのプロセスを容易にすることができます。
-   V3 印刷ドライバーを使用するように印刷エクスペリエンスをカスタマイズしないでください。
-   カスタマイズした印刷 UI で、印刷デバイスのアクセサリをアドバタイズしないでください。
-   Microsoft Store デバイスアプリが呼び出された理由に関連しない販売品目を表示しません。 たとえば、ユーザーが、インクが不足していることを示す通知をクリックした後に、購入した印刷カートリッジを表示する場合に関連します。 ただし、同じシナリオで印刷コードや写真印刷キットを販売するのは適切ではありません。
-   製品の販売のために、会社の web サイトにユーザーをリダイレクトしないでください。
-   印刷設定の設定タスクに関係のない情報は表示されません。 たとえば、印刷ヘッドをクリーニングする方法や、印刷ノズルの整列とテスト方法に関する情報は提供しません。

## <a name="span-idsamplesspanspan-idsamplesspanspan-idsamplesspansamples"></a><span id="Samples"></span><span id="samples"></span><span id="SAMPLES"></span>Samples


プリンター用の UWP デバイスアプリのサンプルは、独自の UWP デバイスアプリで実装できるプリンター関連の機能を示しています。 各サンプルには `PrinterExtensionLibrary` プロジェクトも含まれています。このプロジェクトは、プリンターの拡張機能を利用するために、独自のアプリで再利用できます。 プリンター拡張ライブラリは、[プリンター拡張機能インターフェイス](https://go.microsoft.com/fwlink/p/?LinkID=299887)の COM 実装を v4 印刷ドライバーからラップします。


**Windows 8 のサンプル:**

-   [印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルでは、印刷ジョブを管理し、双方向通信 (Bidi) を使用してプリンターのメンテナンスタスクを実行する方法を示します。

-   [印刷設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)のサンプルでは、詳細な印刷設定用にカスタマイズされたフライアウトを提供する UWP デバイスアプリを作成する方法、プリンターの状態を表示する方法、およびタイルや toasts でプリンターの通知を表示する方法を示します。


**Windows 10 のサンプル:**

-   「[印刷ワークフローアプリを作成する」および「WSDAs を UWP に移行する](https://github.com/microsoft/print-oem-samples)」サンプルでは、OEM プリントパートナーは、印刷ワークフロー機能を使用し、既存の Windows ストアデバイスアプリ (WSDAs) コードをユニバーサル Windows プラットフォームに移行する方法を示しています。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[V4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[プリンター拡張インターフェイス (v4 印刷ドライバー)](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP アプリの概要](getting-started.md)

[UWP デバイスアプリを作成する (ステップバイステップガイド)](step-1--create-a-uwp-device-app.md)

[UWP デバイスアプリのデバイスメタデータを作成する (ステップバイステップガイド)](step-2--create-device-metadata.md)

 

 






