---
Description: MUTT デバイスを使用する前に、テスト システムを準備する必要があります。
title: MUTT テスト ツール実行のためのテスト システムの準備方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e7c60595a621275c95fa98fc9d448e0a2f5e116
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379941"
---
# <a name="how-to-prepare-the-test-system-to-run-mutt-test-tools"></a>MUTT テスト ツール実行のためのテスト システムの準備方法


MUTT デバイスを使用する前に、テスト システムを準備する必要があります。

## <a name="prerequisites"></a>前提条件


このドキュメントの手順は、次の仮定に基づいています。

-   Windows コマンド シェルの理解があります。 テスト ツールのインストールには、管理者特権でコマンド ウィンドウが必要です。 そのウィンドウのコマンド プロンプト ウィンドウを開きを使用して、**管理者として実行**オプション。
-   Windows Driver Kit (WDK) に含まれているツールに慣れています。
-   カーネル デバッグ ツールに慣れています。

**注**  MUTT、MUTTPack、SuperMUTT および SuperMUTT パックにこの設定が適用されます。 これらのデバイスの詳細については、次を参照してください。 [MUTT デバイス](microsoft-usb-test-tool--mutt--devices.md)します。

 

## <a name="instructions"></a>手順


**MUTT USB ハードウェアをテストするためのテスト ツールを実行するシステムを準備するには**

1.  カーネル デバッガーには、テスト システムを接続します。

    詳細については、次を参照してください。[ダウンロードとデバッグ ツールの Windows にインストール](https://go.microsoft.com/fwlink/p/?linkid=236405)と[Windows デバッグ](https://go.microsoft.com/fwlink/p/?linkid=242503)します。

2.  ホスト コント ローラーまたはテスト ハブの使用可能な各ポートには、MUTT デバイスを接続します。

    MUTT ソフトウェア パッケージがインストールされているインストール スクリプトを実行する前に、MUTT デバイスをテスト システムにアタッチする必要があります。

    推奨されるテスト構成については、このドキュメントで MUTT トポロジを参照してください。

3.  テスト システムで管理者特権のコマンド ウィンドウを開くし、テスト ツールのコピー先のフォルダーに移動します。
4.  管理者特権でコマンド ウィンドウで、必要な MUTT ドライバーをインストール**c:\\モジュールとしても\\pnputil – i – a usbfx2.inf**

    Driver verifier を使用してテストするかどうかは、実行することができます**install.cmd**前のコマンドではなく。 これは、必要なドライバーをインストールするだけでなくドライバーの検証ツールを構成します。 使用して**install.cmd**は省略可能です。

5.  テスト ドライバーをインストールするときに、次のダイアログ ボックスが表示されます。

    ![windows セキュリティ ダイアログ](images/fig9-winsec.png)

    確認 **"Microsoft Corporation"からのソフトウェアを常に信頼** ダイアログ ボックスをテストの実行が表示されないようにします。

    テスト システムのコンピューターが再起動した後**install.cmd**インストールが完了します。

6.  新しいドライバーに、MUTT を切り替える**c:\\モジュールとしても\\MuttUtil – UpdateDriver usbfx2.inf**
7.  MUTT と最新のファームウェア更新**c:\\モジュールとしても\\MuttUtil.exe UpdateFirmware**
8.  テスト システムで Windows 8 が実行されている場合は、テストを開始する前に、ホスト コント ローラーの簡単な検証を実行することをお勧めします。

    管理者特権のコマンド プロンプト ウィンドウから、ホスト コント ローラーと、システムに接続されているハブに関する情報を収集するには、次のコマンドを実行します。**C:\\モジュールとしても\\xhciwmi-確認**します。

    ツールは、コマンド ウィンドウで、ホスト コント ローラーに関する情報を表示します。 ベンダー ID、デバイス ID、リビジョンの ID、およびファームウェアのバージョン情報が含まれます。 問題があるテスト対象のホスト コント ローラーがわかっている場合は、ファームウェアの更新を検討してください。

### <a name="tracing-and-logging-events-in-the-usb-driver-stack"></a>トレースと USB ドライバー スタックでイベントをログ記録

移動して https://aka.ms/usbtrace手順については、USB ドライバーからの ETW トレースをキャプチャするためのスクリプトをダウンロードします。

## <a name="related-topics"></a>関連トピック
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



