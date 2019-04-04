---
Description: MuttUtil performs various tasks on MUTT devices.
title: MuttUtil
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54ec748a8c01ba48162b56c6d0a98cd05468e4e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572545"
---
# <a name="muttutil"></a>MuttUtil


MuttUtil に対してさまざまなタスクを実行します[MUTT デバイス](microsoft-usb-test-tool--mutt--devices.md)します。

-   テスト デバイスのファームウェアを更新します。
-   MUTT デバイス用のドライバーをインストールします。
-   デバイスがエラーなしにインストールされていることを確認します。
-   デバイスの動作のバス速度を変更します。
-   指定した期間後に再開ウェイク信号を送信するデバイスを構成します。
-   MUTT パックでは、完全なまたは高速度で動作するハブを設定します。としてシングル TT またはマルチ TT ハブです。

テスト デバイスが最新のファームウェアに正しくアップグレードされたことを確認するには含まれているテスト スクリプトのインストール」セクションでは、MuttUtil 埋め込まれます。 ツールが含まれ、 [MUTT ソフトウェア パッケージ](https://go.microsoft.com/fwlink/p/?linkid=617710)します。

## <a name="how-to-run-muttutil"></a>MuttUtil を実行する方法


**MuttUtil ヘルプ**

コマンド ライン オプションの一覧を取得するには、次のコマンドを実行します。

`MUTTUtil.exe`

**システムに接続されているすべての MUTT デバイスの検索**

`MUTTUtil.exe -list`

``` syntax
       :   : HARDWARE ID                    : PROBLEM CODE : DRIVER
DEVICE : 0 : USB\VID_045E&PID_0611&REV_0034 : 0            : WINUSB
DEVICE : 1 : USB\VID_045E&PID_078E&REV_8011 : 28           :

Return value: 1
```

上記のコマンドは、システムに SuperMUTT (1) と接続された MUTT パック (0) があることを示します。 Microsoft 提供のカーネル モード ドライバー、Winusb.sys は、SuperMUTT デバイス関数ドライバーです。 Winusb.sys の詳細については、[WinUSB](winusb.md)を参照してください。

MUTT パック デバイスの問題のコードの 28 は、デバイスのドライバーが読み込まれていないことを示します。

**MUTT デバイスのパーソナリティを変更します。**

MUTT デバイスは、テスト デバイスとしても使用される、 [USB UWP アプリのサンプル](https://go.microsoft.com/fwlink/p/?linkid=309716)します。 実行して、このシナリオのファームウェアを更新する必要があります、`-SetWinRTUsb`オプション。 この演習では、SuperMUTT デバイスは WinRT 個性に設定されます。

MUTT 個性にこれを変更するには、このコマンドを使用します。

`MuttUtil.exe -# 1 -MuttPersonality`

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -MuttPersonality
Looking for MUTT devices
Send command to change device personality
Return value: 0

c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078F&REV_0034 :             0  : WINUSB
Return value: 1
```

USB にハードウェア ID が変更されたことに注意してください。\\VID\_045E & PID\_078F & REV\_0037 します。 リビジョン バージョンでは、ファームウェアのバージョン番号を示します。

**MUTT デバイスのドライバーをインストールします。**

インストール情報が含まれるドライバーの INF ファイルを指定します。 例えば以下のようにします。

`MUTTUtil.exe -UpdateDriver USBTCD.inf`

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -UpdateDriver USBTCD.inf
Return value: 0

c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078F&REV_0034 :             0  : USBTCD
Return value: 1
```

上記のコマンドでは、指定した USBTCD.sys ドライバーを使用した既存のドライバーが置き換えられます。 ドライバーが含まれている、 [MUTT ソフトウェア パッケージ](https://go.microsoft.com/fwlink/p/?linkid=617710)します。

接続された MUTT デバイスが複数ある場合は、同時に、ドライバーを更新できます。

`MUTTUtil.exe -# 0 -# 1 -MultiUpdateDriver USBTCD.inf usbfx2.inf`

上記のコマンドは、0 のデバイスやデバイス 1、Winusb.sys 用 USBTCD.sys をインストールします。

**MUTT デバイスのファームウェアを更新しています**

`MuttUtil.exe -UpdateFirmware`

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -UpdateFirmware
Looking for MUTT devices
0: Updating device firmware from version 34 to version 37
  Erasing EEPROM -- this takes approx 30 seconds
Writing core firmware image
Writing Table at sector 0x09
Writing Table at sector 0x0A
Writing Table at sector 0x0B
Writing Table at sector 0x0C
Writing Table at sector 0x0D
Writing Table at sector 0x0E
Writing Table at sector 0x0F
Writing Table at sector 0x10
Writing Table at sector 0x08
0: Resetting device
Return value: 0
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078F&REV_0037 :             0  : USBTCD
Return value: 1
```

コマンドは、ファームウェアの EEPROM を更新する*場合にのみ*デバイスのバージョンが古い。 ツールでは、ファームウェア イメージが埋め込まれます。 デバイスのファームウェアのツールがインストールされているよりも新しいバージョンの場合、デバイスのファームウェアは置き換えられません。 バージョンに関係なく、デバイスのファームウェアを置換する場合は、実行と MuttUtil、`-ForceUpdateFirmware`オプションを使用します。

別の方法、ファームウェアの更新の EEPROM または RAM に直接書き込むことです。 これは、ファームウェアのファイルが必要です。

EEPROM を消去するを使用して、`-EraseEEPROM`オプション

**切断、再接続時に、およびデバイスの列挙**

`MuttUtil.exe -Reconnect`

`MuttUtil.exe -CyclePort`

上記のコマンドは、デバイスを切断して再接続して、同じポートでします。

`-CyclePort`オプションにより、デバイスを切断して、デバイスが電気的に切断されていない点を除いて、ポートに接続します。 デバイスが切断され、ソフトウェアで再接続されます。 この操作は、デバイスのリセットにつながるし、PnP マネージャーは、[デバイス] ノードを再構築します。

MUTT パックまたは SuperMUTT パック デバイスのハブをリセットするには、このコマンドを使用します。

`MuttUtil.exe -# 1 -ResetHub`

**デバイスの速度を変更します。**

このコマンドを使用して、MUTT デバイスのデバイスの速度を変更できます。

`MuttUtil.exe -# 0 -SetFullSpeed`

`MuttUtil.exe -# 1 -SetHighSpeed`

コマンドは、デバイスを切断して再接続して、指定した速度で同じポートでします。

MUTT パックまたは SuperMUTT パックでは、ハブの速度を変更する場合は、使用してフル スピードのモードで動作する、`-HubFS`コマンド。

`MuttUtil.exe -# 1 -HubFS`

**システム スリープに再開シグナルを送る**

通常、再開シグナルは、特定ユーザーの操作時に (で省電力) デバイスによって送信されます。 このコマンドを使用して、その動作をシミュレートできます。

`MuttUtil.exe -WakeAfterSuspend 5000`

コマンドは、5 秒、バスを一時停止後再開シグナルの送信にデバイスを構成します。

切断および再接続一定の時間を使用して、バスを中断した後でデバイスを構成することも、`-DisconnectAfterSuspend`オプション。

**設定して、ダウン ストリーム ポート - MUTT パックおよび SuperMUTT パックで、過電流をクリアします。**

これらのコマンドは、設定し、過電流の pin の Mutt パックの公開されているポートをクリアします。

`MuttUtil.exe -# 1 -SetOvercurrent`

`MuttUtil.exe -# 1 -ClearOvercurrent`

**ハブを TT 高速ハブ - MUTT パックおよび SuperMUTT パックに変換します。**

これらのコマンドを使用してマルチ TT 高速ハブまたはシングル TT 高速ハブとして機能するハブを設定できます。

`MuttUtil.exe -# 1 -HubHSMultiTT`

`MuttUtil.exe -# 1 -HubHSSingleTT`

## <a name="related-topics"></a>関連トピック
[USB テスト ツール](usb-test-tools.md)  
[MUTT ソフトウェア パッケージのツール](mutt-software-package.md)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



