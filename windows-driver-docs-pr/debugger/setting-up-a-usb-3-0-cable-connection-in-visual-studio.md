---
title: Visual Studio での USB 3.0 ケーブル経由でのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用して、設定し、USB 3.0 ケーブル経由でのカーネル モードのデバッグを実行することができます。
ms.assetid: F8DD0475-13CE-464A-A491-AEFA962A96DB
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: edf7742c8de8fdb4f7f09d7a7e5481915e529989
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366370"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-30-cable-in-visual-studio"></a>Visual Studio での USB 3.0 ケーブル経由でのカーネルモード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

Microsoft Visual Studio を使用して、設定し、USB 3.0 ケーブル経由でのカーネル モードのデバッグを実行することができます。 カーネル モードのデバッグを Visual Studio を使用するには、Windows Driver Kit (WDK) の Visual Studio と統合が必要です。 統合環境をインストールする方法については、次を参照してください。 [Windows ドライバー開発](https://go.microsoft.com/fwlink/p?linkid=301383)します。

Visual Studio を使用して、USB 3.0 のデバッグを設定する代わりに、セットアップを手動で行うことができます。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動で USB 3.0 ケーブル](setting-up-a-usb-3-0-debug-cable-connection.md)します。

デバッガーを実行しているコンピューターと呼ばれる、*ホスト コンピューター*とは、デバッグ中のコンピューターと呼びます、*対象のコンピュータ*します。

USB 3.0 接続経由でのデバッグには、次のハードウェアが必要です。

-   デバッグの USB 3.0 ケーブル。 これは、USB 3.0 行のみとありません Vbus を持つ、A クロス オーバー ケーブルです。

-   ホスト コンピューター (USB 3.0) の xHCI ホスト コント ローラーで

-   対象のコンピューターのデバッグをサポートしています (USB 3.0) の xHCI ホスト コント ローラー

## <a name="span-idsettingupthecomputerusb3manualspanspan-idsettingupthecomputerusb3manualspanidentifying-a-debug-port-on-the-target-computer"></a><span id="setting_up_the_computer_usb3_manual"></span><span id="SETTING_UP_THE_COMPUTER_USB3_MANUAL"></span>ターゲット コンピューターでデバッグ ポートを識別します。


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

5.  デバッグをサポートする xHCI コント ローラーを特定したら後、次の手順では、xHCI コント ローラー上のポートに関連付けられている物理 USB コネクタを検索します。 物理のコネクタを検索するには、ターゲット コンピューター上の任意の USB コネクタに任意の USB 3.0 デバイスを接続します。 デバイスが配置されている UsbView を更新します。 UsbView xHCI ホスト コント ローラーに接続されているデバイスが表示される場合は、USB 3.0 のデバッグに使用できる物理 USB コネクタを発見しました。

## <a name="span-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>ホストおよびターゲット コンピュータの構成


1.  」の説明に従って、ホストとターゲット コンピューターの構成を開始[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)します。
2.  Visual Studio で、ホスト コンピューターで、コンピューターの構成 ダイアログ ボックスのような場合が選択**コンピューターをプロビジョニングし、デバッガーの設定を選択**します。
3.  **接続の種類**、選択**USB**します。

    ![スクリーン ショットのデバッガーの例を次のフィールドの値の設定を示す: 接続の種類、ターゲットの名前、およびバス パラメーター](images/setupusbvs.png)

    **ターゲット名**、ターゲット コンピューターを表す文字列を入力します。 この文字列は、ターゲット コンピューターの正式な名前を指定する必要はありません。これらの制限を満たしている限り、作成した任意の文字列を指定できます。

    -   文字列の最大長は、24 文字です。
    -   文字列内の唯一の文字はアンダー スコア、ハイフン (-)、(\_)、0 ~ 9 の数字と文字 A ~ Z (大文字または小文字)。

    をターゲット コンピューターに 1 つ以上の USB ホスト コント ローラーがある場合は、入力、 **Bus パラメーター** @property *b*。*d*.*f*ここで、 *b*、 *d*、および*f*バス、デバイス、およびでデバッグするために使用する USB ホスト コント ローラーの番号を関数には対象のコンピュータ。 バス、デバイス、および関数の番号は 10 進数形式である必要があります (例。48.0.0).

