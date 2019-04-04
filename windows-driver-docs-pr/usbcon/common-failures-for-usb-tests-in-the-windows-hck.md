---
Description: Common failures for USB tests in the Windows HLK.
title: Windows HLK で USB テストのための一般的なエラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b8ff4b0debb546befba3ca04ff21268c346b213
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556471"
---
# <a name="common-failures-for-usb-tests-in-the-windows-hlk"></a>Windows HLK で USB テストのための一般的なエラー


Windows HLK で USB テストの一般的なエラー。

## <a name="devfund-tests-for-usb"></a>USB の DevFund テスト


-   エラーの状態:状態を確認するデバイスは、MUTT デバイスが存在しないことを示すエラーで失敗します。

    1.  SuperMUTT が Winusb.sys または Usbtcd.sys ドライバーとして実行されています。 取得できます、ドライバーとドライバーのインストール パッケージ ファイルをインストールして、 [MUTT ソフトウェア パッケージ](https://msdn.microsoft.com/windows/hardware/jj590752)します。 詳細については、[MUTT ソフトウェア パッケージ ツール](mutt-software-package.md)を参照してください。
    2.  デバイス マネージャーとして SuperMUTT のハードウェア ID が表示されることを確認"USB\\VID\_045E & PID\_078F"。 **注**  PID\_078E が正しくありません。
    3.  デバイス マネージャーがいることを確認 (**ビュー&gt;接続によってデバイス**) 列挙 SuperMUTT を示しています。 xHCI コント ローラーのダウン ストリーム。
    4.  USBView で SuperMUTT デバイスが SuperSpeed で動作していることを確認します。 **注**  から USBView をインストールすることができます、**デバッグ ツールの Windows にインストール パッケージ**Microsoft Windows ソフトウェア開発キット (SDK) にします。 または、USBView は、Windows Driver Kit (WDK) でデバッガー フォルダーにインストールされます。
    5.  MUTT ファームウェアが最新であることを確認します。 管理者特権のプロンプトから実行"muttutil updatefirmware"ディレクトリにインストールされている、 [MUTT ソフトウェア パッケージ](https://msdn.microsoft.com/windows/hardware/jj590752)します。

    問題が解決しない場合は、これらの添付ファイルのある問題を報告します。
    -   デバイス マネージャーのスクリーン ショットと USBView が表示された項目を 1 ~ 4 に上記の一覧。
    -   出力、 [MuttUtil](muttutil.md)コマンド。
-   エラーの状態:DevFund は、単純な I/O 転送中に失敗します。
    1.  移動して https://aka.ms/usbtraceusbtrace.cmd をダウンロードします。
    2.  このスクリプトを使用すると、詳しい調査のためのイベントのドライバーのログをキャプチャできます。
    3.  %Systemdrive% のすべての内容をアタッチ\\Windows\Tracing、バグにします。
    4.  保存し、失敗したテストの .hlkx ファイルを添付します。
-   エラーの状態:MUTT デバイスがシステムに接続されているが、適切なドライバーがインストールされていません。

    最も可能性の高いドライバーのインストールが失敗したか、デバイスには、最新のファームウェアはありません。 ドライバーとして Winusb.sys または Usbtcd.sys をインストールします。 取得できます、ドライバーとドライバーのインストール パッケージ ファイルをインストールして、 [MUTT ソフトウェア パッケージ](https://msdn.microsoft.com/windows/hardware/jj590752)します。

 

 




