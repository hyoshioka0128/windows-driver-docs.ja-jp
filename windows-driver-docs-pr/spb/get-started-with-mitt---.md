---
title: MITT の概要
description: ミット テストを実行するには、新しいミット掲示板にミット ファームウェアをインストールする必要があります。 次の手順では、ミット ファームウェアを更新およびミット テストの実行用のホスト コンピューターを準備する方法について説明します。
ms.assetid: 4467B82F-7B06-430B-A0CB-A6825045E5F4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe48e730bb5c8a7bae4c7eaa9126b3019cd4eaae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373790"
---
# <a name="get-started-with-mitt"></a>MITT の概要


**最終更新日**

-   2015 年 1 月

**適用対象:**

-   Windows 8.1

ミット テストを実行するには、新しいミット掲示板にミット ファームウェアをインストールする必要があります。 次の手順では、ミット ファームウェアを更新およびミット テストの実行用のホスト コンピューターを準備する方法について説明します。

## <a name="before-you-begin"></a>開始する前にしています.


-   [ミット ソフトウェア パッケージをダウンロード](https://docs.microsoft.com/previous-versions/dn919810(v=vs.85))します。
-   [ミットを使用するためのハードウェアを購入します。](https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--)
-   昇格された特権で Windows コマンド シェルを実行する方法を理解します。 テスト ツールのインストールには、管理者特権でコマンド ウィンドウが必要です。 そのウィンドウのコマンド プロンプト ウィンドウを開きを使用して、**管理者として実行**オプション。

## <a name="computer-setup-for-running-mitt-tests"></a>ミット テストを実行するためのコンピューターの設定


ミット テストを実行するには、ホストおよびテスト (SUT) 対象のシステムを実行するコンピューターが必要です。

-   コンピューターには、Windows 8.1 のバージョンのオペレーティング システムを実行する必要があります。
-   コンピューターには、ミット ソフトウェア パッケージがインストールされている必要があります。
-   別のコンピューターで実行されているカーネル デバッガーをターゲットとして、コンピューターを接続する必要があります。 Windbg を取得する方法の詳細については、次を参照してください。 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)します。
    **注**  Windbg をスタンドアロン ツールのセットとしてインストールできます。

     

-   ![windows phone に適用されます。](images/Phone.png)

**注**  かどうか、SUT がスマート フォンで、ホスト コンピューター、SUT とミット ボードは、この図のように構成する必要があります。

![ミット コンピューターのセットアップ](images/mitt-computer-setup.jpg)

## <a name="install-wdtf-runtime-library"></a>WDTF ランタイム ライブラリをインストールします。


