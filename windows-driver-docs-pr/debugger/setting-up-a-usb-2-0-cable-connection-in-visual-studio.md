---
title: Visual Studio での USB 2.0 ケーブル経由でのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用して、USB 2.0 ケーブルでカーネルモードのデバッグを設定し、実行することができます。
ms.assetid: 3BEE43E2-32E5-4E7A-BA71-9ADB224578B1
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 214ecc93d865ed13aff379f5764135a3f600280a
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533911"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-20-cable-in-visual-studio"></a>Visual Studio での USB 2.0 ケーブル経由でのカーネルモード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>

Microsoft Visual Studio を使用して、USB 2.0 ケーブルでカーネルモードのデバッグを設定し、実行することができます。 Visual Studio を使用してカーネルモードのデバッグを行うには、Visual Studio に Windows Driver Kit (WDK) が統合されている必要があります。 統合環境をインストールする方法の詳細については、「 [Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)」を参照してください。

Visual Studio を使用して USB 2.0 デバッグを設定する代わりに、手動でセットアップを行うこともできます。 詳細については、「 [USB 2.0 ケーブル経由でカーネルモードのデバッグを手動で設定する](setting-up-a-usb-2-0-debug-cable-connection.md)」を参照してください。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ対象のコンピューターは*ターゲットコンピューター*と呼ばれます。

USB 2.0 接続でのデバッグには、次のハードウェアが必要です。

-   ユニバーサルシリアルバス (USB) 2.0 デバッグケーブル。 このケーブルは、USB2 デバッグデバイスの機能仕様と互換性のある追加のハードウェアコンポーネントがあるため、標準の USB 2.0 ケーブルではありません。 これらのケーブルは、インターネット検索で "USB 2.0 デバッグケーブル" を使用して見つけることができます。

-   ホストコンピューターの EHCI (USB 2.0) ホストコントローラー

-   ターゲットコンピューターで、デバッグをサポートする EHCI (USB 2.0) ホストコントローラー

## <a name="span-ididentifying_a_debug_port_on_the_target_computerspanspan-ididentifying_a_debug_port_on_the_target_computerspanspan-ididentifying_a_debug_port_on_the_target_computerspanidentifying-a-debug-port-on-the-target-computer"></a><span id="Identifying_a_Debug_Port_on_the_Target_Computer"></span><span id="identifying_a_debug_port_on_the_target_computer"></span><span id="IDENTIFYING_A_DEBUG_PORT_ON_THE_TARGET_COMPUTER"></span>ターゲットコンピューターでのデバッグポートの識別


1.  ターゲットコンピューターで、UsbView ツールを起動します。 UsbView ツールは、Windows 用デバッグツールに含まれています。
2.  [UsbView] で、EHCI 仕様と互換性のあるすべてのホストコントローラーを見つけます。 たとえば、"Enhanced" と表示されているコントローラーを探すことができます。
3.  [UsbView] で、EHCI ホストコントローラーのノードを展開します。 ホストコントローラーがデバッグをサポートしていることを確認し、デバッグポートの番号を探します。 たとえば、[UsbView] を使用すると、ポート1でのデバッグをサポートする EHCI ホストコントローラーのこの出力が表示されます。

    ```console
    Xxx xxx xxx USB2 Enhanced Host Controller - 293A
    ...
    Debug Port Number:  1
    Bus.Device.Function (in decimal): 0.29.7
    ```

    **メモ**   多くの EHCI ホストコントローラーはポート1でのデバッグをサポートしていますが、一部の EHCI ホストコントローラーではポート2でのデバッグがサポートされています。

     

4.  デバッグに使用する EHCI コントローラーのバス、デバイス、および関数の番号をメモしておきます。 UsbView には、これらの数値が表示されます。 前の例では、バス番号は0、デバイス番号は29、関数番号は7です。

