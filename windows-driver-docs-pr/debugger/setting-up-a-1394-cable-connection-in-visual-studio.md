---
title: Visual Studio での 1394 ケーブル経由でのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用すると、1394 (Firewire) ケーブルでカーネルモードのデバッグを設定して実行できます。
ms.assetid: 07784500-83F1-4927-998F-7CEEEADAA2B0
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0fc1d0e17e9834db3a47bd1ff64fc57b664dc60a
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534771"
---
# <a name="setting-up-kernel-mode-debugging-over-a-1394-cable-in-visual-studio"></a>Visual Studio での 1394 ケーブル経由でのカーネルモード デバッグの設定


> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>

Microsoft Visual Studio を使用すると、1394 (Firewire) ケーブルでカーネルモードのデバッグを設定して実行できます。 Visual Studio を使用してカーネルモードのデバッグを行うには、Visual Studio に Windows Driver Kit (WDK) が統合されている必要があります。 統合環境をインストールする方法の詳細については、「 [Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)」を参照してください。

Visual Studio を使用して1394デバッグを設定する代わりに、手動でセットアップを行うこともできます。 詳細については、「 [1394 ケーブル経由でカーネルモードのデバッグを手動で設定する](setting-up-a-1394-cable-connection.md)」を参照してください。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ対象のコンピューターは*ターゲットコンピューター*と呼ばれます。 ホストとターゲットのコンピューターには、それぞれ1394アダプターが必要です。

## <a name="span-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>ホストとターゲットコンピューターの構成


1.  ホストとターゲットコンピュータでデバッグ用に選択した1394コントローラに1394ケーブルを接続します。
2.  「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の説明に従って、ホストとターゲットコンピューターの構成を開始します。
3.  ホストコンピューターの Visual Studio で、[コンピューターの構成] ダイアログボックスが表示されたら、[コンピューターのプロビジョニング] を選択し、[**デバッガーの設定**] を選択します。
4.  [**接続の種類**] で、[ **Firewire**] を選択します。

    ![[接続の種類]、[ポート番号]、[キー]、[ホスト ip]、および [バスパラメーター] の各フィールドの値を含むデバッガー設定の例を示すスクリーンショット](images/setup1394vs.png)

    [**チャンネル**] には、1 ~ 62 の10進数を入力します。

    **メモ**   最初にデバッグを設定するときは、チャネルを0に設定しないでください。 既定のチャネル値は0であるため、ソフトウェアでは変更がないと見なされ、設定は更新されません。 チャネル0を使用する必要がある場合は、まず代替チャネル (1 ~ 62) を使用し、次にチャネル0に切り替えます。

    ターゲットコンピューターに 1 1394 個を超えるコントローラーがある場合は、**バスパラメーター**値*b*を入力します。*d*。*f*( *b*、 *d*、 *f* ) は、ターゲットコンピューターでのデバッグに使用する1394コントローラーのバス、デバイス、および関数の番号です。 バス、デバイス、および関数の数値は10進数形式にする必要があります (例: 4.4.0)。

5.  構成プロセスには数分かかり、対象のコンピューターが1回または2回自動的に再起動される場合があります。 プロセスが完了したら、[**完了**] をクリックします。

## <a name="span-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>ターゲットコンピューターの dbgsettings を確認しています

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。
> セキュリティ機能が無効になっている場合は、テストが完了し、テスト PC を適切に管理するときに、これらのセキュリティ機能を再び有効にします。

ターゲットコンピューターで、管理者としてコマンドプロンプトウィンドウを開き、次のコマンドを入力します。

**bcdedit/dbgsettings**

**bcdedit/enum**

```console
...
debugtype               1394
debugport               1
baudrate                115200
channel                 1
...
busparams               4.0.0
...
```

*Debugtype*が1394で、 *channel*がホストコンピューターの Visual Studio で指定したチャネル番号であることを確認します。 *Debugport*と*ボーレート*の値は無視できます。1394でのデバッグには適用されません。

Visual Studio で**バスパラメーター**を入力した場合は、指定したバスパラメーターと*busparams*が一致していることを確認します。

**バスパラメーター**に入力した値が表示されない場合は、次のコマンドを入力します。

**bcdedit/set "{dbgsettings}" busparams** <em>b</em>**。**<em>d</em>**。**<em>f</em>

ここで、 *b*、 *d*、および*f*は、デバッグに使用するように選択したターゲットコンピューター上の1394コントローラーのバス、デバイス、および関数番号です。

次に例を示します。

**bcdedit/set "{dbgsettings}" busparams 4.4.0**

## <a name="span-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグセッションを開始する


1.  ホストコンピューターで、管理者として Visual Studio を開きます。
2.  [**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
3.  [**トランスポート**] で、[ **Windows カーネルモードデバッガー**] を選択します。
4.  [**修飾子**] で、以前に構成したターゲットコンピューターの名前を選択します。
5.  **[アタッチ]** をクリックします。

この時点で、1394デバッグドライバーがホストコンピューターにインストールされます。 このため、Visual Studio を管理者として実行することが重要です。 1394デバッグドライバーをインストールした後は、以降のデバッグセッションで管理者として実行する必要はありません。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグセッションの開始


1.  ホストコンピューターで、Visual Studio の [**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
2.  [**トランスポート**] で、[ **Windows カーネルモードデバッガー**] を選択します。
3.  [**修飾子**] で、以前に構成したターゲットコンピューターの名前を選択します。
4.  **[アタッチ]** をクリックします。

## <a name="span-idtroubleshooting_tips_for_debugging_over_a_1394_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_1394_cablespantroubleshooting-tips-for-debugging-over-a-1394-cable"></a><span id="troubleshooting_tips_for_debugging_over_a_1394_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_1394_CABLE"></span>1394ケーブルでのデバッグに関するトラブルシューティングのヒント


1394デバッグの問題のほとんどは、ホストまたはターゲットコンピューターで複数の1394コントローラーを使用した場合に発生します。 ホストコンピューターでの複数の1394コントローラーの使用はサポートされていません。 ホスト上で実行される1394デバッグドライバーは、レジストリで列挙された最初の1394コントローラーとのみ通信できます。 マザーボードに1394コントローラーを内蔵し、別の1394カードを使用している場合は、カードを取り外すか、組み込みのコントローラーを (デバイスマネージャーを使用して) 無効にします。

ターゲットコンピューターは、複数の1394コントローラーを持つことができますが、これは推奨されません。 ターゲットコンピューターのマザーボードに1394コントローラーが搭載されている場合は、可能であれば、そのコントローラーをデバッグに使用します。 1394カードが追加されている場合は、カードを取り外し、オンボードコントローラーを使用する必要があります。 もう1つの解決策は、コンピューターの BIOS 設定で、オンボード1394コントローラーを無効にすることです。

ターゲットコンピューターで複数の1394コントローラーを有効にする場合は、デバッグのために要求するコントローラーをデバッガーが認識できるように、バスパラメーターを指定する必要があります。 バスパラメーターを指定するにはデバイスマネージャーを開き、デバッグに使用する1394コントローラーを探します。 コントローラーのプロパティページを開き、バス番号、デバイス番号、および関数番号をメモしておきます。 管理者特権でのコマンドプロンプトウィンドウで、次のコマンドを入力します。ここで、 *b*、 *d*、および*f*は、10進形式のバス、デバイス、および関数の数値です。

**bcdedit/set "{dbgsettings}" busparams** <em>b</em>**。**<em>d</em>**。**<em>f</em>

ターゲット コンピューターを再起動します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグの設定](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






