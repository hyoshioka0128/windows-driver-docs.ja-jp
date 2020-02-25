---
title: 1394 ケーブル経由のカーネルモード デバッグの手動設定
description: Windows 用デバッグツールでは、1394 (Firewire) ケーブル経由のカーネルデバッグがサポートされています。 このトピックでは、1394デバッグを手動で設定する方法について説明します。
ms.assetid: bcfc61a1-0315-451c-a279-f6305995b05f
keywords: 1394ケーブル接続、1394接続、IEEE 1394 ケーブル、FireWire ケーブルを作成する
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 98a8f0e1e3f912ee21b1f19440247a32b382f1cd
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528956"
---
# <a name="setting-up-kernel-mode-debugging-over-a-1394-cable-manually"></a>1394 ケーブル経由のカーネルモード デバッグの手動設定

> [!IMPORTANT]
> 1394トランスポートは、Windows 10 バージョン1607以前で使用できます。 これは、以降のバージョンの Windows では使用できません。 イーサネットを使用して KDNET などの他のトランスポートにプロジェクトを移行する必要があります。 そのトランスポートの詳細については、「 [KDNET Network カーネルデバッグの自動](setting-up-a-network-debugging-connection-automatically.md)セットアップ」を参照してください。
>

Windows 用デバッグツールでは、1394 (Firewire) ケーブル経由のカーネルデバッグがサポートされています。 このトピックでは、1394デバッグを手動で設定する方法について説明します。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。 ホストとターゲットコンピュータにはそれぞれ1394アダプターがあり、Windows XP 以降を実行している必要があります。 ホストとターゲットのコンピューターは、同じバージョンの Windows を実行している必要はありません。

## <a name="span-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspansetting-up-the-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>ターゲットコンピューターのセットアップ

1. ホストとターゲットコンピュータでデバッグ用に選択した1394コントローラに1394ケーブルを接続します。

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。
> セキュリティ機能が無効になっている場合は、テストが完了し、テスト PC を適切に管理するときに、これらのセキュリティ機能を再び有効にします。

2. 管理者特権でのコマンドプロンプトウィンドウで、次のコマンドを入力します。ここで、 *n*は選択したチャネル番号です (0 ~ 62)。

   **bcdedit/debug on**

   **bcdedit/dbgsettings 1394 channel:** <em>n</em>

