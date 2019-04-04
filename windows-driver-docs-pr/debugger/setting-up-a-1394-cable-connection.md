---
title: 1394 ケーブル経由のカーネルモード デバッグの手動設定
description: デバッグ ツールの Windows カーネルは、1394 (Firewire) ケーブル経由でデバッグをサポートします。 このトピックでは、1394 デバッグを手動で設定する方法について説明します。
ms.assetid: bcfc61a1-0315-451c-a279-f6305995b05f
keywords: 1394 ケーブルの接続、1394 接続を IEEE 1394 ケーブル、FireWire ケーブルの作成
ms.date: 05/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6bd273e328d6fd6642f8ca6bf1b281b737383b10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570278"
---
# <a name="setting-up-kernel-mode-debugging-over-a-1394-cable-manually"></a>1394 ケーブル経由のカーネルモード デバッグの手動設定

> [!IMPORTANT]
> 1394 トランスポートは、Windows 10 バージョン 1607 およびそれ以前で使用できます。 以降のバージョンの Windows でご利用いただけません。 イーサネットを使用して KDNET などの他のトランスポートにプロジェクトを移行する必要があります。 トランスポートの詳細については、[カーネル モード デバッグのセットアップを手動でのネットワーク ケーブル](setting-up-a-network-debugging-connection.md)を参照してください。
>

デバッグ ツールの Windows カーネルは、1394 (Firewire) ケーブル経由でデバッグをサポートします。 このトピックでは、1394 デバッグを手動で設定する方法について説明します。

デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*対象のコンピュータ*します。 ホストおよびターゲット コンピューター 1394 アダプターに対し、および Windows XP を実行する必要がありますまたはそれ以降。 ホストとターゲットのコンピューターを同じバージョンの Windows を実行する必要はありません。

## <a name="span-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspansetting-up-the-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>ターゲット コンピューターをセットアップします。


1.  ホストおよびターゲット コンピューターでデバッグするため、選択した 1394 コント ローラーには、1394 ケーブルを接続します。

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。
> テストが完了すると、これらのセキュリティ機能を再度有効にし、適切なセキュリティ機能を無効にするテスト PC を管理します。

2. 管理者特権でコマンド プロンプト ウィンドウで、次のコマンドを入力します。 ここ*n*は 0 ~ 62、任意のチャンネル番号。

   **bcdedit /debug on**

   **bcdedit/dbgsettings 1394 チャネル:**<em>n</em>

