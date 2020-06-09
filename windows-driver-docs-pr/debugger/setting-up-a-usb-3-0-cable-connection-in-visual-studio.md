---
title: Visual Studio での USB 3.0 ケーブル経由でのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用して、USB 3.0 ケーブルでカーネルモードのデバッグを設定し、実行することができます。
ms.assetid: F8DD0475-13CE-464A-A491-AEFA962A96DB
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: a987fa88d9a7b5c5dc6c959949afe285d7f7a3cf
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534315"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-30-cable-in-visual-studio"></a>Visual Studio での USB 3.0 ケーブル経由でのカーネルモード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>

Microsoft Visual Studio を使用して、USB 3.0 ケーブルでカーネルモードのデバッグを設定し、実行することができます。 Visual Studio を使用してカーネルモードのデバッグを行うには、Visual Studio に Windows Driver Kit (WDK) が統合されている必要があります。 統合環境をインストールする方法の詳細については、「 [Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)」を参照してください。

Visual Studio を使用して USB 3.0 デバッグを設定する代わりに、手動でセットアップを行うこともできます。 詳細については、「 [USB 3.0 ケーブル経由でカーネルモードのデバッグを手動で設定する](setting-up-a-usb-3-0-debug-cable-connection.md)」を参照してください。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ対象のコンピューターは*ターゲットコンピューター*と呼ばれます。

USB 3.0 接続でのデバッグには、次のハードウェアが必要です。

-   USB 3.0 デバッグケーブル。 これは、USB 3.0 ラインと Vbus を持たないクロスオーバーケーブルです。

-   ホストコンピューターで、xHCI (USB 3.0) ホストコントローラー

-   ターゲットコンピューターで、デバッグをサポートする xHCI (USB 3.0) ホストコントローラー

## <a name="span-idsetting_up_the_computer_usb3_manualspanspan-idsetting_up_the_computer_usb3_manualspanidentifying-a-debug-port-on-the-target-computer"></a><span id="setting_up_the_computer_usb3_manual"></span><span id="SETTING_UP_THE_COMPUTER_USB3_MANUAL"></span>ターゲットコンピューターでのデバッグポートの識別


1.  ターゲットコンピューターで、UsbView ツールを起動します。 UsbView ツールは、Windows 用デバッグツールに含まれています。
2.  [UsbView] で、すべての xHCI ホストコントローラーを見つけます。
3.  [UsbView] で、xHCI ホストコントローラーのノードを展開します。 ホストコントローラーのポートでデバッグがサポートされていることを確認します。

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

4.  デバッグに使用する xHCI コントローラーのバス、デバイス、および関数の番号をメモしておきます。 UsbView には、これらの数値が表示されます。 次の例では、バス番号が48、デバイス番号が0、関数番号が0になっています。

    ```console
    USB xHCI Compliant Host Controller
    ...
    DriverKey: {36fc9e60-c465-11cf-8056-444553540000}\0020
    ...
    Bus.Device.Function (in decimal): 48.0.0
    ```

5.  デバッグをサポートする xHCI コントローラーを特定したら、次の手順として、xHCI コントローラーのポートに関連付けられている物理 USB コネクタを探します。 物理コネクタを見つけるには、任意の USB 3.0 デバイスをターゲットコンピューター上の任意の USB コネクタに接続します。 UsbView を更新して、デバイスが配置されている場所を確認します。 XHCI ホストコントローラーに接続されているデバイスが UsbView に示されている場合は、USB 3.0 デバッグに使用できる物理 USB コネクタが見つかりました。

## <a name="span-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>ホストとターゲットコンピューターの構成


1.  「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の説明に従って、ホストとターゲットコンピューターの構成を開始します。
2.  ホストコンピューターの Visual Studio で、[コンピューターの構成] ダイアログボックスが表示されたら、[コンピューターのプロビジョニング] を選択し、[**デバッガーの設定**] を選択します。
3.  [**接続の種類**] で [ **USB**] を選択します。

    ![[接続の種類]、[ターゲット名]、[バスパラメーター] の各フィールドの値を含むデバッガー設定の例を示すスクリーンショット](images/setupusbvs.png)

    [**ターゲット名**] に、対象のコンピューターを表す文字列を入力します。 この文字列は、ターゲットコンピューターの正式な名前である必要はありません。次の制限を満たしている限り、任意の文字列を指定できます。

    -   文字列の最大長は24文字です。
    -   文字列内の文字は、ハイフン (-)、アンダースコア ( \_ )、0 ~ 9 の数字、および文字 A ~ Z (大文字または小文字) のみです。

    ターゲットコンピューターに複数の USB ホストコントローラーがある場合は、**バスパラメーター**値*b*を入力します。*d*。*f*( *b*、 *d*、 *f* ) は、ターゲットコンピューターでのデバッグに使用する USB ホストコントローラーのバス、デバイス、および関数の番号です。 バス、デバイス、および関数の数値は10進数形式にする必要があります (例: 48.0.0)。

