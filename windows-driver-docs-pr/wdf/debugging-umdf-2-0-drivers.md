---
title: ドライバーがクラッシュする UMDF 2.0 のトラブルシューティング
description: ユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 を開始するには、UMDF ドライバーをデバッグするのに Wdfkd.dll で実装されたデバッガー拡張機能コマンドのサブセットを使用できます。
ms.assetid: df1bfc10-379b-457f-a9c8-40fa10048f81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba636c96e7cbf3e38afb96f62ac069d4ac50f29a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552727"
---
# <a name="troubleshooting-umdf-20-driver-crashes"></a>ドライバーがクラッシュする UMDF 2.0 のトラブルシューティング


ユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 を開始するには、UMDF ドライバーをデバッグするのに Wdfkd.dll で実装されたデバッガー拡張機能コマンドのサブセットを使用できます。 このトピックでは、UMDF ドライバーに関する問題のトラブルシューティングを起動する可能性がありますコマンドについて説明します。

##  <a name="determining-why-a-umdf-20-driver-crashed"></a>ドライバーがクラッシュした理由 UMDF 2.0 を決定します。


ドライバーのホスト プロセスを終了すると場合に、ドライバーで発生するコールバックで問題がある可能性があります、[ホスト タイムアウト](how-umdf-enforces-time-outs.md)しきい値を超えています。 ここで、reflector は、ドライバーのホスト プロセスを終了します。

調査のため、カーネル モードのデバッグ セッションの設定」の説明に従って[UMDF ドライバーのデバッグを有効にする方法](enabling-a-debugger.md)します。

- 場合**HostFailKdDebugBreak**設定は、カーネル モード デバッガーのタイムアウトしきい値を超えたときに、リフレクタ中断します。 デバッガーの出力に表示されますいくつかの提案を開始する方法のなどのリンクをクリックすることができます。 次に、例を示します。

  ```cpp
  **** Problem detected in UMDF driver "WUDFOsrUsbFx2". !process 0xFFFFE0000495B080 0x1f, !devstack 0xFFFFE000032BFA10, Problem code 3 ****
  **** Dump UMDF driver image name and stack: !wdfkd.wdfumdevstack 0x000000BEBB49AE20
  **** Dump UM Irps for this stack: !wdfkd.wdfumirps 0x000000BEBB49AE20
  **** Dump UMDF trace log: !wmitrace.logdump WUDFTrace
  **** Helpful UMDF debugger extension commands: !wdfkd.wdfhelp
  **** Note that driver host process may get terminated if you go past this break, making it difficult to debug the problem!
  ```

- 使用[ **! 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112)試みることができます、エラー、およびその他の UMDF 拡張機能コマンドに関する情報を表示します。
- 使用[ **! プロセス 0 0x1f wudfhost.exe** ](https://msdn.microsoft.com/library/windows/hardware/ff564717)スレッド スタック情報を含むすべて Wudfhost.exe ドライバー ホスト プロセスを一覧表示します。

  使用することも[ **! wdfkd.wdfldr** ](https://msdn.microsoft.com/library/windows/hardware/ff565803) WDF に現在バインドされているすべてのドライバーを表示します。 UMDF ドライバーのイメージ名をクリックすると、デバッガーには、ホスト プロセスのアドレスが表示されます。 そのプロセスに固有の情報を表示するプロセスのアドレスをクリックすることができます。

- 必要に応じて、使用して[ **.process/r/p*プロセス*** ](https://msdn.microsoft.com/library/windows/hardware/ff564723)ドライバーをホストしている Wudfhost プロセスのプロセスのコンテキストを切り替える。 使用[ **.cache forcedecodeuser** ](https://msdn.microsoft.com/library/windows/hardware/ff562180)と**lmu**ドライバーが、現在のプロセスでホストされていることを確認します。
- スレッドの呼び出し履歴を調べます ([**! スレッド*アドレス***](https://msdn.microsoft.com/library/windows/hardware/ff565440)) ドライバーのコールバックがタイムアウトしたかどうかを判断します。スレッドのティック数を確認します。 Windows 8.1 ので、reflector は 1 分後にタイムアウトします。
- 使用[ **! wdfkd.wdfdriverinfo MyDriver.dll 0x10** ](https://msdn.microsoft.com/library/windows/hardware/ff565724)詳細フォームに、デバイス ツリーを表示します。 をクリックして[ **! wdfdevice**](https://msdn.microsoft.com/library/windows/hardware/ff565703)します。 このコマンドは、詳細な電源、電源ポリシー、プラグ アンド プレイ (PnP) の状態情報を表示します。
- 使用[ **! wdfkd.wdfumirps** ](https://msdn.microsoft.com/library/windows/hardware/dn265384)に保留中の Irp を探します。
- 使用[ **! wdfkd.wdfdevicequeues** ](https://msdn.microsoft.com/library/windows/hardware/ff565715)ドライバーのキューの状態を確認します。
- カーネル モードのデバッグ セッションで使用できます[ **! wmitrace.logdump WudfTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff566159)トレース ログを表示します。

## <a name="displaying-the-umdf-20-ifr-log"></a>IFR ログインの UMDF 2.0 を表示します。


カーネル モードのデバッグ セッションで使用することができます、 [ **! wdfkd.wdflogdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565805)使用可能な場合、Windows Driver Frameworks (WDF) インフライト レコーダー (IFR) ログを表示する拡張機能のコマンドを記録します。

## <a name="finding-memory-dump-files"></a>メモリ ダンプ ファイルを検索します。


参照してください[リフレクターが、ホスト プロセスを終了した理由を判断する](determining-why-the-reflector-terminated-the-host-process.md)をユーザー モード ダンプ ファイルを見つける方法について。 参照してください[UMDF ドライバーで WPP ソフトウェア トレースを使用して](using-wpp-software-tracing-in-umdf-drivers.md)を設定する方法については、 **LogMinidumpType**ミニダンプ ファイルに格納されている情報の種類を指定するレジストリ値。









