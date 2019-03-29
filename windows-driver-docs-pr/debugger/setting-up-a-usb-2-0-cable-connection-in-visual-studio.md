---
title: Visual Studio での USB 2.0 ケーブル経由でのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用して、設定し、USB 2.0 ケーブル経由でのカーネル モードのデバッグを実行することができます。
ms.assetid: 3BEE43E2-32E5-4E7A-BA71-9ADB224578B1
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: a2ced2f82a8893a000ca0e328e72f019eaf34125
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579795"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-20-cable-in-visual-studio"></a>Visual Studio での USB 2.0 ケーブル経由でのカーネルモード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

Microsoft Visual Studio を使用して、設定し、USB 2.0 ケーブル経由でのカーネル モードのデバッグを実行することができます。 カーネル モードのデバッグを Visual Studio を使用するには、Windows Driver Kit (WDK) の Visual Studio と統合が必要です。 統合環境をインストールする方法については、次を参照してください。 [Windows ドライバー開発](https://go.microsoft.com/fwlink/p?linkid=301383)します。

Visual Studio を使用して USB 2.0 のデバッグを設定する代わりに、セットアップを手動で行うことができます。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動で USB 2.0 ケーブル](setting-up-a-usb-2-0-debug-cable-connection.md)します。

デバッガーを実行しているコンピューターと呼ばれる、*ホスト コンピューター*とは、デバッグ中のコンピューターと呼びます、*対象のコンピュータ*します。

USB 2.0 接続経由でのデバッグには、次のハードウェアが必要です。

-   ユニバーサル シリアル バス (USB) 2.0 デバッグ ケーブル。 USB2 デバッグ デバイス機能仕様と互換性のあるようにする追加のハードウェア コンポーネントがあるために、このケーブルは、標準の USB 2.0 ケーブルではありません。 「USB 2.0 デバッグ ケーブル」のインターネットを検索してこれらのケーブルが見つかります。

-   ホスト コンピューター (USB 2.0) EHCI ホスト コント ローラーで

-   対象のコンピューターのデバッグをサポートしています (USB 2.0) EHCI ホスト コント ローラー

## <a name="span-ididentifyingadebugportonthetargetcomputerspanspan-ididentifyingadebugportonthetargetcomputerspanspan-ididentifyingadebugportonthetargetcomputerspanidentifying-a-debug-port-on-the-target-computer"></a><span id="Identifying_a_Debug_Port_on_the_Target_Computer"></span><span id="identifying_a_debug_port_on_the_target_computer"></span><span id="IDENTIFYING_A_DEBUG_PORT_ON_THE_TARGET_COMPUTER"></span>ターゲット コンピューターでデバッグ ポートを識別します。


1.  対象のコンピューターに UsbView ツールを起動します。 Windows ツールのデバッグにはに UsbView ツールが含まれます。
2.  UsbView、EHCI 仕様と互換性があるホスト コント ローラーのすべてを見つけます。 たとえば、拡張としてリストされているコント ローラーを検索する可能性があります。
3.  UsbView、EHCI ホスト コント ローラーのノードを展開します。 ホスト コント ローラーがデバッグするをサポートしていることを示す値を検索し、デバッグ ポートの番号を探します。 たとえば、UsbView EHCI ホスト コント ローラー 1 のポートでのデバッグをサポートするためには、この出力を表示します。

    ```console
    Xxx xxx xxx USB2 Enhanced Host Controller - 293A
    ...
    Debug Port Number:  1
    Bus.Device.Function (in decimal): 0.29.7
    ```

    **注**  多く EHCI ホスト コント ローラーは、EHCI ホスト コント ローラーが、1 は、ポート 2 でのデバッグをサポートするポートでのデバッグをサポートします。

     

4.  デバッグに使用する、EHCI コント ローラーには、バス、デバイス、および関数の番号をメモしてをおきます。 UsbView には、これらの数が表示されます。 前の例では、バス番号は 0、デバイス番号は 29、および関数の数は 7 です。

