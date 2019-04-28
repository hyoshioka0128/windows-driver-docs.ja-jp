---
title: WDF ドライバー呼び出しトレーサー (WdfCallTracer)
description: WDF ドライバー呼び出しトレーサー (WdfCallTracer)
ms.assetid: 67ad4b5e-9117-435e-bd81-90069a806d3c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 379c8665120c5b94e0935a7ff6ab35cf7c2e2cfc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380458"
---
# <a name="wdf-driver-call-tracer-wdfcalltracer"></a>WDF ドライバー呼び出しトレーサー (WdfCallTracer)


WdfCallTracer を使用して、リアルタイムでのフレームワークとドライバーの通信をトレースおよび表示することができます。 WdfCallTracer は、機能の独立した実行可能ファイルではありません (この個別のバイナリはありません)。 名です。

この機能を使用して、DDI を表示できます。 リアルタイムでイベントを呼び出します。

次の手順は、する方法を示します KMDF 静的バス ドライバー サンプル (Statbus.sys WDK で使用可能な) ドライバーの通信を使用して、WdfTester を構成します。 現在のみ DDI 呼び出しを表示できます。

**WDF ドライバー呼び出しのトレースを設定し、ドライバーのサンプルをビルドするには**

1.  インストール[WdfTester インストール](wdftester-installation.md)します。

2.  KMDF 静的バス ドライバー サンプル (Statbus.sys) をビルドします。 KMDF サンプルが記載されています、 *%wdkroot*\\src\\全般\\トースター\\toastDrv\\kmdf\\bus\\静的ディレクトリ。

3.  バス ドライバーのサンプルをインストールした WdfTester ファイルを含むディレクトリにコピーします。 KMDF トースター サンプルの手順に従って、ドライバーを読み込みます。 使用[DevCon](devcon.md) (Devcon.exe) または**ハードウェアの追加ウィザード**します。

次の手順を使用して、DDI を表示して、リアルタイムでイベントを呼び出すように traceview でを構成するには

**Traceview で新しいログ セッションを作成するには**

1.  TraceView.exe を開始 (*%wdkroot*\\ツール\\*&lt;プラットフォーム&gt;*)。

2.  **ファイル** メニューのをクリックして**Create New Log Session**します。

3.  **Create New Log Session**ダイアログ ボックスで、をクリックして**プロバイダーの追加**します。

4.  **プロバイダー コントロールの GUID セットアップ**ダイアログ ボックスで、をクリックして**CTL (コントロールの GUID) ファイル**します。

5.  をクリックして、**参照**ボタンをクリックし、WdfTester ファイルおよびドライバーを含むディレクトリから Wdftester.ctl ファイルを選択します。

6.  **[OK]** をクリックします。

7.  **形式情報ソースを選択します**ダイアログ ボックスで、をクリックして**TMF ファイルの選択**、 をクリック**ok**します。

8.  **トレース形式情報セットアップ**ダイアログ ボックスで、 をクリックして**追加、** WdfTester ファイルが配置されるディレクトリを参照します。

9.  Wdftester.tmf をクリックし**オープン**ファイルを選択してクリックして**完了**します。

10. をクリックして **[次へ]** で、 **Create New Log Session**クリックしてダイアログ ボックスで、**完了**。

ドライバーを登録し、ドライバーの通信を表示できるように、トレースを有効にする準備が整いました。

**KMDF ドライバーを登録し、トレースを有効にするには**

1.  コマンド プロンプト ウィンドウを開き、Wdftester ファイルがインストールされているディレクトリに変更します。

2.  (この例では、Statbus.sys) では、KMDF ドライバーを WdftesterScript.wsf スクリプトを使用して登録します。
    ```
    cscript WdftesterScript.wsf register statbus.sys
    ```

3.  デバイス マネージャーから、ドライバーを有効または、ハードウェアを接続します。 ドライバーが既に有効になっている場合は、デバイス マネージャーを使用して無効にしとし、再度有効にします。

Traceview でアプリケーションの通信をドライバーが表示されます。

 

 





