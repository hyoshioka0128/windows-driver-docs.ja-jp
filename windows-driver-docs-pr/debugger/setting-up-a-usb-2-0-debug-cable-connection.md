---
title: カーネル モード経由でのデバッグ、USB 2.0 ケーブル手動での設定
description: デバッグ ツールの Windows カーネルが USB 2.0 ケーブル経由でデバッグをサポートします。 このトピックでは、USB 2.0 を手動でのデバッグを設定する方法について説明します。
ms.assetid: 8dd0703a-ddcd-461f-b164-1c079a93bb3a
keywords:
- USB 2.0 ケーブルの接続のセットアップ
- USB 2.0 デバッグ ケーブル、ケーブル接続
- USB 2.0 デバッグ接続
- USB 2.0 接続をデバッグ、ハードウェアの設定
- USB 2.0 のデバッグ接続、ソフトウェアの要件
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: b22f16ceaec12ebec4d0f5fc5d72f44e6eeac8b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528360"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-20-cable-manually"></a>カーネル モード経由でのデバッグ、USB 2.0 ケーブル手動での設定


デバッグ ツールの Windows カーネルが USB 2.0 ケーブル経由でデバッグをサポートします。 このトピックでは、USB 2.0 を手動でのデバッグを設定する方法について説明します。

デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*対象のコンピュータ*します。

USB 2.0 ケーブル経由でのデバッグには、次のハードウェアが必要です。

-   デバッグの USB 2.0 ケーブル。 USB2 デバッグ デバイス機能仕様と互換性のあるようにする追加のハードウェア コンポーネントがあるために、このケーブルは、標準の USB 2.0 ケーブルではありません。 これらのケーブル インターネット検索用語の使用を検索する*2.0 の USB デバッグ ケーブル*します。

-   ホスト コンピューター (USB 2.0) EHCI ホスト コント ローラーで

-   対象のコンピューターのデバッグをサポートしています (USB 2.0) EHCI ホスト コント ローラー

