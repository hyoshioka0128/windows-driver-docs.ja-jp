---
Description: このトピックでは、パーサー Netmon と USB ETW に関するインストール情報を示します。
title: Netmon と USB ETW パーサーのインストール方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a7f62cf203e6e0071db1c03d6e93924b4469876
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364796"
---
# <a name="how-to-install-netmon-and-usb-etw-parsers"></a>Netmon と USB ETW パーサーのインストール方法

このトピックでは、パーサー Netmon と USB ETW に関するインストール情報を示します。

Netmon、Microsoft ダウンロード センターからインストールしてからインストールから USB ETW パーサー [Windows Driver Kit (WDK)](https://msdn.microsoft.com/windows/hardware/hh852362.aspx)します。 Netmon バージョン 3.3 以降では、USB ETW パーサーがサポートされています。

## <a name="to-install-the-netmon-tool-and-the-netmon-usb-parser"></a>Netmon ツールと Netmon USB パーサーをインストールするには

1. コンピューターで Windows の 32 ビットまたは 64 ビット Windows を実行しているかどうかを決定します。

    1. 開く、**開始** メニューを右クリックして**コンピューター**とビュー**プロパティ**。
    2. 見て、**システム型**フィールド。

    X86 を使用する場合は、システムの種類は 32 ビットのオペレーティング システムをダウンロードします。 システムの種類が 64 ビット オペレーティング システム、プロセッサが Itanium の場合は、ia64 のダウンロードを使用します。 その他のプロセッサの種類、x64、または AMD64 ダウンロードを使用します。

2. ネットワーク モニターをインストールします。
    1. [Windows ネットワーク モニター](https://go.microsoft.com/fwlink/p/?linkid=103158) Microsoft ダウンロード センター ページし、ツールの説明を読みます。
    2. **でこのダウンロード ファイル**、ページの下部のセクションで、、**ダウンロード**システムの種類のボタンをクリックします。
    3. ダウンロードして、セットアップ ウィザードを起動する .exe ファイルを実行します。
    4. 選択**標準**とセットアップの種類の選択を求められます。

3. WDK をインストール[Windows Driver Kit 8](https://msdn.microsoft.com/windows/hardware/hh852362.aspx)します。
4. PowerShell スクリプトの実行を許可します。
    1. [Start] 画面で、"powershell"の入力、Windows PowerShell 結果を右クリックし、選択**管理者として実行**します。
    2. PowerShell ウィンドウで、このコマンドを入力します。

        ```syntax
        Set-ExecutionPolicy RemoteSigned -Force
        ```

    3. PowerShell ウィンドウを閉じます。
    4. PowerShell ウィンドウを開きます (する必要はありません**管理者として実行**) し、次のコマンドを実行します。 別の場所に、キットがインストールされている場合は、パスを調整します。

        ```syntax
        cd "C:\Program Files (x86)\Windows Kits\8.0\Tools\x86\Network Monitor Parsers\usb"
        ..\NplAutoProfile.ps1
        ```

    5. 変更を適用する Netmon を再起動します。

5. プロファイルが Netmon でアクティブであることを確認します。
    1. **ツール**メニューの **オプション**します。
    2. **パーサー プロファイル** タブで、ことを確認します **(生成) 自動プロファイル**がアクティブに設定します。 設定は、このイメージのようになります。

        ![自動プロファイル パーサーのプロファイル タブのスクリーン ショットは、アクティブとして設定](images/netmon-parsers1.png)

    3. **[OK]** をクリックします。

Netmon が USB ETW トレース ファイルを使用するために構成されました。 詳細については、次を参照してください。 [Netmon で USB の ETW トレースを表示する方法](how-to-examining-a-trace-file-by-using-netmon.md)します。

## <a name="related-topics"></a>関連トピック

[USB の ETW を使用してください。](using-usb-etw.md)  
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  
[Netmon で ETW トレースを開く方法](how-to-examining-a-trace-file-by-using-netmon.md)  
