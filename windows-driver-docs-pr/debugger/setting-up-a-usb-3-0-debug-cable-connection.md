---
title: USB 3.0 ケーブル経由のカーネルモード デバッグの手動設定
description: デバッグ ツールの Windows カーネルが USB 3.0 ケーブル経由でデバッグをサポートします。 このトピックでは、USB 3.0 を手動でのデバッグを設定する方法について説明します。
ms.assetid: 9A9F5DA0-B98A-4C19-A723-67D06B2409B5
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 588f12f4fe1080e5df460743405e362a3bba73a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582428"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-30-cable-manually"></a>USB 3.0 ケーブル経由のカーネルモード デバッグの手動設定


デバッグ ツールの Windows カーネルが USB 3.0 ケーブル経由でデバッグをサポートします。 このトピックでは、USB 3.0 を手動でのデバッグを設定する方法について説明します。

デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*対象のコンピュータ*します。

USB 3.0 ケーブル経由でのデバッグには、次のハードウェアが必要です。

-   デバッグの USB 3.0 ケーブル。 これは、USB 3.0 行のみとありません Vbus を持つ、A クロス オーバー ケーブルです。

-   ホスト コンピューター (USB 3.0) の xHCI ホスト コント ローラーで

-   対象のコンピューターのデバッグをサポートしています (USB 3.0) の xHCI ホスト コント ローラー

## <a name="span-idsettingupthecomputerusb3manualspanspan-idsettingupthecomputerusb3manualspansetting-up-the-target-computer"></a><span id="setting_up_the_computer_usb3_manual"></span><span id="SETTING_UP_THE_COMPUTER_USB3_MANUAL"></span>ターゲット コンピューターをセットアップします。


1.  対象のコンピューターに UsbView ツールを起動します。 Windows ツールのデバッグにはに UsbView ツールが含まれます。
2.  UsbView では、すべての xHCI ホスト コント ローラーを見つけます。
3.  UsbView、xHCI ホスト コント ローラーのノードを展開します。 ホスト コント ローラー上のポートがデバッグをサポートしていることを示す値を探します。

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

4.  デバッグに使用する、xHCI コント ローラーには、バス、デバイス、および関数の番号をメモしてをおきます。 UsbView には、これらの数が表示されます。 次の例では、バス番号は 48 です、デバイス数は 0、および関数の数は 0。

    ```console
    USB xHCI Compliant Host Controller
    ...
    DriverKey: {36fc9e60-c465-11cf-8056-444553540000}\0020
    ...
    Bus.Device.Function (in decimal): 48.0.0
    ```

5.  デバッグをサポートする xHCI コント ローラーを特定したら後、次の手順では、xHCI コント ローラー上のポートに関連付けられている物理 USB コネクタを検索します。 物理のコネクタを検索するには、ターゲット コンピューター上の任意の USB コネクタに任意の USB 3.0 デバイスを接続します。 デバイスが配置されている UsbView を更新します。 UsbView を示しています、選択した xHCI ホスト コント ローラーに接続されているデバイス、USB 3.0 のデバッグに使用できる物理 USB コネクタを発見しました。

> [!IMPORTANT]
> Bcdedit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。 セキュア ブートは、再度有効に完了したらとデバッグは無効になりましたカーネル デバッグします。  


6. 対象のコンピューターに管理者としてコマンド プロンプト ウィンドウを開きし、これらのコマンドを入力します。

   - **bcdedit /debug on**
   - **bcdedit/dbgsettings usb targetname:**<em>TargetName</em>

   場所*TargetName*対象のコンピュータ用に作成した名前を指定します。 なお*TargetName*対象のコンピュータの正式な名前を指定する必要はありませんこれらの制限を満たしている限り、作成した任意の文字列にすることができます。

   -   文字列の最大長は、24 文字です。
   -   文字列内の唯一の文字はアンダー スコア、ハイフン (-)、(\_)、0 ~ 9 の数字と文字 A ~ Z (大文字または小文字)。