## <a name="span-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspansetting-up-the-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>ターゲット コンピューターをセットアップします。


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

    **注**  を参照してください[この注釈](#what-if-usbview-shows-a-debug-capable-port)例外。

> [!IMPORTANT]
> Bcdedit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。 セキュア ブートは、再度有効に完了したらとデバッグは無効になりましたカーネル デバッグします。  

   

6. 対象のコンピューターに管理者としてコマンド プロンプト ウィンドウを開きし、これらのコマンドを入力します。

   - **bcdedit /debug on**
   - **bcdedit/dbgsettings usb targetname:**<em>TargetName</em>

   場所*TargetName*対象のコンピュータ用に作成した名前を指定します。 なお*TargetName*対象のコンピュータの正式な名前を指定する必要はありませんこれらの制限を満たしている限り、作成した任意の文字列にすることができます。

   -   文字列の最大長は、24 文字です。
   -   文字列内の唯一の文字はアンダー スコア、ハイフン (-)、(\_)、0 ~ 9 の数字と文字 A ~ Z (大文字または小文字)。

7. ターゲット コンピューターに 1 つ以上の USB ホスト コント ローラーがある場合は、このコマンドを入力します。

   <span id="Windows_7_or_later"></span><span id="windows_7_or_later"></span><span id="WINDOWS_7_OR_LATER"></span>Windows 7 以降  
   **bcdedit /set "{dbgsettings}" busparams** *b.d.f*

   場所*b*、 *d*、および*f*バス、デバイス、およびホスト コント ローラーの関数の番号。 バス、デバイス、および関数の番号は 10 進数形式である必要があります (たとえば、 **busparams 0.29.7**)。

   <span id="Windows_Vista"></span><span id="windows_vista"></span><span id="WINDOWS_VISTA"></span>Windows Vista  
   **bcdedit /set "{current}" loadoptions busparams=**<em>f.d.f</em>

   場所*b*、 *d*、および*f*バス、デバイス、およびホスト コント ローラーの関数の番号。 バス、デバイス、および関数の数値を 16 進形式である必要があります (たとえば、 **busparams = 0.1 D. 7**)。

8. ターゲット コンピューターを再起動します。

## <a name="span-idsetting-up-the-host-computerspanspan-idsettingupthehostcomputerspanspan-idsettingupthehostcomputerspansetting-up-the-host-computer"></a><span id="Setting-Up-the-Host-Computer"></span><span id="setting_up_the_host_computer"></span><span id="SETTING_UP_THE_HOST_COMPUTER"></span>ホスト コンピューターをセットアップします。


1.  USB デバッグのターゲットにするのには、ホスト コンピューターが構成されていないことを確認します。 (必要に応じて、管理者としてコマンド プロンプト ウィンドウを開き、入力**オフ bcdedit/debug**、し、再起動します)。
2.  ホスト コンピューターには、EHCI ホスト コント ローラーとデバッグをサポートするポートを検索するのに UsbView を使用します。 可能であれば、デバッグをサポートしていない (ホスト コンピューター) 上の EHCI ポートに USB 2.0 のデバッグ ケーブルの一端を差し込みます。 それ以外の場合、ホスト コンピューター上の任意の EHCI ポートにケーブルを接続します。
3.  ターゲット コンピューターの前に特定したコネクタに USB 2.0 デバッグ ケーブルのもう一方の端を差し込みます。

## <a name="span-idstarting-a-debugging-session-for-the-first-timespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting-a-Debugging-Session-for-the-First-Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>初めてデバッグ セッションの開始


1.  ホスト コンピューターで実行されている Windows のビット数 (32 ビットまたは 64 ビット) を決定します。
2.  ホスト コンピューターでは、ホスト コンピューターで実行されている Windows のビット数に一致する (管理者) として WinDbg のバージョンが開きます。 たとえば、ホスト コンピューターで Windows の 64 ビット版が実行されている場合は、管理者として WinDbg の 64 ビット バージョンを開きます。
3.  **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、 **USB**タブ。ターゲット コンピューターをセットアップするときに作成したターゲットの名前を入力します。 **[OK]** をクリックします。

この時点では、USB デバッグのドライバーは、ホスト コンピューターにインストールを取得します。 これは、ため、Windows のビット数に WinDbg のビット数と一致することが重要です。 USB デバッグ ドライバーがインストールされた後は、後続のデバッグ セッション WinDbg の 32 ビットまたは 64 ビット バージョンのいずれかを使用できます。

**注**  USB 2.0 デバッグ ケーブルが途中でドングルを実際に 2 本のケーブル。 ドングルの方向は重要です。一方の側が、デバイスを補強し、もう一方の側はありません。 USB デバッグが機能しない場合は、ドングルの方向をスワップしてみます。 つまり、ドングルから両方のケーブルを取り外します、辺に、ケーブルが接続されているをスワップします。

 

## <a name="span-idstarting-a-debugging-sessionspanspan-idstartingadebuggingsessionspanspan-idstartingadebuggingsessionspanstarting-a-debugging-session"></a><span id="Starting-a-Debugging-Session"></span><span id="starting_a_debugging_session"></span><span id="STARTING_A_DEBUGGING_SESSION"></span>デバッグ セッションの開始


### <a name="span-idusing-windbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using-WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg を使用します。

ホスト コンピューターでは、WinDbg を開きます。 **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、 **USB**タブ。ターゲット コンピューターをセットアップするときに作成したターゲットの名前を入力します。 **[OK]** をクリックします。

コマンド プロンプト ウィンドウで、次のコマンドを入力して、WinDbg でセッションを開始することもできます、 *TargetName*はターゲット コンピューターをセットアップするときに作成したターゲットの名前です。

**windbg /k usb:targetname=**<em>TargetName</em>

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD を使用します。

ホスト コンピューターでは、コマンド プロンプト ウィンドウを開き、次のコマンドを入力して、 *TargetName*はターゲット コンピューターをセットアップするときに作成したターゲット名です。

**kd /k usb:targetname=**<em>TargetName</em>

## <a name="span-idwhat-if-usbview-shows-a-debug-capable-portspanspan-idwhatifusbviewshowsadebugcapableportspanwhat-if-usbview-shows-a-debug-capable-port-but-does-not-show-the-port-mapped-to-any-physical-connector"></a><span id="what-if-usbview-shows-a-debug-capable-port"></span><span id="WHAT_IF_USBVIEW_SHOWS_A_DEBUG_CAPABLE_PORT"></span>USBView がデバッグ対応のポートを示していますが、物理コネクタにマップされているポートが表示されない場合ですか。


一部のコンピューターでは、USBView がデバッグ対応のポートを示していますが、物理的な USB コネクタにマップされているポートは表示されません。 たとえば、USBView は eHCI コント ローラーのデバッグ ポート番号としてポート 2 を表示する可能性があります。

```console
... USB Enhanced Host Controller ...
...
Debug Port Number:  2
Bus.Device.Function (in decimal): 0.29.0
```

また、USBView を使用して、個々 のポートを確認すると、デバッグ対応として表示されます。

```console
[Port 2]
Is Port User Connectiable: Yes
Is Port Debug Capable: Yes
...
Protocols Supported
  USB 1.1      yes
  USB 2.0      yes
  USB 3.0      no
```

USBView デバッグできるポート (この例ではポート 2) に接続されているデバイス (フラッシュ ドライブ) のように、コンピューター上のすべての USB コネクタに USB 2.0 デバイスを接続するときに表示しません。 USBView は eHCI コント ローラーのデバッグに対応したポートに、外部のコネクタが実際にマップされている場合は、xHCI コント ローラーのポートにマップされている外部コネクタを表示する場合があります。

![xhci と usbview で ehci のスクリーン ショット](images/usbview01.png)

このような場合は、カーネル モードの USB 2.0 ケーブル経由でのデバッグを確立することがある可能性があります。 ここに示す例では、xHCI コント ローラーのポート 2 にマップされていると表示されるコネクタに、USB 2.0 デバッグ ケーブルを接続します。 バス、デバイス、および関数の数 (この例では、0.29.0) では eHCI コント ローラーに、バス パラメーターを設定します。

**bcdedit /set "{dbgsettings}" busparams 0.29.0**

### <a name="span-idsoftware-setupspanspan-idsoftwaresetupspanadditional-support"></a><span id="software-setup"></span><span id="SOFTWARE_SETUP"></span>その他のサポート

トラブルシューティングのヒントとカーネルが USB 経由でデバッグの設定の詳細については、[カーネル デバッグのセットアップと USB 2.0](https://go.microsoft.com/fwlink/p?linkid=389435)を参照してください。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[カーネル モードのデバッグを手動での設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






