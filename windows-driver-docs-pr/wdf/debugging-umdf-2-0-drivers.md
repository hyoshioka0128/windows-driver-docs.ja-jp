---
title: UMDF 2.0 ドライバーのクラッシュのトラブルシューティング
description: ユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 を開始するには、UMDF ドライバーをデバッグするのに Wdfkd.dll で実装されたデバッガー拡張機能コマンドのサブセットを使用できます。
ms.assetid: df1bfc10-379b-457f-a9c8-40fa10048f81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62ae6efccd3326c2c64246e974124f63145ec193
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377469"
---
# <a name="troubleshooting-umdf-20-driver-crashes"></a>UMDF 2.0 ドライバーのクラッシュのトラブルシューティング


ユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 を開始するには、UMDF ドライバーをデバッグするのに Wdfkd.dll で実装されたデバッガー拡張機能コマンドのサブセットを使用できます。 このトピックでは、UMDF ドライバーに関する問題のトラブルシューティングを起動する可能性がありますコマンドについて説明します。

##  <a name="determining-why-a-umdf-20-driver-crashed"></a>ドライバーがクラッシュした理由 UMDF 2.0 を決定します。


ドライバーのホスト プロセスを終了すると場合に、ドライバーで発生するコールバックで問題がある可能性があります、[ホスト タイムアウト](how-umdf-enforces-time-outs.md)しきい値を超えています。 ここで、reflector は、ドライバーのホスト プロセスを終了します。

調査のため、カーネル モードのデバッグ セッションの設定」の説明に従って[UMDF ドライバーのデバッグを有効にする方法](enabling-a-debugger.md)します。

- 場合**HostFailKdDebugBreak**設定は、カーネル モード デバッガーのタイムアウトしきい値を超えたときに、リフレクタ中断します。 デバッガーの出力に表示されますいくつかの提案を開始する方法のなどのリンクをクリックすることができます。 例:

  ```cpp
  **** Problem detected in UMDF driver "WUDFOsrUsbFx2". !process 0xFFFFE0000495B080 0x1f, !devstack 0xFFFFE000032BFA10, Problem code 3 ****
  **** Dump UMDF driver image name and stack: !wdfkd.wdfumdevstack 0x000000BEBB49AE20
  **** Dump UM Irps for this stack: !wdfkd.wdfumirps 0x000000BEBB49AE20
  **** Dump UMDF trace log: !wmitrace.logdump WUDFTrace
  **** Helpful UMDF debugger extension commands: !wdfkd.wdfhelp
  **** Note that driver host process may get terminated if you go past this break, making it difficult to debug the problem!
  ```

- 使用[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)試みることができます、エラー、およびその他の UMDF 拡張機能コマンドに関する情報を表示します。
- 使用[ **! プロセス 0 0x1f wudfhost.exe** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process)スレッド スタック情報を含むすべて Wudfhost.exe ドライバー ホスト プロセスを一覧表示します。

  使用することも[ **! wdfkd.wdfldr** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfldr) WDF に現在バインドされているすべてのドライバーを表示します。 UMDF ドライバーのイメージ名をクリックすると、デバッガーには、ホスト プロセスのアドレスが表示されます。 そのプロセスに固有の情報を表示するプロセスのアドレスをクリックすることができます。

- 必要に応じて、使用して[ **.process/r/p*プロセス*** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process--set-process-context-)ドライバーをホストしている Wudfhost プロセスのプロセスのコンテキストを切り替える。 使用[ **.cache forcedecodeuser** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-cache--set-cache-size-)と**lmu**ドライバーが、現在のプロセスでホストされていることを確認します。
- スレッドの呼び出し履歴を調べます ([ **! スレッド*アドレス*** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-thread)) ドライバーのコールバックがタイムアウトしたかどうかを判断します。スレッドのティック数を確認します。 Windows 8.1 ので、reflector は 1 分後にタイムアウトします。
- 使用[ **! wdfkd.wdfdriverinfo MyDriver.dll 0x10** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)詳細フォームに、デバイス ツリーを表示します。 をクリックして[ **! wdfdevice**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)します。 このコマンドは、詳細な電源、電源ポリシー、プラグ アンド プレイ (PnP) の状態情報を表示します。
- 使用[ **! wdfkd.wdfumirps** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps)に保留中の Irp を探します。
- 使用[ **! wdfkd.wdfdevicequeues** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevicequeues)ドライバーのキューの状態を確認します。
- カーネル モードのデバッグ セッションで使用できます[ **! wmitrace.logdump WudfTrace** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wmitrace-logdump)トレース ログを表示します。

## <a name="displaying-the-umdf-20-ifr-log"></a>IFR ログインの UMDF 2.0 を表示します。


カーネル モードのデバッグ セッションで使用することができます、 [ **! wdfkd.wdflogdump** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)使用可能な場合、Windows Driver Frameworks (WDF) インフライト レコーダー (IFR) ログを表示する拡張機能のコマンドを記録します。

## <a name="finding-memory-dump-files"></a>メモリ ダンプ ファイルを検索します。


参照してください[リフレクターが、ホスト プロセスを終了した理由を判断する](determining-why-the-reflector-terminated-the-host-process.md)をユーザー モード ダンプ ファイルを見つける方法について。 参照してください[UMDF ドライバーで WPP ソフトウェア トレースを使用して](using-wpp-software-tracing-in-umdf-drivers.md)を設定する方法については、 **LogMinidumpType**ミニダンプ ファイルに格納されている情報の種類を指定するレジストリ値。