5.  EHCI コント ローラーとデバッグをサポートしているポート番号を特定したら後、次の手順では、正しいポート番号に関連付けられている物理 USB コネクタを検索します。 物理のコネクタを検索するには、ターゲット コンピューター上の任意の USB コネクタに任意の USB 2.0 デバイスを接続します。 デバイスが配置されている UsbView を更新します。 UsbView EHCI ホスト コント ローラーとデバッグ ポートとして指定したポートに接続されているデバイスが表示される場合は、デバッグに使用できる物理 USB コネクタを発見しました。 EHCI コント ローラー上のデバッグ ポートに関連付けられている外部の物理 USB コネクタが存在しない可能性があります。 その場合は、コンピューター内の物理的な USB コネクタ検索することができます。 内部の USB コネクタはカーネル デバッグに適しているかどうかを判断するのと同じ手順を実行します。 物理的な USB コネクタが見つからない場合、デバッグ ポートに関連付けられている (外部または内部) し、USB 2.0 ケーブル経由のデバッグ ターゲットとして、コンピューターを使用することはできません。

    **注**  を参照してください[この注釈](setting-up-a-usb-2-0-debug-cable-connection.md#what-if-usbview-shows-a-debug-capable-port)例外。

     

## <a name="span-idconnectingtheusbdebugcablespanspan-idconnectingtheusbdebugcablespanspan-idconnectingtheusbdebugcablespanconnecting-the-usb-debug-cable"></a><span id="Connecting_the_USB_debug_cable"></span><span id="connecting_the_usb_debug_cable"></span><span id="CONNECTING_THE_USB_DEBUG_CABLE"></span>USB デバッグ ケーブルの接続


1.  USB デバッグのターゲットにするのには、ホスト コンピューターが構成されていないことを確認します。 (必要に応じて、管理者としてコマンド プロンプト ウィンドウを開き、入力**オフ bcdedit/debug**、し、再起動します)。
2.  ホスト コンピューターには、EHCI ホスト コント ローラーとデバッグをサポートするポートを検索するのに UsbView を使用します。 可能であれば、デバッグをサポートしていない (ホスト コンピューター) 上の EHCI ポートに USB 2.0 のデバッグ ケーブルの一端を差し込みます。 それ以外の場合、ホスト コンピューター上の任意の EHCI ポートにケーブルを接続します。
3.  ターゲット コンピューターの前に特定したコネクタに USB 2.0 デバッグ ケーブルのもう一方の端を差し込みます。

## <a name="span-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>ホストおよびターゲット コンピュータの構成


1.  」の説明に従って、ホストとターゲット コンピューターの構成を開始[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)します。
2.  Visual Studio で、ホスト コンピューターで、コンピューターの構成 ダイアログ ボックスのような場合が選択**コンピューターをプロビジョニングし、デバッガーの設定を選択**します。
3.  **接続の種類**、選択**USB**します。

    ![スクリーン ショットのデバッガーの例を次のフィールドの値の設定を示す: 接続の種類、ターゲットの名前、およびバス パラメーター](images/setupusb2vs.png)

    **ターゲット名**、ターゲット コンピューターを表す文字列を入力します。 この文字列は、ターゲット コンピューターの正式な名前を指定する必要はありません。これらの制限を満たしている限り、作成した任意の文字列を指定できます。

    -   文字列の最大長は、24 文字です。
    -   文字列内の唯一の文字はアンダー スコア、ハイフン (-)、(\_)、0 ~ 9 の数字と文字 A ~ Z (大文字または小文字)。

    をターゲット コンピューターに 1 つ以上の USB ホスト コント ローラーがある場合は、入力、 **Bus パラメーター** @property *b*。*d*.*f*ここで、 *b*、 *d*、および*f*バス、デバイス、およびでデバッグするために使用する USB ホスト コント ローラーの番号を関数には対象のコンピュータ。 バス、デバイス、および関数の番号は 10 進数形式である必要があります (例。0.29.7).

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
busparams               0.29.7
...
```

いることを確認*debugtype* usb と*targetname*ホスト コンピューターで Visual Studio で指定した名前を指定します。 値は無視してかまいません*debugport*と*baudrate*; USB 経由でのデバッグには適用されません。

入力した場合**Bus パラメーター** Visual Studio であることを確認*busparams*指定したバス パラメーターと一致します。

用に入力した値が表示されない場合**Bus パラメーター**、このコマンドを入力します。

**bcdedit /set "{dbgsettings}" busparams** <em>b</em>**.**<em>d</em>**.**<em>f</em>

場所*b*、 *d*、および*f*は、バス、デバイス、およびデバッグに使用する、選択したターゲット コンピューター上の EHCI コント ローラーの関数の数。

例:

**bcdedit /set "{dbgsettings}" busparams 0.29.7**

ターゲット コンピューターを再起動します。

## <a name="span-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグ セッションの開始


1.  ホストおよびターゲット コンピューターでデバッグするため、選択した USB 2.0 ポートに USB 2.0 デバッグ ケーブルを接続します。
2.  ホスト コンピューターには、管理者として Visual Studio を開きます。
3.  **ツール**] メニューの [選択**プロセスにアタッチ**します。
4.  **トランスポート**、選択**Windows カーネル モードのデバッガー**します。
5.  **修飾子**、以前に構成されているターゲット コンピューターの名前を選択します。
6.  クリックして**アタッチ**します。

この時点では、USB デバッグのドライバーは、ホスト コンピューターにインストールを取得します。 これは、ため、Visual Studio を管理者として実行することが重要です。 USB デバッグ ドライバーがインストールされた後、後続のデバッグ セッションを管理者として実行する必要はありません。

## <a name="span-idstartingadebuggingsessionspanspan-idstartingadebuggingsessionspanspan-idstartingadebuggingsessionspanstarting-a-debugging-session"></a><span id="Starting_a_Debugging_Session"></span><span id="starting_a_debugging_session"></span><span id="STARTING_A_DEBUGGING_SESSION"></span>デバッグ セッションの開始


1.  Visual Studio で、ホスト コンピューター上で、**ツール**] メニューの [選択**プロセスにアタッチ**します。
2.  **トランスポート**、選択**Windows カーネル モードのデバッガー**します。
3.  **修飾子**構成中に入力したターゲットの名前を選択します。
4.  クリックして**アタッチ**します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグの設定](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






