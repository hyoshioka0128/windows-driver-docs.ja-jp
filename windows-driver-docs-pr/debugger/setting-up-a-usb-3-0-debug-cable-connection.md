---
title: USB 3.0 ケーブル経由のカーネルモード デバッグの手動設定
description: Windows 用デバッグツールは、USB 3.0 ケーブルでのカーネルデバッグをサポートしています。 このトピックでは、USB 3.0 デバッグを手動で設定する方法について説明します。
ms.assetid: 9A9F5DA0-B98A-4C19-A723-67D06B2409B5
ms.date: 01/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8fb12186cdb0d395f75da1e3e399e8372697f874
ms.sourcegitcommit: 0a31c9fa18d5bf02373e7c000abd65e3db78b280
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2020
ms.locfileid: "76910352"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-30-cable-manually"></a>USB 3.0 ケーブル経由のカーネルモード デバッグの手動設定

Windows 用デバッグツールは、USB 3.0 ケーブルでのカーネルデバッグをサポートしています。 このトピックでは、USB 3.0 デバッグを手動で設定する方法について説明します。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。

USB 3.0 ケーブルでのデバッグには、次のハードウェアが必要です。

- USB 3.0 デバッグケーブル。 これは、USB 3.0 ラインと Vbus を持たないクロスオーバーケーブルです。

- ホストコンピューターで、xHCI (USB 3.0) ホストコントローラー

- ターゲットコンピューターで、デバッグをサポートする xHCI (USB 3.0) ホストコントローラー

## <a name="span-idsetting_up_the_computer_usb3_manualspanspan-idsetting_up_the_computer_usb3_manualspansetting-up-the-target-computer"></a><span id="setting_up_the_computer_usb3_manual"></span><span id="SETTING_UP_THE_COMPUTER_USB3_MANUAL"></span>ターゲットコンピューターのセットアップ

1. ターゲットコンピューターで、UsbView ツールを起動します。 UsbView ツールは、Windows 用デバッグツールに含まれています。
2. [UsbView] で、すべての xHCI ホストコントローラーを見つけます。
3. [UsbView] で、xHCI ホストコントローラーのノードを展開します。 ホストコントローラーのポートでデバッグがサポートされていることを確認します。

    ```console
    [Port1]

    Is Port User Connectable:         yes
    Is Port Debug Capable:            yes
    Companion Port Number:            3
    Companion Hub Symbolic Link Name: USB#ROOT_HUB30#5&32bab638&0&0#{...}
    Protocols Supported:
     USB 1.1:                         no
     USB 2.0:                         no
     USB 3.0:                         yes
    ```

4. デバッグに使用する xHCI コントローラーのバス、デバイス、および関数の番号をメモしておきます。 UsbView には、これらの数値が表示されます。 次の例では、バス番号が48、デバイス番号が0、関数番号が0になっています。

    ```console
    USB xHCI Compliant Host Controller
    ...
    DriverKey: {36fc9e60-c465-11cf-8056-444553540000}\0020
    ...
    Bus.Device.Function (in decimal): 48.0.0
    ```

5. デバッグをサポートする xHCI コントローラーを特定したら、次の手順として、xHCI コントローラーのポートに関連付けられている物理 USB コネクタを探します。 物理コネクタを見つけるには、任意の USB 3.0 デバイスをターゲットコンピューター上の任意の USB コネクタに接続します。 UsbView を更新して、デバイスが配置されている場所を確認します。 UsbView によって、選択した xHCI ホストコントローラーに接続されているデバイスが表示された場合は、USB 3.0 デバッグに使用できる物理 USB コネクタがあります。

> [!IMPORTANT]
> Bcdedit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。 デバッグが完了し、カーネルデバッグを無効にした後、セキュアブートを再度有効にすることができます。  

6. ターゲットコンピューターで、管理者としてコマンドプロンプトウィンドウを開き、次のコマンドを入力します。

   - **bcdedit/debug on**
   - **bcdedit/dbgsettings usb targetname:** <em>targetname</em>

   *TargetName*はターゲットコンピューター用に作成する名前です。 *TargetName*はターゲットコンピューターの正式な名前である必要はないことに注意してください。次の制限を満たしている限り、任意の文字列を指定できます。

   -  文字列では、大文字と小文字の組み合わせで*TargetName*内の任意の場所に "debug" を含めることはできません。 たとえば、targetname 内の任意の場所で "DeBuG" または "DEBUG" を使用すると、デバッグは正しく機能しません。  
   -  文字列内の唯一の文字は、ハイフン (-)、アンダースコア (\_)、0 ~ 9 の数字、および文字 A ~ Z (大文字または小文字) です。
   -  文字列の最大長は24文字です。

