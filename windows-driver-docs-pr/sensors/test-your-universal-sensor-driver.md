---
title: ユニバーサル センサー ドライバーをテストします。
description: このトピックでは、ユニバーサル センサー ドライバーをテストする方法について説明します。
ms.assetid: 46F50544-B130-4690-8047-6FBB6DD4749F
ms.date: 11/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6d0b2c481efb93022e0bd2ad75cce630f2f1b108
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558708"
---
# <a name="test-your-universal-sensor-driver"></a>ユニバーサル センサー ドライバーをテストします。

このトピックでは、ユニバーサル センサー ドライバーをテストする方法について説明します。

## <a name="sensor-driver-specific-testing"></a>センサー ドライバー固有のテスト

した後に正常に[サメ Cove 掲示板にセンサーを接続](connect-your-sensor-to-the-sharks-cove-board.md)とする[作成および配置には、ユニバーサル センサー ドライバー](write-and-deploy-your-universal-sensor-driver.md)、ユニバーサル センサーをテストおよびデバッグの次のツールを使用することができますドライバー。

-   **MALT (Microsoft Ambent 光ツール)** <br/>MALT ツールは、ソリューションをテスト信号として使用できます。 詳細については、次を参照してください。[光テスト ツールの構築](testing-MALT-building-a-light-testing-tool.md)します。

-   **SensorInfo アプリ** <br/>ユニバーサル Windows プラットフォーム (UWP) アプリのテスト センサー ドライバーを使用するかどうかを使用して、 [SensorInfo アプリ](http://apps.microsoft.com/windows/app/95015d9e-2116-44b8-9d3c-15c7b8753086?ocid=Apps_Search_WOL_en-us_search-main_search-results-from_search-sensorinfo_image_sensorinfo)します。 このアプリは任意のセンサーに接続されている (またはに埋め込まれている) を自動的に検出、プラットフォームでは、その関連するドライバーを呼び出します。 アプリが、センサーから読み取った情報が表示され、波形を移動することで情報を表示します。

-   **センサー診断ツール** <br/>単にデータの取得を監視する場合のイベント処理、レポートの間隔はサメ Cove これらセンサーの値を監視するためにこのツールをインストールします。 センサー診断ツールは、Windows driver kit (WDK) に同梱され、次のフォルダーに格納されたことができます。*&lt;キット ルート&gt;\\ツール\\&lt;アーキテクチャ&gt;\\sensordiagnostictool.exe*します。 <br/><br/>たとえば、ドライバー開発用コンピューターは x64 ベースのマシンでは、既定の場所に WDK をインストールした場合は、次のフォルダーにセンサー診断ツールが検索されます。<br/><br/>*C:\\プログラム ファイル (x86)\\Windows キット\\10\\ツール\\x64\\sensordiagnostictool.exe* <br/><br/>**注**  センサー診断ツールは Windows 10 の非推奨となりました。 Microsoft Store で、すべてのセンサーのテストと診断の SensorInfo アプリを使用してください。

## <a name="general-driver-testing"></a>一般的なドライバーのテスト

一般を参照してください、次のリソースでドライバーをテストについて確認する場合は。

-   **Visual Studio のカーネル モードを使用したデバッグ シリアル USB 経由で**
    <br/>Visual Studio のヘルプのセンサーとそのユニバーサル センサー ドライバーのデバッグ セッションを設定する場合は、このテスト/デバッグ オプションを使用します。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップ シリアルを使用して、Visual Studio での USB 経由で](https://msdn.microsoft.com/library/windows/hardware/dn745913.aspx)します。
-   **USB 経由でシリアルを使用して、カーネル モードのデバッグを手動で設定します。**
    <br/>テスト/デバッグ、ユニバーサル センサー ドライバーをセットアップを行うための Visual Studio を使用したくない場合は、このオプションを使用できます。 これを行う方法の詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動で USB シリアルを使用して](https://msdn.microsoft.com/library/windows/hardware/dn745914.aspx)します。
-   **WDK のドライバー インターフェイスをテスト**ドライバーをテストするインターフェイスのテスト、Microsoft Visual Studio を使用して Windows driver kit (WDK) ドライバーを使用することができます。 これを行う方法については、次を参照してください。[ドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver)します。

トレース プロバイダーの動作を監視する方法については、次を参照してください。[ログの収集と WPP をデコード](collecting-and-decoding-wpp-logs.md)します。








