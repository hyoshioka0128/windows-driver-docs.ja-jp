---
title: WinLogon のデバッグ
description: WinLogon のデバッグ
ms.assetid: 408727cd-fb59-44fe-b896-88317d2bc087
keywords:
- WinLogon のデバッグ
- CSRSS をデバッグする NTSD
- winlogon プロセスをデバッグ、カーネル デバッガーからユーザー モード デバッガーの制御
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c82afa9cd90ae707e4046d816f38771818ae4fdc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346337"
---
# <a name="debugging-winlogon"></a>WinLogon のデバッグ


## <span id="ddk_debugging_winlogon_with_ntsd_dbg"></span><span id="DDK_DEBUGGING_WINLOGON_WITH_NTSD_DBG"></span>


WinLogon は、ログオンとログオフ、対話型のユーザーのタスクを処理し、CTRL + ALT + DEL キーのすべてのインスタンスを処理するユーザー モード プロセスです。

### <a name="span-idcontrollingntsdfromthekerneldebuggerspanspan-idcontrollingntsdfromthekerneldebuggerspancontrolling-ntsd-from-the-kernel-debugger"></a><span id="controlling_ntsd_from_the_kernel_debugger"></span><span id="CONTROLLING_NTSD_FROM_THE_KERNEL_DEBUGGER"></span>カーネル デバッガーから NTSD を制御します。

Winlogon プロセスをデバッグする最も簡単な方法は NTSD を使用して[カーネル デバッガーによる制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)します。

### <a name="span-idenablingwinlogondebuggingspanspan-idenablingwinlogondebuggingspanenabling-winlogon-debugging"></a><span id="enabling_winlogon_debugging"></span><span id="ENABLING_WINLOGON_DEBUGGING"></span>WinLogon のデバッグの有効化

カーネル デバッガーに、ユーザー モード デバッガーの出力をリダイレクトするためには、カーネル デバッグ接続を設定する必要があります。 参照してください[デバッグ設定](getting-set-up-for-debugging.md)します。

Winlogon プロセスにデバッガーをアタッチするには、レジストリを通じてに移動する必要がありますので、プロセスの開始時刻からデバッグします。 WinLogon のデバッグを設定するには、設定**HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\イメージ ファイルの実行オプション\\WinLogon.EXE\\デバッガー**に。

```console
ntsd -d -x -g 
```

**-D**オプションは、カーネル デバッガーに制御を渡します。 **-X**オプションにより、デバッガーを 2 回目の例外として、アクセス違反をキャプチャします。 **-G**オプションにより、WinLogon プロセスに、添付ファイルの後に実行します。 追加しないでください、 **-g** Winlogon.exe が (たとえば、最初のブレークポイントを設定する) 場合に開始する前にデバッグを開始するかどうか。

さらに、で書き留めた値を設定する必要があります、 **winlogon.exe** REG キー\_DWORD"0x000400F0"。 ヒープ チェックと FLG 設定\_を有効にする\_KDEBUG\_シンボル\_ロードします。 ただし、ためこの 2 つ目のフラグは、カーネル デバッガーにのみ影響を与える、シンボルする必要がありますもコピーする対象のコンピュータに、デバッガーを開始する前にします。

レジストリの変更には、再起動を有効にする必要があります。

### <a name="span-idperformingthedebuggingspanspan-idperformingthedebuggingspanperforming-the-debugging"></a><span id="performing_the_debugging"></span><span id="PERFORMING_THE_DEBUGGING"></span>デバッグを実行します。

次の再起動後に、デバッガーは winlogon プロセスに自動的に中断されます。

参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)続行する方法の詳細について。

ホスト コンピューター上の場所またはネットワーク上の他の場所には、シンボル パスを設定する必要があります。 WinLogon のデバッグ中は、ターゲット コンピューターのネットワークの認証は正しく機能しません。

 

 





