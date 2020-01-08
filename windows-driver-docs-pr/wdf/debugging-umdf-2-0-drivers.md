---
title: UMDF 2.0 ドライバーのクラッシュのトラブルシューティング
description: ユーザーモードドライバーフレームワーク (UMDF) バージョン2以降では、Wdfkd に実装されているデバッガー拡張機能コマンドのサブセットを使用して、UMDF ドライバーをデバッグできます。
ms.assetid: df1bfc10-379b-457f-a9c8-40fa10048f81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4336f7b007fe1d03f5f2fb902658779d24d5f84d
ms.sourcegitcommit: 9355a80229bb2384dd45493d36bdc783abdd8d7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75694242"
---
# <a name="troubleshooting-umdf-20-driver-crashes"></a>UMDF 2.0 ドライバーのクラッシュのトラブルシューティング


ユーザーモードドライバーフレームワーク (UMDF) バージョン2以降では、Wdfkd に実装されているデバッガー拡張機能コマンドのサブセットを使用して、UMDF ドライバーをデバッグできます。 このトピックでは、UMDF ドライバーの問題をトラブルシューティングするために、どのコマンドを起動するかについて説明します。

##  <a name="determining-why-a-umdf-20-driver-crashed"></a>UMDF 2.0 ドライバーがクラッシュした原因の特定


ドライバーのホストプロセスが終了した場合、コールバックで[ホストのタイムアウト](how-umdf-enforces-time-outs.md)しきい値を超えた問題が発生している可能性があります。 この場合、リフレクタはドライバーホストプロセスを終了します。

調査するには、まず、「 [UMDF ドライバーのデバッグを有効にする方法](enabling-a-debugger.md)」の説明に従って、カーネルモードのデバッグセッションを設定します。 テストシステムにアタッチされたカーネルデバッガーで、UMDF ドライバーのすべての開発とテストを行い、WUDFHost で[アプリケーション検証ツール ()](../debugger/debugger-download-tools.md)を有効にすることを強くお勧めします。 次のコマンドを使用して、カーネルデバッガーをアタッチし、再起動します。

```cpp
AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
```

- **HostFailKdDebugBreak**が設定されている場合 (これは既定で Windows 8 を起動しています)、タイムアウトしきい値を超えたときに、リフレクターはカーネルモードのデバッガーを中断します。 デバッガーの出力には、クリックできるリンクなど、開始方法に関するいくつかの推奨事項が表示されます。 たとえば次のようになります。

  ```cpp
  **** Problem detected in UMDF driver "WUDFOsrUsbFx2". !process 0xFFFFE0000495B080 0x1f, !devstack 0xFFFFE000032BFA10, Problem code 3 ****
  **** Dump UMDF driver image name and stack: !wdfkd.wdfumdevstack 0x000000BEBB49AE20
  **** Dump UM Irps for this stack: !wdfkd.wdfumirps 0x000000BEBB49AE20
  **** Dump UMDF trace log: !wmitrace.logdump WUDFTrace
  **** Helpful UMDF debugger extension commands: !wdfkd.wdfhelp
  **** Note that driver host process may get terminated if you go past this break, making it difficult to debug the problem!
  ```

- [ **! Analyze**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)を使用して、エラーに関する情報と、実行できるその他の UMDF 拡張コマンドを表示します。
- [ **! Process 0 0x1f wudfhost .exe**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process)を使用して、スレッドスタック情報を含むすべての Wudfhost .exe ドライバーのホストプロセスを一覧表示します。

  また、! wdfkd. wdfumtriage と[ **! wdfkd. wdfldr**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfldr)を使用すると、現在 WDF にバインドされているすべてのドライバーを表示できます。 UMDF ドライバーのイメージ名をクリックすると、ホストプロセスのアドレスがデバッガーに表示されます。 次に、プロセスのアドレスをクリックすると、そのプロセスに固有の情報が表示されます。

- 必要に応じて、 [ **. process/r/P*プロセス*** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process--set-process-context-)を使用して、プロセスコンテキストを、ドライバーをホストしている wudfhost プロセスのコンテキストに切り替えます。 [ **. Cache forcedecodeuser**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-cache--set-cache-size-)と**lmu**を使用して、ドライバーが現在のプロセスでホストされていることを確認します。
- スレッド呼び出し履歴 ([ **! スレッド*アドレス*** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-thread)) を調べて、ドライバーコールバックがタイムアウトしたかどうかを確認します。スレッドのティック数を確認します。 Windows 8.1 では、リフレクターは1分後にタイムアウトします。
- デバイスツリーを詳細な形式で表示するには、 [ **! wdfkd. wdfdriverinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)を使用します。 次に、[ [ **! wdfdevice**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)] をクリックします。 このコマンドは、電源、電源ポリシー、およびプラグアンドプレイ (PnP) の詳細な状態情報を表示します。
- [**Wdfumirps**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps)を使用して、保留中の irp を探します。
- [ **! Wdfkd. wdfdevicequeues**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevicequeues)を使用して、ドライバーのキューの状態を確認します。
- カーネルモードのデバッグセッションでは、 [ **! Wmitrace WudfTrace**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wmitrace-logdump)を使用してトレースログを表示できます。

## <a name="displaying-the-umdf-20-ifr-log"></a>UMDF 2.0 IFR ログの表示


カーネルモードのデバッグセッションでは、 [ **! wdfkd. wdflogdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump) extension コマンドを使用して、Windows Driver FRAMEWORK (WDF) の実行中のレコーダー (IFR) ログレコードを表示できます (使用可能な場合)。

## <a name="finding-memory-dump-files"></a>メモリダンプファイルの検索


ユーザーモードのダンプファイルの検索について[は、「リフレクターがホストプロセスを終了した理由の特定](determining-why-the-reflector-terminated-the-host-process.md)」を参照してください。 **LogMinidumpType**レジストリ値を設定してミニダンプファイルに格納されている情報の種類を指定する方法については、「 [UMDF ドライバーでの WPP ソフトウェアトレースの使用](using-wpp-software-tracing-in-umdf-drivers.md)」を参照してください。







