---
title: Visual Studio での 1394 ケーブル経由でのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用して、設定し、カーネル モードの 1394 (Firewire) ケーブル経由でのデバッグを実行することができます。
ms.assetid: 07784500-83F1-4927-998F-7CEEEADAA2B0
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 65f9dfb5dff6b13fef47ba4112624d6652a4574a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366390"
---
# <a name="setting-up-kernel-mode-debugging-over-a-1394-cable-in-visual-studio"></a>Visual Studio での 1394 ケーブル経由でのカーネルモード デバッグの設定


> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

Microsoft Visual Studio を使用して、設定し、カーネル モードの 1394 (Firewire) ケーブル経由でのデバッグを実行することができます。 カーネル モードのデバッグを Visual Studio を使用するには、Windows Driver Kit (WDK) の Visual Studio と統合が必要です。 統合環境をインストールする方法については、次を参照してください。 [Windows ドライバー開発](https://go.microsoft.com/fwlink/p?linkid=301383)します。

1394 デバッグを設定する Visual Studio を使用する代わりに、セットアップを手動で行うことができます。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動での 1394 ケーブル](setting-up-a-1394-cable-connection.md)します。

デバッガーを実行しているコンピューターと呼ばれる、*ホスト コンピューター*とは、デバッグ中のコンピューターと呼びます、*対象のコンピュータ*します。 ホストおよびターゲット コンピューターが、それぞれあります 1394 アダプターであります。

## <a name="span-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>ホストおよびターゲット コンピュータの構成


1.  ホストおよびターゲット コンピューターでデバッグするため、選択した 1394 コント ローラーには、1394 ケーブルを接続します。
2.  」の説明に従って、ホストとターゲット コンピューターの構成を開始[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)します。
3.  Visual Studio で、ホスト コンピューターで、コンピューターの構成 ダイアログに表示される場合が選択**コンピューターをプロビジョニングし、デバッガーの設定を選択**します。
4.  **接続の種類**、選択**Firewire**します。

    ![スクリーン ショットのデバッガーの例を次のフィールドの値の設定を示す: 接続の種類、ポート番号、キー、ホストの ip アドレス、およびバス パラメーター](images/setup1394vs.png)

    **チャネル**、1 ~ 62 好きな 10 進数を入力します。

    **注**  最初のデバッグを設定するも 0 に、チャネルが設定しないでください。 既定のチャネルの値が 0 の場合、ソフトウェアがあると仮定するための変更はなく、設定を更新できません。 0 のチャネルを使用する必要がありますまず別のチャネル (1 ~ 62) を使用してし、し、チャネル 0 に切り替えます。

    1 つ以上ある場合、対象のコンピューターに 1394 コント ローラーの入力を**Bus パラメーター**の値*b*.*d*.*f*ここで、 *b*、 *d*、および*f*バス、デバイス、および関数の番号でデバッグするために使用する、1394 コント ローラーには、対象のコンピュータ。 バス、デバイス、および関数の番号は 10 進数形式である必要があります (例。4.4.0).

5.  構成プロセスには数分かかりますが自動的に、コンピューターを再起動ターゲットまたは 2 回。 プロセスが完了したら、クリックして**完了**します。

## <a name="span-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>ターゲット コンピューター上の dbgsettings を確認しています

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。
> テストが完了すると、これらのセキュリティ機能を再度有効にし、適切なセキュリティ機能を無効にするテスト PC を管理します。

対象のコンピューターに管理者としてコマンド プロンプト ウィンドウを開きし、このコマンドを入力します。

**bcdedit /dbgsettings**

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

いることを確認*debugtype* 1394 および*チャネル*はホスト コンピューターで Visual Studio で指定したチャネルの数です。 値は無視してかまいません*debugport*と*baudrate*; 超える 1394 デバッグには適用されません。

入力した場合**Bus パラメーター** Visual Studio であることを確認*busparams*指定したバス パラメーターと一致します。

用に入力した値が表示されない場合**Bus パラメーター**、このコマンドを入力します。

**bcdedit /set "{dbgsettings}" busparams** <em>b</em> **.** <em>d</em> **.** <em>f</em>

場所*b*、 *d*、および*f*は、バス、デバイス、およびデバッグに使用する、選択したターゲット コンピューターに 1394 コント ローラーの関数の数。

以下に例を示します。

**bcdedit /set "{dbgsettings}" busparams 4.4.0**

## <a name="span-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグ セッションの開始


1.  ホスト コンピューターには、管理者として Visual Studio を開きます。
2.  **ツール**] メニューの [選択**プロセスにアタッチ**します。
3.  **トランスポート**、選択**Windows カーネル モードのデバッガー**します。
4.  **修飾子**、以前に構成されているターゲット コンピューターの名前を選択します。
5.  クリックして**アタッチ**します。

この時点では、1394 デバッグ ドライバーが、ホスト コンピューターにインストールを取得します。 これは、ため、Visual Studio を管理者として実行することが重要です。 1394 デバッグ ドライバーがインストールされた後、後続のデバッグ セッションを管理者として実行する必要はありません。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグ セッションの開始


1.  Visual Studio で、ホスト コンピューター上で、**ツール**] メニューの [選択**プロセスにアタッチ**します。
2.  **トランスポート**、選択**Windows カーネル モードのデバッガー**します。
3.  **修飾子**、以前に構成されているターゲット コンピューターの名前を選択します。
4.  クリックして**アタッチ**します。

## <a name="span-idtroubleshootingtipsfordebuggingovera1394cablespanspan-idtroubleshootingtipsfordebuggingovera1394cablespantroubleshooting-tips-for-debugging-over-a-1394-cable"></a><span id="troubleshooting_tips_for_debugging_over_a_1394_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_1394_CABLE"></span>1394 ケーブル経由でのデバッグのトラブルシューティングのヒント


1394 デバッグの問題のほとんどは、ホストまたはターゲットのいずれかのコンピューターで複数の 1394 コント ローラーを使用して、発生します。 ホスト コンピューターに 1394 の複数のコント ローラーを使用することはサポートされていません。 ホスト上で実行され、1394 デバッグ ドライバーは、レジストリに列挙された 1394 最初のコント ローラーとのみ通信できます。 カードを削除するか (デバイス マネージャーを使用) を無効にする場合は、マザーボード、および個別の 1394 カードに組み込まれている 1394 コント ローラーがある場合は、組み込みのコント ローラー。

これは推奨されませんが、ターゲット コンピューター、複数の 1394 コント ローラーことができます。 マザーボード上のターゲット コンピューターに 1394 コント ローラーした場合、デバッグ可能であれば、そのコント ローラーを使用します。 追加 1394 のカードがある場合は、カードを取り外すをオンボード コント ローラーを使用する必要があります。 別のソリューションでは、オンボードの 1394 コント ローラーで、コンピューターの BIOS 設定を無効にします。

ターゲット コンピューターで有効になって 1394 コント ローラーが複数ある場合は、デバッガーがデバッグの要求をコント ローラーを認識できるように bus パラメーターを指定する必要があります。 デバイス マネージャーを開き、バスのパラメーターを指定し、デバッグに使用する 1394 コント ローラーを見つけます。 コント ローラーのプロパティ ページを開き、バス番号、デバイスの数、および関数の数をメモしておきます。 管理者特権でコマンド プロンプト ウィンドウで、次のコマンドを入力します。 ここ*b*、 *d*、および*f* bus、デバイス、および関数の数値を 10 進数形式では。

**bcdedit /set "{dbgsettings}" busparams** <em>b</em> **.** <em>d</em> **.** <em>f</em>

ターゲット コンピューターを再起動します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグの設定](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