4.  構成プロセスには数分かかり、対象のコンピューターが1回または2回自動的に再起動される場合があります。 プロセスが完了したら、[**完了**] をクリックします。

## <a name="span-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>ターゲットコンピューターの dbgsettings を確認しています


ターゲットコンピューターで、管理者としてコマンドプロンプトウィンドウを開き、次のコマンドを入力します。

**bcdedit/dbgsettings**

**bcdedit/enum**

```console
...
targetname              MyUsbTarget
debugtype               USB
debugport               1
baudrate                115200
...
busparams               48.0.0
```

*Debugtype*が USB で、 *targetname*がホストコンピューターの Visual Studio で指定した名前であることを確認します。 *Debugport*と*ボーレート*の値は無視できます。USB 経由のデバッグには適用されません。

Visual Studio で**バスパラメーター**を入力した場合は、指定したバスパラメーターと*busparams*が一致していることを確認します。

**バスパラメーター**に入力した値が表示されない場合は、次のコマンドを入力します。

**bcdedit/set "{dbgsettings}" busparams** <em>b</em>**。**<em>d</em>**。**<em>f</em>

ここで、 *b*、 *d*、および*f*は、デバッグに使用するように選択したターゲットコンピューター上の xHCI コントローラーのバス、デバイス、および関数の番号です。

例:

**bcdedit/set "{dbgsettings}" busparams 48.0.0**

ターゲット コンピューターを再起動します。

## <a name="span-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグセッションを開始する


1.  ユニバーサルシリアルバス (USB) 3.0 デバッグケーブルを、ホストとターゲットコンピュータでデバッグ用に選択した USB 3.0 ポートに接続します。
2.  ホストコンピューターで、管理者として Visual Studio を開きます。
3.  [**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
4.  [**トランスポート**] で、[ **Windows カーネルモードデバッガー**] を選択します。
5.  [**修飾子**] で、以前に構成したターゲットコンピューターの名前を選択します。
6.  **[アタッチ]** をクリックします。

この時点で、USB デバッグドライバーがホストコンピューターにインストールされます。 このため、Visual Studio を管理者として実行することが重要です。 USB デバッグドライバーをインストールした後は、以降のデバッグセッションで管理者として実行する必要はありません。

## <a name="span-idstarting_the_debugging_session_usb3_vsspanspan-idstarting_the_debugging_session_usb3_vsspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session_usb3_vs"></span><span id="STARTING_THE_DEBUGGING_SESSION_USB3_VS"></span>デバッグセッションの開始


1.  ホストコンピューターで、Visual Studio の [**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
2.  [**トランスポート**] で、[ **Windows カーネルモードデバッガー**] を選択します。
3.  [**修飾子**] で、以前に構成したターゲットコンピューターの名前を選択します。
4.  **[アタッチ]** をクリックします。

## <a name="span-idtroubleshooting_tips_for_debugging_over_usb_30spanspan-idtroubleshooting_tips_for_debugging_over_usb_30spantroubleshooting-tips-for-debugging-over-usb-30"></a><span id="troubleshooting_tips_for_debugging_over_usb_3.0"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_USB_3.0"></span>USB 3.0 でのデバッグに関するトラブルシューティングのヒント


場合によっては、電源切り替えが USB 3.0 でのデバッグに干渉することがあります。 この問題が発生した場合は、デバッグに使用している xHCI ホストコントローラー (およびそのルートハブ) のセレクティブサスペンドを無効にしてください。

1.  デバイスマネージャーで、xHCI ホストコントローラーのノードに移動します。 ノードを右クリックし、[**プロパティ**] を選択します。 [**電源管理**] タブが表示されている場合は、[電源管理を有効にする] チェックボックスをオフにし、[**コンピューターでこのデバイスの電源をオフにすることを許可**する] チェックボックスをオフにします。
2.  デバイスマネージャーで、xHCI ホストコントローラーのルートハブのノードに移動します。 ノードを右クリックし、[**プロパティ**] を選択します。 [**電源管理**] タブが表示されている場合は、[電源管理を有効にする] チェックボックスをオフにし、[**コンピューターでこのデバイスの電源をオフにすることを許可**する] チェックボックスをオフにします。

デバッグに xHCI host controller の使用が終了したら、xHCI ホストコントローラーのセレクティブサスペンドを有効にします。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグの設定](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






