---
title: MITT の概要
description: MITT テストを実行するには、MITT ファームウェアを新しい MITT ボードにインストールする必要があります。 次の手順では、MITT ファームウェアを更新し、MITT テストを実行するホストコンピューターを準備する方法について説明します。
ms.assetid: 4467B82F-7B06-430B-A0CB-A6825045E5F4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaa37caf6105eba71932a17851d2a67b1d856c2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845245"
---
# <a name="get-started-with-mitt"></a>MITT の概要


**最終更新日**

-   2015年1月

**適用対象:**

-   Windows 8.1

MITT テストを実行するには、MITT ファームウェアを新しい MITT ボードにインストールする必要があります。 次の手順では、MITT ファームウェアを更新し、MITT テストを実行するホストコンピューターを準備する方法について説明します。

## <a name="before-you-begin"></a>開始する前に...


-   [MITT ソフトウェアパッケージをダウンロード](https://docs.microsoft.com/previous-versions/dn919810(v=vs.85))します。
-   [MITT を使用するためのハードウェアの購入](https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--)
-   管理者特権で Windows コマンドシェルを実行する方法について説明します。 テストツールをインストールするには、管理者特権のコマンドウィンドウが必要です。 このウィンドウでは、 **[管理者として実行]** オプションを使用してコマンドプロンプトウィンドウを開くことができます。

## <a name="computer-setup-for-running-mitt-tests"></a>MITT テストを実行するためのコンピューターのセットアップ


MITT テストを実行するには、ホストとして実行されるコンピューターと、テスト対象のシステム (SUT) が必要です。

-   コンピューターで Windows 8.1 バージョンのオペレーティングシステムが実行されている必要があります。
-   コンピューターには、MITT ソフトウェアパッケージがインストールされている必要があります。
-   コンピューターは、別のコンピューターで実行されているカーネルデバッガーのターゲットとして接続されている必要があります。 Windbg を取得する方法の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。
    **  Windbg**は、スタンドアロンのツールセットとしてインストールできます。

     

-   ![windows phone に適用されます](images/Phone.png)

**注意**  SUT が電話の場合は、この図に示すように、ホストコンピューター、SUT、MITT board を構成する必要があります。

![mitt コンピューターのセットアップ](images/mitt-computer-setup.jpg)

## <a name="install-wdtf-runtime-library"></a>WDTF Runtime Library のインストール


MITT テストを実行するには、Windows Driver Test Framework (WDTF) が必要です。 Windows Driver Kit (WDK) をインストールすると、ランタイムが自動的にインストールされます。 完全なインストール手順については、「 [Wdtf Runtime Library](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」に記載されている手順に従ってください。

**ダウンロード場所**: [WDK および WinDbg ダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=733614)

ランタイムはここ% ProgramFiles (x86)%\\Windows Kit\\8.1\\テスト\\ランタイム\\TAEF にインストールされています

テスト対象のシステムがカーネルデバッガーに接続されている必要があります。 デバッグツールは、WDK と共にインストールされます。 詳細については、「 [windows 用デバッグツール (WinDbg、KD、CDB、NTSD)](https://docs.microsoft.com/windows-hardware/drivers/debugger/index) 」および「 [windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbols)」を参照してください。

## <a name="install-mitt-firmware"></a>MITT ファームウェアのインストール


1.  MITT ボードをホストコンピューターの USB 2.0 ポートに接続します。 ルートハブポートを使用し、ハブが埋め込まれているコントローラーを使用しないことをお勧めします。
2.  (オーディオジャックの横にある) ボード電源スイッチがオンになっていることを確認します。 赤い電源 LED が点灯しているはずです。
3.  デバイスマネージャーで、デバイスノードを見つけます。

    ![mitt のデバイスノード](images/install-mitt.png)

4.  ノードを右クリックし、 **[ドライバーソフトウェアの更新...]** を選択します。
5.  **[ドライバーソフトウェアの更新]** ダイアログで **[コンピューターをドライバーソフトウェア用に参照する]** を選択します。
6.  **[コンピューターのデバイスドライバーの一覧から選択できるようにする]** を選択します。
7.  **[すべてのデバイスを表示]** を選択し、 **[下の一覧からデバイスの種類を選択]** してください ページで **[次へ]** をクリックします。
8.  **[このハードウェアにインストールするデバイスドライバーを選択]** してください ページで、 **[ディスク使用...]** をクリックします。
9.  [**ディスクからインストール] ダイアログ**で、MITT インストールディレクトリ (program FILES\\MITT\\ *&lt;architecture&gt;* または program files (x86)\\MITT\\ *&lt;architecture&gt;* ) を参照し、 **[Ok]** をクリックします。
10. **[製造元]** で、 **[Microsoft]** を選択します。 **[モデル]** で、一覧から **[USB MUTT の既定値]** を選択し、 **[次へ]** をクリックします。
11. **[はい]** をクリックしてドライバーをインストールします。 ドライバーに関する警告を無視すると、ハードウェアと互換性がある可能性があります。 最後のページを閉じます。
12. プログラムファイル\\MITT\\ *&lt;アーキテクチャ&gt;* のコマンドプロンプトで、次のコマンドを実行します。

    **MuttUtil-List**

    ![mitt ファームウェアのアップグレード](images/mitt-setup1.png)

    上記の出力は、WinUSB がボードのデバイスドライバーとして読み込まれたことを示しています。

13. MITT ボードには、ファームウェアを必要とする2つの異なるチップがあります。 このタスクでは、 [MuttUtil](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)を使用します。 次のコマンドを実行します。

    **MuttUtil – UpdateFirmware**

    FPGA 開発ボードを使用している場合、プログラムの作成には最大5分かかることがあります。 MuttUtil は、ボード上のファームウェアのバージョンと MuttUtil 内に含まれるファームウェアのバージョンを比較します。 ファームウェアは、MuttUtil に新しいファームウェアがある場合にのみ更新されます。

    ![mitt ファームウェアのアップグレード](images/mitt-setup2.png)

    上記の出力は、最初のファームウェアイメージが正常にインストールされたことを示しています。

14. 最初のファームウェアの更新が完了した後、2番目のチップに対して**MuttUtil – UpdateFirmware**をもう一度実行します。 2番目のチップのファームウェアは、最初のチップがインストールされるまで更新できません。

    ![mitt ファームウェアのアップグレード](images/mitt-setup3.png)

    上記の出力は、2番目の MITT ファームウェアイメージが正常にインストールされたことを示しています。 MITT ボードの7つのセグメントに注目してください。 000X を確認する必要があります。 X は MITT ファームウェアの現在のバージョンです。

**Updatefirmware**オプション  MITT ボードにインストールされているファクトリファームウェアイメージを復元できないことに**注意**してください。

 

ファームウェアの更新中またはインストール中に MuttUtil からエラーが返された場合は、

-   MITT ボードの電源スイッチがオンになっているかどうかを確認します。 ボードの電源が入っている場合は、プラグを抜いてボードから USB ケーブルを接続し、コマンドをもう一度実行します。
-   コマンドが成功しても、7セグメントにファームウェアのバージョンが表示されない場合は、リセットボタンを押すか、USB ケーブルと電源ケーブルを取り外してプラグを抜いて、MITT ボードを再起動します。 7つのセグメントに引き続きバージョンが表示されない場合は、コマンドをもう一度実行します。

## <a name="known-issues-and-workaround"></a>既知の問題と回避策


-   MITT をホストコンピューターの xHCI ルートハブに直接接続することはお勧めできません。 テストは、そのセットアップでランダムにハングすることがあります。 回避策として、xHCI port と MITT board の間に、電源が入っている USB 2.0 ハブを追加します。

## <a name="related-topics"></a>関連トピック
[マルチインターフェイステストツール (MITT) を使用したテスト](https://docs.microsoft.com/windows-hardware/drivers/spb/testing-with-multi-interface-test-tool--mitt-)  



