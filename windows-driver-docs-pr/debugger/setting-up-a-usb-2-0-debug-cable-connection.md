---
title: USB 2.0 ケーブルを経由のカーネルモード デバッグの手動設定
description: Windows 用デバッグツールは、USB 2.0 ケーブルでのカーネルデバッグをサポートしています。 このトピックでは、USB 2.0 デバッグを手動で設定する方法について説明します。
ms.assetid: 8dd0703a-ddcd-461f-b164-1c079a93bb3a
keywords:
- セットアップ、USB 2.0 ケーブル接続の確立
- ケーブル接続、USB 2.0 デバッグケーブル
- USB 2.0 デバッグ接続
- USB 2.0 接続のデバッグ、ハードウェアの設定
- USB 2.0 デバッグ接続、ソフトウェア要件
ms.date: 02/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: d796a1fb9bb99d8f0684c916bcf1e8c4204222d1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534765"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-20-cable-manually"></a>USB 2.0 ケーブルを経由のカーネルモード デバッグの手動設定


Windows 用デバッグツールは、USB 2.0 ケーブルでのカーネルデバッグをサポートしています。 このトピックでは、USB 2.0 デバッグを手動で設定する方法について説明します。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。

USB 2.0 ケーブルでのデバッグには、次のハードウェアが必要です。

-   USB 2.0 デバッグケーブル。 このケーブルは、USB2 デバッグデバイスの機能仕様と互換性のある追加のハードウェアコンポーネントがあるため、標準の USB 2.0 ケーブルではありません。 これらのケーブルは、 *USB 2.0 デバッグケーブル*のインターネット検索で検索できます。

-   ホストコンピューターの EHCI (USB 2.0) ホストコントローラー

-   ターゲットコンピューターで、デバッグをサポートする EHCI (USB 2.0) ホストコントローラー