3. ターゲットコンピューターに 1 1394 を超えるコントローラーがある場合は、デバッグに使用する1394コントローラーのバス、デバイス、および関数番号を指定する必要があります。 詳細については、「 [1394 デバッグのトラブルシューティングのヒント](#troubleshooting-tips-for-debugging-over-a-1394-cable)」を参照してください。

4. ターゲットコンピューターをまだ再起動しないでください。

## <a name="span-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグセッションを開始する

1.  ホストコンピューター上で実行されている Windows のビット数 (32 ビットまたは64ビット) を確認します。
2.  ホストコンピューターで、ホストコンピューター上で実行されている Windows のビットと一致するバージョンの WinDbg (管理者として) を開きます。 たとえば、ホストコンピューターで64ビットバージョンの Windows が実行されている場合は、管理者として、WinDbg の64ビットバージョンを開きます。
3.  **[ファイル]** メニューの **[カーネルデバッグ]** をクリックします。 カーネルデバッグ ダイアログボックスで、 **1394** タブを開きます。チャンネル番号を入力し、**OK** をクリックします。

    この時点で、1394デバッグドライバーがホストコンピューターにインストールされます。 このため、WinDbg のビットと Windows のビットを一致させることが重要です。 1394デバッグドライバーをインストールした後、次のデバッグセッションでは、WinDbg の32ビットバージョンまたは64ビットバージョンのいずれかを使用できます。

4.  ターゲット コンピューターを再起動します。

## <a name="span-idstarting_a_debugging_sessionspanspan-idstarting_a_debugging_sessionspanspan-idstarting_a_debugging_sessionspanstarting-a-debugging-session"></a><span id="Starting_a_Debugging_Session"></span><span id="starting_a_debugging_session"></span><span id="STARTING_A_DEBUGGING_SESSION"></span>デバッグセッションの開始

### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg の使用

- ホストコンピューターで、[WinDbg] を開きます。 **[ファイル]** メニューの **[カーネルデバッグ]** をクリックします。 カーネルデバッグ ダイアログボックスで、 **1394** タブを開きます。チャンネル番号を入力し、**OK** をクリックします。

  また、コマンドプロンプトウィンドウで次のコマンドを入力して、WinDbg を使用してセッションを開始することもできます。ここで、 *n*はチャネル番号です。

  **windbg/k 1394: channel =** <em>n</em>

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD の使用

- ホストコンピューターで、コマンドプロンプトウィンドウを開き、次のコマンドを入力します。ここで、 *n*はチャネル番号です。

  **kd/k 1394: channel =** <em>n</em>

## <a name="span-idusing_environment_variablesspanspan-idusing_environment_variablesspanspan-idusing_environment_variablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>環境変数の使用


ホストコンピューターでは、環境変数を使用して1394チャネルを指定できます。 その後、デバッグセッションを開始するたびにチャネルを指定する必要はありません。 環境変数を使用して1394チャネルを指定するには、コマンドプロンプトウィンドウを開き、次のコマンドを入力します。ここで、 *n*はチャネル番号です。

- **\_NT\_デバッグ\_バス = 1394 を設定します。**
- **\_NT\_デバッグ\_1394\_CHANNEL =** <em>n</em>に設定します。

デバッグセッションを開始するには、コマンドプロンプトウィンドウを開き、次のいずれかのコマンドを入力します。

-   **kd**
-   **windbg**

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


**Bcdedit**コマンドと boot.ini ファイルの完全なドキュメントについては、Windows driver KIT (WDK) ドキュメントの「ドライバーテストおよびデバッグ用のブートオプション」を参照してください。

## <a name="span-idtroubleshooting-tips-for-debugging-over-a-1394-cablespanspan-idtroubleshooting-tips-for-debugging-over-a-1394-cablespantroubleshooting-tips-for-debugging-over-a-1394-cable"></a><span id="troubleshooting-tips-for-debugging-over-a-1394-cable"></span><span id="TROUBLESHOOTING-TIPS-FOR-DEBUGGING-OVER-A-1394-CABLE"></span>1394ケーブルでのデバッグに関するトラブルシューティングのヒント


1394デバッグの問題のほとんどは、ホストまたはターゲットコンピューターで複数の1394コントローラーを使用した場合に発生します。 ホストコンピューターでの複数の1394コントローラーの使用はサポートされていません。 ホスト上で実行される1394デバッグドライバーは、レジストリで列挙された最初の1394コントローラーとのみ通信できます。 マザーボードに1394コントローラーを内蔵し、別の1394カードを使用している場合は、カードを取り外すか、コンピューターの BIOS 設定でビルトインコントローラーを無効にします。

ターゲットコンピューターは、複数の1394コントローラーを持つことができますが、これは推奨されません。 ターゲットコンピューターのマザーボードに1394コントローラーが搭載されている場合は、可能であれば、そのコントローラーをデバッグに使用します。 1394カードが追加されている場合は、カードを取り外し、オンボードコントローラーを使用する必要があります。 もう1つの解決策は、コンピューターの BIOS 設定で、オンボード1394コントローラーを無効にすることです。

ターゲットコンピューターで複数の1394コントローラーを有効にする場合は、デバッグのために要求するコントローラーをデバッガーが認識できるように、バスパラメーターを指定する必要があります。 バスパラメーターを指定するには、ターゲットコンピューターでデバイスマネージャーを開き、デバッグに使用する1394コントローラーを探します。 コントローラーのプロパティページを開き、バス番号、デバイス番号、および関数番号をメモしておきます。 管理者特権でのコマンドプロンプトウィンドウで、次のコマンドを入力します。ここで、 *b*、 *d*、および*f*は、10進形式のバス、デバイス、および関数の数値です。

**bcdedit-"{dbgsettings}" busparams** <em>b</em>**を設定します。** <em>d</em> **。** <em>f</em>。

ターゲット コンピューターを再起動します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[カーネルモードデバッグの手動設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

[KDNET Network カーネルデバッグを自動的に設定する](setting-up-a-network-debugging-connection-automatically.md)