7. ターゲットコンピューターに複数の USB ホストコントローラーがある場合は、次のコマンドを入力します。

   **bcdedit/set "{dbgsettings}" busparams** *b. d. f*

   ここで、 *b*、 *d*、および*f*は、デバッグに使用する USB ホストコントローラーのバス、デバイス、および関数の番号です。 バス、デバイス、および関数の数値は、10進形式である必要があります。

   例:

   **bcdedit/set "{dbgsettings}" busparams 48.0.0**

8. ターゲット コンピューターを再起動します。

## <a name="span-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグセッションを開始する

1. ユニバーサルシリアルバス (USB) 3.0 デバッグケーブルを、ホストとターゲットコンピュータでデバッグ用に選択した USB 3.0 ポートに接続します。
2. ホストコンピューター上で実行されている Windows のビット数 (32 ビットまたは64ビット) を確認します。
3. ホストコンピューターで、ホストコンピューター上で実行されている Windows のビットと一致するバージョンの WinDbg (管理者として) を開きます。 たとえば、ホストコンピューターで64ビットバージョンの Windows が実行されている場合は、管理者として、WinDbg の64ビットバージョンを開きます。
4. **[ファイル]** メニューの **[カーネルデバッグ]** をクリックします。 カーネルデバッグ ダイアログボックスで、 **USB** タブを開きます。ターゲットコンピューターを設定するときに作成したターゲットの名前を入力します。 **[OK]** をクリックすると、

この時点で、USB デバッグドライバーがホストコンピューターにインストールされます。 このため、WinDbg のビットと Windows のビットを一致させることが重要です。 USB デバッグドライバーをインストールした後、次のデバッグセッションでは、32ビットまたは64ビットバージョンの WinDbg を使用できます。

## <a name="span-idstarting_the_debugging_session_usb3_manualspanspan-idstarting_the_debugging_session_usb3_manualspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session_usb3_manual"></span><span id="STARTING_THE_DEBUGGING_SESSION_USB3_MANUAL"></span>デバッグセッションの開始

### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg の使用

ホストコンピューターで、[WinDbg] を開きます。 **[ファイル]** メニューの **[カーネルデバッグ]** をクリックします。 カーネルデバッグ ダイアログボックスで、 **USB** タブを開きます。ターゲットコンピューターを設定するときに作成したターゲットの名前を入力します。 **[OK]** をクリックすると、

また、コマンドプロンプトウィンドウで次のコマンドを入力して、WinDbg を使用してセッションを開始することもできます。ここで、 *TargetName*はターゲットコンピューターをセットアップしたときに作成したターゲット名です。

**windbg/k usb: targetname =** <em>targetname</em>

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD の使用

ホストコンピューターで、コマンドプロンプトウィンドウを開き、次のコマンドを入力します。 *TargetName*はターゲットコンピューターをセットアップしたときに作成したターゲット名です。

**kd/k usb: targetname =** <em>targetname</em>

デバッガーが接続されたら、ターゲットコンピューターを再起動します。 PC を再起動する方法の1つとして、管理者のコマンドプロンプトから `shutdown -r -t 0 ` コマンドを使用する方法があります。

対象の PC が再起動すると、デバッガーは自動的に接続されます。

## <a name="span-idtroubleshooting_tips_for_debugging_over_usb_30spanspan-idtroubleshooting_tips_for_debugging_over_usb_30spantroubleshooting-tips-for-debugging-over-usb-30"></a><span id="troubleshooting_tips_for_debugging_over_usb_3.0"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_USB_3.0"></span>USB 3.0 でのデバッグに関するトラブルシューティングのヒント

場合によっては、電源切り替えが USB 3.0 でのデバッグに干渉することがあります。 この問題が発生した場合は、デバッグに使用している xHCI ホストコントローラー (およびそのルートハブ) のセレクティブサスペンドを無効にしてください。

1. デバイスマネージャーで、xHCI ホストコントローラーのノードに移動します。 ノードを右クリックし、 **[プロパティ]** を選択します。 **[電源管理]** タブが表示されている場合は、電源管理を有効にする チェックボックスをオフにし、 **[コンピューターでこのデバイスの電源をオフにすることを許可]** する チェックボックスをオフにします。

2. デバイスマネージャーで、xHCI ホストコントローラーのルートハブのノードに移動します。 ノードを右クリックし、 **[プロパティ]** を選択します。 **[電源管理]** タブが表示されている場合は、電源管理を有効にする チェックボックスをオフにし、 **[コンピューターでこのデバイスの電源をオフにすることを許可]** する チェックボックスをオフにします。

デバッグに xHCI host controller の使用が終了したら、xHCI ホストコントローラーのセレクティブサスペンドを有効にします。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[カーネルモードデバッグの手動設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