5.  EHCI コントローラーと、デバッグをサポートするポート番号を特定したら、次の手順では、正しいポート番号に関連付けられている物理 USB コネクタを見つけます。 物理コネクタを見つけるには、任意の USB 2.0 デバイスをターゲットコンピューター上の任意の USB コネクタに接続します。 UsbView を更新して、デバイスが配置されている場所を確認します。 [UsbView] に、デバッグポートとして指定した EHCI ホストコントローラーとポートに接続しているデバイスが表示されている場合は、デバッグに使用できる物理 USB コネクタがあります。 EHCI コントローラーのデバッグポートに関連付けられている外部の物理 USB コネクタがない可能性があります。 その場合は、コンピューター内で物理 USB コネクタを探すことができます。 内部 USB コネクタがカーネルデバッグに適しているかどうかを判断するには、同じ手順を実行します。 デバッグポートに関連付けられている物理 USB コネクタ (外部または内部) が見つからない場合は、そのコンピューターを USB 2.0 ケーブルでデバッグするためのターゲットとして使用することはできません。

    **メモ**   例外については、[このコメント](setting-up-a-usb-2-0-debug-cable-connection.md#what-if-usbview-shows-a-debug-capable-port)を参照してください。

     

## <a name="span-idconnecting_the_usb_debug_cablespanspan-idconnecting_the_usb_debug_cablespanspan-idconnecting_the_usb_debug_cablespanconnecting-the-usb-debug-cable"></a><span id="Connecting_the_USB_debug_cable"></span><span id="connecting_the_usb_debug_cable"></span><span id="CONNECTING_THE_USB_DEBUG_CABLE"></span>USB デバッグケーブルの接続


1.  ホストコンピューターが、USB デバッグのターゲットとなるように構成されていないことを確認します。 (必要に応じて、管理者としてコマンドプロンプトウィンドウを開き、「 **bcdedit/debug off**」と入力して再起動します)。
2.  ホストコンピューターで、[UsbView] を使用して、デバッグをサポートする EHCI ホストコントローラーとポートを検索します。 可能であれば、USB 2.0 デバッグケーブルの一端を、デバッグをサポートしていない EHCI ポート (ホストコンピューター上) に接続します。 それ以外の場合は、ホストコンピューターの任意の EHCI ポートにケーブルを接続します。
3.  USB 2.0 デバッグケーブルのもう一方の端を、ターゲットコンピューターで以前に特定したコネクタに接続します。

## <a name="span-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>ホストとターゲットコンピューターの構成


1.  「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の説明に従って、ホストとターゲットコンピューターの構成を開始します。
2.  ホストコンピューターの Visual Studio で、[コンピューターの構成] ダイアログボックスが表示されたら、[コンピューターのプロビジョニング] を選択し、[**デバッガーの設定**] を選択します。
3.  [**接続の種類**] で [ **USB**] を選択します。

    ![[接続の種類]、[ターゲット名]、[バスパラメーター] の各フィールドの値を含むデバッガー設定の例を示すスクリーンショット](images/setupusb2vs.png)

    [**ターゲット名**] に、対象のコンピューターを表す文字列を入力します。 この文字列は、ターゲットコンピューターの正式な名前である必要はありません。次の制限を満たしている限り、任意の文字列を指定できます。

    -   文字列の最大長は24文字です。
    -   文字列内の文字は、ハイフン (-)、アンダースコア ( \_ )、0 ~ 9 の数字、および文字 A ~ Z (大文字または小文字) のみです。

    ターゲットコンピューターに複数の USB ホストコントローラーがある場合は、**バスパラメーター**値*b*を入力します。*d*。*f*( *b*、 *d*、 *f* ) は、ターゲットコンピューターでのデバッグに使用する USB ホストコントローラーのバス、デバイス、および関数の番号です。 バス、デバイス、および関数の数値は10進数形式にする必要があります (例: 0.29.7)。

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
busparams               0.29.7
...
```

*Debugtype*が USB で、 *targetname*がホストコンピューターの Visual Studio で指定した名前であることを確認します。 *Debugport*と*ボーレート*の値は無視できます。USB 経由のデバッグには適用されません。

Visual Studio で**バスパラメーター**を入力した場合は、指定したバスパラメーターと*busparams*が一致していることを確認します。

**バスパラメーター**に入力した値が表示されない場合は、次のコマンドを入力します。

**bcdedit/set "{dbgsettings}" busparams** <em>b</em>**。**<em>d</em>**。**<em>f</em>

ここで、 *b*、 *d*、および*f*は、デバッグに使用することを選択したターゲットコンピューター上の EHCI コントローラーのバス、デバイス、および関数の番号です。

例:

**bcdedit/set "{dbgsettings}" busparams 0.29.7**

ターゲット コンピューターを再起動します。

## <a name="span-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグセッションを開始する


1.  USB 2.0 デバッグケーブルを、ホストとターゲットコンピュータでデバッグ用に選択した USB 2.0 ポートに接続します。
2.  ホストコンピューターで、管理者として Visual Studio を開きます。
3.  [**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
4.  [**トランスポート**] で、[ **Windows カーネルモードデバッガー**] を選択します。
5.  [**修飾子**] で、以前に構成したターゲットコンピューターの名前を選択します。
6.  **[アタッチ]** をクリックします。

この時点で、USB デバッグドライバーがホストコンピューターにインストールされます。 このため、Visual Studio を管理者として実行することが重要です。 USB デバッグドライバーをインストールした後は、以降のデバッグセッションで管理者として実行する必要はありません。

## <a name="span-idstarting_a_debugging_sessionspanspan-idstarting_a_debugging_sessionspanspan-idstarting_a_debugging_sessionspanstarting-a-debugging-session"></a><span id="Starting_a_Debugging_Session"></span><span id="starting_a_debugging_session"></span><span id="STARTING_A_DEBUGGING_SESSION"></span>デバッグセッションの開始


1.  ホストコンピューターで、Visual Studio の [**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
2.  [**トランスポート**] で、[ **Windows カーネルモードデバッガー**] を選択します。
3.  [**修飾子**] で、構成中に入力したターゲット名を選択します。
4.  **[アタッチ]** をクリックします。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグの設定](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