3. 1 つ以上を使用する必要がある場合、ターゲット コンピューターに 1394 コント ローラーは、バス、デバイス、およびデバッグに使用する、1394 コント ローラーの関数の番号を指定する必要があります。 詳細については、[を 1394 デバッグ用のトラブルシューティングのヒント](#troubleshooting-tips-for-debugging-over-a-1394-cable)を参照してください。

4. まだ対象のコンピュータを再起動されません。

## <a name="span-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグ セッションの開始


1.  ホスト コンピューターで実行されている Windows のビット数 (32 ビットまたは 64 ビット) を決定します。
2.  ホスト コンピューターでは、ホスト コンピューターで実行されている Windows のビット数に一致する (管理者) として WinDbg のバージョンが開きます。 たとえば、ホスト コンピューターで Windows の 64 ビット版が実行されている場合は、管理者として WinDbg の 64 ビット バージョンを開きます。
3.  **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、 **1394**タブ。チャンネル番号を入力し、クリックして**OK**します。

    この時点では、1394 デバッグ ドライバーが、ホスト コンピューターにインストールを取得します。 これは、ため、Windows のビット数に WinDbg のビット数と一致することが重要です。 1394 デバッグ ドライバーがインストールされた後は、後続のデバッグ セッション WinDbg の 32 ビットまたは 64 ビット バージョンのいずれかを使用できます。

4.  ターゲット コンピューターを再起動します。

## <a name="span-idstartingadebuggingsessionspanspan-idstartingadebuggingsessionspanspan-idstartingadebuggingsessionspanstarting-a-debugging-session"></a><span id="Starting_a_Debugging_Session"></span><span id="starting_a_debugging_session"></span><span id="STARTING_A_DEBUGGING_SESSION"></span>デバッグ セッションの開始


### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg を使用します。

- ホスト コンピューターでは、WinDbg を開きます。 **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、 **1394**タブ。チャンネル番号を入力し、クリックして**OK**します。

  コマンド プロンプト ウィンドウで、次のコマンドを入力して、WinDbg でセッションを開始することもできます、 *n*チャネル番号します。

  **windbg/k 1394:channel =**<em>n</em>

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD を使用します。

- ホスト コンピューターでは、コマンド プロンプト ウィンドウを開き、次のコマンドを入力して、 *n*チャネル番号します。

  **kd/k 1394:channel =**<em>n</em>

## <a name="span-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>環境変数の使用


ホスト コンピューターでは、1394 チャネルを指定するのに環境変数を使用することができます。 デバッグ セッションを開始するたびに、チャネルを指定する必要はありません。 環境変数を使用して、1394 チャネルを指定、コマンド プロンプト ウィンドウを開き、次のコマンドを入力する場所*n*チャネル番号します。

- **設定\_NT\_デバッグ\_BUS 1394 を =**
- **設定\_NT\_デバッグ\_1394\_チャネル =**<em>n</em>

デバッグ セッションを開始するにはコマンド プロンプト ウィンドウを開き、次のコマンドのいずれかを入力します。

-   **kd**
-   **windbg**

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


完全なドキュメントについて、 **bcdedit**コマンドと、boot.ini ファイルで、Windows Driver Kit (WDK) ドキュメントのドライバーのテストおよびデバッグのブート オプションを参照してください。

## <a name="span-idtroubleshooting-tips-for-debugging-over-a-1394-cablespanspan-idtroubleshooting-tips-for-debugging-over-a-1394-cablespantroubleshooting-tips-for-debugging-over-a-1394-cable"></a><span id="troubleshooting-tips-for-debugging-over-a-1394-cable"></span><span id="TROUBLESHOOTING-TIPS-FOR-DEBUGGING-OVER-A-1394-CABLE"></span>1394 ケーブル経由でのデバッグのトラブルシューティングのヒント


1394 デバッグの問題のほとんどは、ホストまたはターゲットのいずれかのコンピューターで複数の 1394 コント ローラーを使用して、発生します。 ホスト コンピューターに 1394 の複数のコント ローラーを使用することはサポートされていません。 ホスト上で実行され、1394 デバッグ ドライバーは、レジストリに列挙された 1394 最初のコント ローラーとのみ通信できます。 1394 のコント ローラーと個別 1394 カードのマザーボードに組み込まれている場合は、カードを取り外すか、または組み込みのコント ローラーで、コンピューターの BIOS 設定を無効にします。

これは推奨されませんが、ターゲット コンピューター、複数の 1394 コント ローラーことができます。 マザーボード上のターゲット コンピューターに 1394 コント ローラーした場合、デバッグ可能であれば、そのコント ローラーを使用します。 追加 1394 のカードがある場合は、カードを取り外すをオンボード コント ローラーを使用する必要があります。 別のソリューションでは、オンボードの 1394 コント ローラーで、コンピューターの BIOS 設定を無効にします。

ターゲット コンピューターで有効になって 1394 コント ローラーが複数ある場合は、デバッガーがデバッグの要求をコント ローラーを認識できるように bus パラメーターを指定する必要があります。 ターゲット コンピューターでは、デバイス マネージャーを開き、バスのパラメーターを指定し、デバッグに使用する 1394 コント ローラーを見つけます。 コント ローラーのプロパティ ページを開き、バス番号、デバイスの数、および関数の数をメモしておきます。 管理者特権でコマンド プロンプト ウィンドウで、次のコマンドを入力します。 ここ*b*、 *d*、および*f* bus、デバイス、および関数の数値を 10 進数形式では。

**bcdedit の設定"{dbgsettings}"busparams** <em>b</em>**.**<em>d</em>**.**<em>f</em>します。

ターゲット コンピューターを再起動します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カーネル モードのデバッグを手動での設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