4.  構成プロセスには数分かかりますが自動的に、コンピューターを再起動ターゲットまたは 2 回。 プロセスが完了したら、クリックして**完了**します。

## <a name="span-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>ターゲット コンピューター上の dbgsettings を確認しています


対象のコンピューターに管理者としてコマンド プロンプト ウィンドウを開きし、これらのコマンドを入力します。

**bcdedit /dbgsettings**

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

いることを確認*debugtype* usb と*targetname*ホスト コンピューターで Visual Studio で指定した名前を指定します。 値は無視してかまいません*debugport*と*baudrate*; USB 経由でのデバッグには適用されません。

入力した場合**Bus パラメーター** Visual Studio であることを確認*busparams*指定したバス パラメーターと一致します。

用に入力した値が表示されない場合**Bus パラメーター**、このコマンドを入力します。

**bcdedit /set "{dbgsettings}" busparams** <em>b</em> **.** <em>d</em> **.** <em>f</em>

場所*b*、 *d*、および*f*は、バス、デバイス、およびデバッグに使用する、選択したターゲット コンピューター上の xHCI コント ローラーの関数の数。

以下に例を示します。

**bcdedit /set "{dbgsettings}" busparams 48.0.0**

ターゲット コンピューターを再起動します。

## <a name="span-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグ セッションの開始


1.  ユニバーサル シリアル バス (USB) 3.0 デバッグ ケーブルをホストとターゲット コンピューターでデバッグするため、選択した USB 3.0 ポートに接続します。
2.  ホスト コンピューターには、管理者として Visual Studio を開きます。
3.  **ツール**] メニューの [選択**プロセスにアタッチ**します。
4.  **トランスポート**、選択**Windows カーネル モードのデバッガー**します。
5.  **修飾子**、以前に構成されているターゲット コンピューターの名前を選択します。
6.  クリックして**アタッチ**します。

この時点では、USB デバッグのドライバーは、ホスト コンピューターにインストールを取得します。 これは、ため、Visual Studio を管理者として実行することが重要です。 USB デバッグ ドライバーがインストールされた後、後続のデバッグ セッションを管理者として実行する必要はありません。

## <a name="span-idstartingthedebuggingsessionusb3vsspanspan-idstartingthedebuggingsessionusb3vsspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session_usb3_vs"></span><span id="STARTING_THE_DEBUGGING_SESSION_USB3_VS"></span>デバッグ セッションの開始


1.  Visual Studio で、ホスト コンピューター上で、**ツール**] メニューの [選択**プロセスにアタッチ**します。
2.  **トランスポート**、選択**Windows カーネル モードのデバッガー**します。
3.  **修飾子**、以前に構成されているターゲット コンピューターの名前を選択します。
4.  クリックして**アタッチ**します。

## <a name="span-idtroubleshootingtipsfordebuggingoverusb30spanspan-idtroubleshootingtipsfordebuggingoverusb30spantroubleshooting-tips-for-debugging-over-usb-30"></a><span id="troubleshooting_tips_for_debugging_over_usb_3.0"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_USB_3.0"></span>USB 3.0 経由でのデバッグのトラブルシューティングのヒント


場合によっては、電源遷移できる USB 3.0 経由でのデバッグに干渉することです。 この問題は、選択的に無効にした場合は、デバッグを使用している xHCI ホスト コント ローラー (とそのルート ハブ) を中断します。

1.  デバイス マネージャーでは、xHCI ホスト コント ローラーのノードに移動します。 ノードを右クリックし、選択**プロパティ**します。 ある場合、**電源管理**タブ、タブを開き、オフ、**電力を節約するには、このデバイスを無効にするコンピューターを許可する**チェック ボックスをオンします。
2.  デバイス マネージャーでは、xHCI ホスト コント ローラーのルート ハブのノードに移動します。 ノードを右クリックし、選択**プロパティ**します。 ある場合、**電源管理**タブ、タブを開き、オフ、**電力を節約するには、このデバイスを無効にするコンピューターを許可する**チェック ボックスをオンします。

XHCI ホスト コント ローラーを使用して、デバッグが完了したら、有効にするオプションを選択は、xHCI ホスト コント ローラーを中断します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグの設定](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






