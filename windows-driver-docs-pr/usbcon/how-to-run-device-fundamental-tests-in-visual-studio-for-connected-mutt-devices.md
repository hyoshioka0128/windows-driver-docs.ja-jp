---
Description: 使用可能なポートに接続された MUTT デバイスの実行が必要なデバイスの基本的なテストについて説明します。
title: Visual Studio で MUTT デバイスのシステム電源 devfund テストを実行します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61c9c14b4dbea00de855e89135593836ba81f385
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366052"
---
# <a name="how-to-run-system-power-devfund-tests-in-visual-studio-for-mutt-devices"></a>Visual Studio での MUTT デバイスのシステム電源 devfund テストの実行方法


MUTT デバイスで利用できるポートに関連付けられている実行が必要なデバイスの基本的なテストについて説明しますストレスおよび転送テストおよびシステム電源のテストを実行します。

これらのテストは、システム電源イベントを実行すると同時に、シンプルなデバイスの転送を実行します。 Devfund テストは Windows 8 でのみ実行できますに注意してください。 ことはできません[ストレスを実行し、テストに転送](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)およびシステムの電源が同時にテストします。 別のシステムには、これらのテストを実行します。 ただし、ストレスの転送とシステム間で切り替えることができますの電源をテストします。 これを行うに最初の一連のテストの完了や、コンピューターを再起動し、次のテストの指示に従います。

## <a name="how-to-run-device-fundamental-devfund-tests-in-visual-studio-for-connected-mutt-devices"></a>Visual Studio で接続された MUTT デバイスのデバイス基本 (devfund) のテストを実行する方法


Devfund テストは、ドライバーとハードウェアのテストに使用するテストのコレクションです。 これらのテストは、Windows 8 の WDK に含まれています。 Microsoft Visual Studio Professional 2012 RC に WDK を追加で実行でき、開発環境からこれらのテストを実行することができます。

### <a name="prerequisites"></a>前提条件

Devfund テストの実行を開始する前に、次の要件を満たしていることを確認します。

-   これらのテストを実行するには、コンピューター 2 台以上必要があります。 ホストおよびテストします。 ホストを構成し、テストとデバッグ用のコンピューターをテストします。

    -   Windows 8 の Microsoft Visual Studio Professional 2012 と Windows Driver Kit (WDK) をインストールする必要があります。
    -   テスト コンピューターには、Windows 8 の最新バージョンを実行する必要があります。

    Visual Studio と WDK からダウンロードできます[Windows ハードウェア開発のダウンロード](https://go.microsoft.com/fwlink/p/?linkid=309780)します。

    構成に関する手順については、次を参照してください。[ドライバーの展開、テスト、およびデバッグ用コンピューターの構成](https://go.microsoft.com/fwlink/p/?linkid=235504)します。

-   テスト コンピューターに、ホスト コンピューターを接続する前にするテスト コンピューターでファイルとプリンタの共有とネットワーク探索を有効にする必要があります。 コントロール パネル、または管理者特権でコマンド プロンプトで次のコマンドを使用して、これらのオプションを有効にできます。

    `netsh.exe advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes`

-   設定して、MUTT デバイスを構成し、ファームウェアをインストールします。 詳細については、次を参照してください。[テスト システムを準備する方法](mutt-testing-options.md)します。
-   テスト コンピューターをプロビジョニングします。 手順については、次を参照してください。[ドライバーの展開、テスト、およびデバッグ用コンピューターの構成](https://go.microsoft.com/fwlink/p/?linkid=235504)します。

### <a name="scheduling-tests"></a>テストのスケジュール設定

1.  テスト コンピューターで実行するテストを選択します。 手順については、次を参照してください。**手順 2。テスト コンピューターで実行するテストを選択**で[Visual Studio を使用して実行時にドライバーをテストする方法](https://go.microsoft.com/fwlink/p/?linkid=290770)します。
2.  次の図のように、次のランタイム パラメーターを設定します。

    -   DQ:クラス 'モジュールとしても' を =
    -   TestCycles:100

    ![visual studio テスト グループ](images/fig11-vs-testgroup.png)

3.  テスト パラメーターを構成します。 構成の詳細については、次を参照してください。**手順 3。テスト パラメーターの構成**で[Visual Studio を使用して実行時にドライバーをテストする方法](https://go.microsoft.com/fwlink/p/?linkid=290770)します。
4.  テストを実行します。 テストの実行については、次を参照してください。**手順 5。テスト コンピューターでテストを実行**で[Visual Studio を使用して実行時にドライバーをテストする方法](https://go.microsoft.com/fwlink/p/?linkid=290770)します。

### <a name="recommended-tests-to-schedule-with-the-connected-mutt-device"></a>接続された MUTT デバイスを使用してスケジュールするためのテストをお勧めします。

-   前後に IO をスリープ状態します。
-   (Basic) の中に IO をスリープ状態します。
-   PNP (無効および有効にする) と後で IO の前に

上記のテストの詳細については、次を参照してください。**について、基本的なデバイス テスト**で[を選択し、デバイスの基本的なテストを構成する方法](https://go.microsoft.com/fwlink/p/?linkid=316387)します。

## <a name="related-topics"></a>関連トピック
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



