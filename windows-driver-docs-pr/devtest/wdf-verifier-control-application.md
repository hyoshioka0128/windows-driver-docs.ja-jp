---
title: WDF 検証ツール制御アプリケーション
description: Windows Driver Frameworks (WDF) Verifier コントロール アプリケーション (WdfVerifier.exe) は、KMDF および UMDF ドライバーをデバッグするためのツールです。
ms.assetid: 896b63db-69c6-4fcb-a50f-0c4aed394b0b
keywords:
- WDF Verifier コントロール アプリケーション WDK の機能
- WDF Verifier WDK
- ツールを WDK、ドライバーの検証
- ドライバー WDK WDF のテスト
- ドライバー WDK WDF のデバッグ
- ドライバー WDK WDF の確認
- WDK KMDF の検証ツール
- WDK UMDF の検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4ba2fc80c9bece971089a9411954ad0728750fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380452"
---
# <a name="wdf-verifier-control-application"></a>WDF 検証ツール制御アプリケーション


Windows Driver Frameworks (WDF) Verifier コントロール アプリケーション (WdfVerifier.exe) は、カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) ドライバーをデバッグするためのツールです。 デバッガーの設定を変更するコンピューターで、ドライバーの簡易評価用ツールを使用することができます。

このドキュメントでは、Windows Driver Kit (WDK) 8.1 の一部として同梱されているアプリケーションのバージョンで見つかったオプションについて説明します。

**重要な**WDF Verifier を使用するには、コンピューターで管理者特権が必要です。

 

### <a name="span-idwdfverifierfeaturesspanspan-idwdfverifierfeaturesspanwhat-can-i-do-with-it"></a><span id="wdf_verifier_features"></span><span id="WDF_VERIFIER_FEATURES"></span>それには、どうすればでしょうか。

-   コンピューターにすべての WDF ドライバーに関する概要情報を取得します。 ドライバーによって、またはデバイスでは、一覧を整理できます。
-   WDF のドライバーをデバッグするためには、レジストリ設定を管理します。
-   UMDF ドライバーのホスト プロセスと、ホスト ドライバーを表示します。
-   診断出力を管理します。
-   手動または自動で、ユーザー モードのデバッグ セッションを開始します。

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
<td align="left"><p><a href="wdf-drivers-tab.md" data-raw-source="[WDF Drivers Tab](wdf-drivers-tab.md)">WDF ドライバー タブ</a></p></td>
<td align="left"><p>このトピックでは、WDF Verifier のについて詳細な情報を提供します。 <strong>WDF ドライバー</strong>ページ。 このページには、コンピューター上のすべての WDF ドライバーが一覧表示し、検証の設定と、それらを使用するデバイスの設定を変更することができます。 特定のドライバーに関心がある場合は、ここからを開始します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="devices-using-wdf-tab.md" data-raw-source="[Devices Using WDF Tab](devices-using-wdf-tab.md)">WDF タブを使用してデバイス</a></p></td>
<td align="left"><p>このトピックで説明 WDF Verifier の<strong>WDF を使用してデバイス</strong>ページ。 このページには、WDF のドライバーを使用しているすべてのデバイスが一覧表示されます。 デバイスを選択すると、強調表示されているデバイスの WDF ドライバー スタックを参照してください。 この画面からの検証の設定を変更することもできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="global-wdf-settings-tab.md" data-raw-source="[Global WDF Settings Tab](global-wdf-settings-tab.md)">WDF のグローバル設定 タブ</a></p></td>
<td align="left"><p>このトピックでは、WDF Verifier のについて詳細な情報を提供します。 <strong>WDF のグローバル設定</strong>ページ。 このページは、グローバル (システム全体) WDF の検証のオプションを表示し、UMDF ドライバーがホストされているホスト プロセスを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="umdf-settings-test-use-only-tab.md" data-raw-source="[UMDF Settings (Test Use Only) Tab](umdf-settings-test-use-only-tab.md)">UMDF 設定 (テスト使用のみ) タブ</a></p></td>
<td align="left"><p>このトピックについて詳しく説明 WDF Verifier の<strong>UMDF 設定 (テスト使用のみ)</strong>ページ。 このページで、1 つまたは複数の UMDF ドライバーとシステム全体をテストするのに役立つ設定を変更できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="my-preferences-tab.md" data-raw-source="[My Preferences Tab](my-preferences-tab.md)">[基本設定] タブ</a></p></td>
<td align="left"><p>このトピックで説明 WDF Verifier の<strong>個人設定</strong>ページ。 このページで、パネルの機能のコントロールのいくつかの基本設定を設定できます。</p></td>
</tr>
</tbody>
</table>

 

 

 