## <a name="setting-up-the-target-computer"></a>ターゲットコンピューターのセットアップ


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

    **メモ**   例外については、[このコメント](#what-if-usbview-shows-a-debug-capable-port)を参照してください。

> [!IMPORTANT]
> Bcdedit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。 デバッグが完了し、カーネルデバッグを無効にした後、セキュアブートを再度有効にすることができます。  

6. ターゲットコンピューターで、管理者としてコマンドプロンプトウィンドウを開き、次のコマンドを入力します。

   - **bcdedit/debug on**
   - **bcdedit/dbgsettings usb targetname:**<em>targetname</em>

   *TargetName*はターゲットコンピューター用に作成する名前です。 *TargetName*はターゲットコンピューターの正式な名前である必要はないことに注意してください。次の制限を満たしている限り、任意の文字列を指定できます。

   -   文字列では、大文字と小文字の組み合わせで*TargetName*内の任意の場所に "debug" を含めることはできません。 たとえば、targetname 内の任意の場所で "DeBuG" または "DEBUG" を使用すると、デバッグは正しく機能しません。  
   -   文字列内の文字は、ハイフン (-)、アンダースコア ( \_ )、0 ~ 9 の数字、および文字 A ~ Z (大文字または小文字) のみです。
   -   文字列の最大長は24文字です。

7. ターゲットコンピューターに複数の USB ホストコントローラーがある場合は、次のコマンドを入力します。

   <span id="Windows_7_or_later"></span><span id="windows_7_or_later"></span><span id="WINDOWS_7_OR_LATER"></span>Windows 7 以降  
   **bcdedit/set "{dbgsettings}" busparams** *b. d. f*

   ここで、 *b*、 *d*、および*f*は、ホストコントローラーのバス、デバイス、および関数の番号です。 バス、デバイス、および関数の数値は、10進形式 ( **busparams 0.29.7**など) である必要があります。

   <span id="Windows_Vista"></span><span id="windows_vista"></span><span id="WINDOWS_VISTA"></span>Windows Vista  
   **bcdedit/set "{current}" loadoptions busparams =**<em>f. d. f</em>

   ここで、 *b*、 *d*、および*f*は、ホストコントローラーのバス、デバイス、および関数の番号です。 バス、デバイス、および関数の番号は16進形式である必要があります (例: **busparams = 0.1 d. 7**)。

8. ターゲット コンピューターを再起動します。

## <a name="setting-up-the-host-computer"></a>ホストコンピューターのセットアップ


1.  ホストコンピューターが、USB デバッグのターゲットとなるように構成されていないことを確認します。 (必要に応じて、管理者としてコマンドプロンプトウィンドウを開き、「 **bcdedit/debug off**」と入力して再起動します)。
2.  ホストコンピューターで、[UsbView] を使用して、デバッグをサポートする EHCI ホストコントローラーとポートを検索します。 可能であれば、USB 2.0 デバッグケーブルの一端を、デバッグをサポートしていない EHCI ポート (ホストコンピューター上) に接続します。 それ以外の場合は、ホストコンピューターの任意の EHCI ポートにケーブルを接続します。
3.  USB 2.0 デバッグケーブルのもう一方の端を、ターゲットコンピューターで以前に特定したコネクタに接続します。

## <a name="starting-a-debugging-session-for-the-first-time"></a>初めてデバッグセッションを開始する


1.  ホストコンピューター上で実行されている Windows のビット数 (32 ビットまたは64ビット) を確認します。
2.  ホストコンピューターで、ホストコンピューター上で実行されている Windows のビットと一致するバージョンの WinDbg (管理者として) を開きます。 たとえば、ホストコンピューターで64ビットバージョンの Windows が実行されている場合は、管理者として、WinDbg の64ビットバージョンを開きます。
3.  [**ファイル**] メニューの [**カーネルデバッグ**] をクリックします。 [カーネルデバッグ] ダイアログボックスで、[ **USB** ] タブを開きます。ターゲットコンピューターを設定するときに作成したターゲットの名前を入力します。 **[OK]** をクリックします。

この時点で、USB デバッグドライバーがホストコンピューターにインストールされます。 このため、WinDbg のビットと Windows のビットを一致させることが重要です。 USB デバッグドライバーをインストールした後、次のデバッグセッションでは、32ビットまたは64ビットバージョンの WinDbg を使用できます。

**メモ**   USB 2.0 デバッグケーブルは実際には、ドングルが中央にある2本のケーブルです。 ドングルの方向は重要です。一方はデバイスの電源を入れ、もう一方の側はデバイスの電源を入れません。 USB デバッグが機能しない場合は、ドングルの方向にスワップしてみてください。 つまり、ドングルから両方のケーブルを取り外し、ケーブルが接続されている面を交換します。


## <a name="starting-a-debugging-session"></a>デバッグセッションの開始

### <a name="using-windbg"></a>WinDbg の使用

ホストコンピューターで、[WinDbg] を開きます。 [**ファイル**] メニューの [**カーネルデバッグ**] をクリックします。 [カーネルデバッグ] ダイアログボックスで、[ **USB** ] タブを開きます。ターゲットコンピューターを設定するときに作成したターゲットの名前を入力します。 **[OK]** をクリックします。

また、コマンドプロンプトウィンドウで次のコマンドを入力して、WinDbg を使用してセッションを開始することもできます。ここで、 *TargetName*はターゲットコンピューターをセットアップしたときに作成したターゲット名です。

**windbg/k usb: targetname =**<em>targetname</em>

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD の使用

ホストコンピューターで、コマンドプロンプトウィンドウを開き、次のコマンドを入力します。 *TargetName*はターゲットコンピューターをセットアップしたときに作成したターゲット名です。

**kd/k usb: targetname =**<em>targetname</em>

## <a name="span-idwhat-if-usbview-shows-a-debug-capable-portspanspan-idwhat_if_usbview_shows_a_debug_capable_portspanwhat-if-usbview-shows-a-debug-capable-port-but-does-not-show-the-port-mapped-to-any-physical-connector"></a><span id="what-if-usbview-shows-a-debug-capable-port"></span><span id="WHAT_IF_USBVIEW_SHOWS_A_DEBUG_CAPABLE_PORT"></span>USBView にデバッグ対応のポートが表示されていても、どの物理コネクタにもマップされているポートが表示されない場合はどうなりますか。

コンピューターによっては、USBView にデバッグ対応のポートが表示されますが、どの物理 USB コネクタにもマップされているポートは表示されません。 たとえば、USBView では、eHCI コントローラーのデバッグポート番号としてポート2が表示される場合があります。

```console
... USB Enhanced Host Controller ...
...
Debug Port Number:  2
Bus.Device.Function (in decimal): 0.29.0
```

また、[USBView] を使用して個々のポートを確認すると、[デバッグ対応] として表示されます。

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

しかし、USB 2.0 デバイス (フラッシュドライブなど) をコンピューター上のすべての USB コネクタに接続する場合、USBView は、デバイスがデバッグ対応ポート (この例ではポート 2) に接続されていることを示していません。 USBView では、xHCI コントローラーのポートにマップされた外部コネクタが表示されることがあります。これは、実際には、外部コネクタが eHCI コントローラーのデバッグ対応ポートにマップされるためです。

![xhci と ehci の [usbview] のスクリーンショット](images/usbview01.png)

このような場合でも、USB 2.0 ケーブルでカーネルモードのデバッグを確立できる可能性があります。 ここで示されている例では、USB 2.0 デバッグケーブルを、xHCI コントローラーのポート2にマップされていると表示されるコネクタに接続します。 次に、バスパラメーターを eHCI コントローラーのバス、デバイス、および関数番号 (この例では 0.29.0) に設定します。

`bcdedit /set "{dbgsettings}" busparams 0.29.0`

### <a name="additional-support"></a>その他のサポート

トラブルシューティングのヒントとその他の情報については、 [MICROSOFT USB ブログ](https://techcommunity.microsoft.com/t5/microsoft-usb-blog/bg-p/MicrosoftUSBBlog)を参照してください。

## <a name="related-topics"></a>関連トピック

[カーネル モードのデバッグを手動でセットアップする](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