ミット テストを実行するには、Windows ドライバー テスト フレームワーク (WDTF) する必要があります。 Windows Driver Kit (WDK) をインストールするときに、ランタイムが自動的にインストールされていることにします。 完全なインストール手順については、記載された手順に従います[WDTF ランタイム ライブラリ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

**ダウンロード場所**:[WDK と WinDbg のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=733614)

ランタイムがインストールされているここでは %programfiles (x86) %\\Windows キット\\8.1\\テスト\\ランタイム\\TAEF

テスト対象のシステムは、カーネル デバッガーに接続する必要があります。 デバッグ ツールは、WDK と共にインストールされます。 詳細については、次を参照してください。[デバッグ ツールの Windows (WinDbg、KD、CDB、NTSD)](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)と[Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbols)します。

## <a name="install-mitt-firmware"></a>ミット ファームウェアをインストールします。


1.  ミット ボードは、ホスト コンピューター上の USB 2.0 ポートに接続します。 ルート ハブのポートを使用してコント ローラー埋め込み hubs の使用を避けることをお勧めします。
2.  (オーディオ ジャック) 横にあるボードの電源スイッチが有効であることを確認します。 赤いに電源 LED があります。
3.  デバイス マネージャーでは、[デバイス] ノードを探します。

    ![ミットのデバイス ノード](images/install-mitt.png)

4.  ノードを右クリックし、選択**ドライバー ソフトウェアの更新しています.** .
5.  選択**参照コンピューターでドライバー ソフトウェア**で、**ドライバー ソフトウェアの更新**ダイアログ。
6.  選択**コンピューター上のデバイス ドライバーの一覧から選択できるように**します。
7.  選択**すべてのデバイスを表示** をクリック**次**で、**以下の一覧からデバイスの種類を選択**ページ。
8.  をクリックして**ディスクがある.** 上、**このハードウェアをインストールするデバイス ドライバーを選択**ページ。
9.  ミット インストール ディレクトリに移動 (Program Files\\ミット\\ *&lt;アーキテクチャ&gt;* または Program Files (x86)\\ミット\\ *&lt;アーキテクチャ&gt;* ) で、**ディスクからインストール ダイアログ ボックス**クリック**Ok**。
10. **製造元**選択**Microsoft**します。 [**モデル**選択**USB MUTT 既定**] をクリックし、リストから**次**。
11. クリックして**はい**ドライバーをインストールするとします。 無視ドライバーに関する警告は、ハードウェアと互換性のある可能性があります。 最後のページを閉じます。
12. プログラム ファイルからコマンド プロンプトで\\ミット\\ *&lt;アーキテクチャ&gt;* 、このコマンドを実行します。

    **MuttUtil.exe -List**

    ![ミット ファームウェアのアップグレード](images/mitt-setup1.png)

    ボードのデバイス ドライバーとして、WinUSB が読み込まれている上記の出力を示しています。

13. ミット ボードにファームウェアを必要とする 2 つの個別チップがあります。 このタスクで使用[MuttUtil](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)します。 次のコマンドを実行します。

    **MuttUtil.exe – UpdateFirmware**

    FPGA 開発ボードを使用している場合、EEPROM にプログラムには、最大 5 分はかかります。 MuttUtil は、MuttUtil 内に含まれているファームウェアのバージョンでボードにファームウェアのバージョンを比較します。 MuttUtil に新しいファームウェアがある場合にのみ、ファームウェアが更新されます。

    ![ミット ファームウェアのアップグレード](images/mitt-setup2.png)

    上記の出力は、最初のファームウェア イメージのインストールが成功を示しています。

14. 実行**MuttUtil.exe – UpdateFirmware**最初のファームウェアの更新が完了した後、2 つ目のチップをもう一度です。 最初のチップがインストールされるまで、2 つ目のチップのファームウェアを更新することはできません。

    ![ミット ファームウェアのアップグレード](images/mitt-setup3.png)

    上記の出力は、2 つ目のミット ファームウェア イメージのインストールが成功を示しています。 ミット ボードの 7 つのセグメントに注意してください。 X は現在のバージョンのミット ファームウェア 000 X を確認する必要があります。

**注**  、 **UpdateFirmware**オプション ミット掲示板にインストールされているファクトリ ファームウェア イメージを復元することはできません。

 

MuttUtil 更新またはファームウェアのインストール中にエラーが返されます場合

-   ミット ボードの電源スイッチがオンかどうかを確認します。 ボードを活用すると場合、取り外すと USB ケーブルをボードからとコマンドを再度実行します。
-   コマンドの成功、7 つのセグメントがファームウェアのバージョンを表示しない場合は、ミット ボードを再起動するには、リセット ボタンを押してまたはプラグを抜くと、USB 接続ケーブルと電源ケーブル。 7 つのセグメントが表示されない場合、バージョン、再度コマンドを実行します。

## <a name="known-issues-and-workaround"></a>既知の問題と回避策


-   ホスト コンピューター上の xHCI ルート ハブに直接ミットを接続することは推奨されません。 テストは、そのセットアップをランダムにぶら下げることができます。 この問題を回避するには、xHCI ポートとミット ボード電源の USB 2.0 ハブを追加します。

## <a name="related-topics"></a>関連トピック
[複数のインターフェイスのテスト ツール (ミット) でのテスト](https://docs.microsoft.com/windows-hardware/drivers/spb/testing-with-multi-interface-test-tool--mitt-)  