7. をターゲット コンピューターに 1 つ以上の USB ホスト コント ローラーがある場合は、このコマンドを入力します。

   **bcdedit /set "{dbgsettings}" busparams** *b.d.f*

   場所*b*、 *d*、および*f*は、バス、デバイス、およびデバッグに使用する予定の USB ホスト コント ローラーの関数の番号。 バス、デバイス、および関数の番号は、10 進数形式でなければなりません。

   例:

   **bcdedit /set "{dbgsettings}" busparams 48.0.0**

8. ターゲット コンピューターを再起動します。

## <a name="span-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグ セッションの開始


1.  ユニバーサル シリアル バス (USB) 3.0 デバッグ ケーブルをホストとターゲット コンピューターでデバッグするため、選択した USB 3.0 ポートに接続します。
2.  ホスト コンピューターで実行されている Windows のビット数 (32 ビットまたは 64 ビット) を決定します。
3.  ホスト コンピューターでは、ホスト コンピューターで実行されている Windows のビット数に一致する (管理者) として WinDbg のバージョンが開きます。 たとえば、ホスト コンピューターで Windows の 64 ビット版が実行されている場合は、管理者として WinDbg の 64 ビット バージョンを開きます。
4.  **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、 **USB**タブ。ターゲット コンピューターをセットアップするときに作成したターゲットの名前を入力します。 **[OK]** をクリックします。

この時点では、USB デバッグのドライバーは、ホスト コンピューターにインストールを取得します。 これは、ため、Windows のビット数に WinDbg のビット数と一致することが重要です。 USB デバッグ ドライバーがインストールされた後は、後続のデバッグ セッション WinDbg の 32 ビットまたは 64 ビット バージョンのいずれかを使用できます。

## <a name="span-idstartingthedebuggingsessionusb3manualspanspan-idstartingthedebuggingsessionusb3manualspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session_usb3_manual"></span><span id="STARTING_THE_DEBUGGING_SESSION_USB3_MANUAL"></span>デバッグ セッションの開始


### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg を使用します。

ホスト コンピューターでは、WinDbg を開きます。 **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、 **USB**タブ。ターゲット コンピューターをセットアップするときに作成したターゲットの名前を入力します。 **[OK]** をクリックします。

コマンド プロンプト ウィンドウで、次のコマンドを入力して、WinDbg でセッションを開始することもできます、 *TargetName*はターゲット コンピューターをセットアップするときに作成したターゲットの名前です。

**windbg /k usb:targetname=**<em>TargetName</em>

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD を使用します。

ホスト コンピューターでは、コマンド プロンプト ウィンドウを開き、次のコマンドを入力して、 *TargetName*はターゲット コンピューターをセットアップするときに作成したターゲット名です。

**kd /k usb:targetname=**<em>TargetName</em>

## <a name="span-idtroubleshootingtipsfordebuggingoverusb30spanspan-idtroubleshootingtipsfordebuggingoverusb30spantroubleshooting-tips-for-debugging-over-usb-30"></a><span id="troubleshooting_tips_for_debugging_over_usb_3.0"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_USB_3.0"></span>USB 3.0 経由でのデバッグのトラブルシューティングのヒント


場合によっては、電源遷移できる USB 3.0 経由でのデバッグに干渉することです。 この問題は、選択的に無効にした場合は、デバッグを使用している xHCI ホスト コント ローラー (とそのルート ハブ) を中断します。

1.  デバイス マネージャーでは、xHCI ホスト コント ローラーのノードに移動します。 ノードを右クリックし、選択**プロパティ**します。 ある場合、**電源管理**タブ、タブを開き、オフ、**電力を節約するには、このデバイスを無効にするコンピューターを許可する**チェック ボックスをオンします。
2.  デバイス マネージャーでは、xHCI ホスト コント ローラーのルート ハブのノードに移動します。 ノードを右クリックし、選択**プロパティ**します。 ある場合、**電源管理**タブ、タブを開き、オフ、**電力を節約するには、このデバイスを無効にするコンピューターを許可する**チェック ボックスをオンします。

XHCI ホスト コント ローラーを使用して、デバッグが完了したら、有効にするオプションを選択は、xHCI ホスト コント ローラーを中断します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カーネル モードのデバッグを手動での設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






