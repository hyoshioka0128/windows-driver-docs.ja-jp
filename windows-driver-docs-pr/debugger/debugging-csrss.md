---
title: CSRSS のデバッグ
description: CSRSS のデバッグ
ms.assetid: 9c3a8498-d9e4-4070-aee8-c038fa1666a4
keywords:
- CSRSS デバッグ
- NTSD, CSRSS のデバッグ
- カーネルデバッガーからのユーザーモードデバッガーの制御、CSRSS のデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71e74710deca5e6cfc83f6771e2ca6157b1a1828
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209382"
---
# <a name="debugging-csrss"></a>CSRSS のデバッグ


## <span id="ddk_debugging_csrss_with_ntsd_dbg"></span><span id="DDK_DEBUGGING_CSRSS_WITH_NTSD_DBG"></span>


クライアントサーバーの実行時サブシステム (CSRSS) は、Windows 環境の基礎となるレイヤーを制御するユーザーモードのプロセスです。 CSRSS 自体をデバッグするために必要ないくつかの問題があります。

CSRSS のデバッグは、Windows サブシステムが予期せず終了し、[**バグチェック 0xc000021a**](bug-check-0xc000021a--winlogin-fatal-error.md) (WINLOGON\_致命的な\_エラー) が発生した場合にも役立ちます。 この場合、CSRSS をデバッグすると、"予期しない" ポイントになる前にエラーをキャッチします。

### <a name="span-idcontrolling_ntsd_from_the_kernel_debuggerspanspan-idcontrolling_ntsd_from_the_kernel_debuggerspancontrolling-ntsd-from-the-kernel-debugger"></a><span id="controlling_ntsd_from_the_kernel_debugger"></span><span id="CONTROLLING_NTSD_FROM_THE_KERNEL_DEBUGGER"></span>カーネルデバッガーからの NTSD の制御

CSRSS をデバッグする最も簡単な方法は、NTSD を使用して[カーネルデバッガーから制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)することです。

### <a name="span-idenabling_csrss_debuggingspanspan-idenabling_csrss_debuggingspanenabling-csrss-debugging"></a><span id="enabling_csrss_debugging"></span><span id="ENABLING_CSRSS_DEBUGGING"></span>CSRSS デバッグを有効にする

操作を続行する前に、CSRSS デバッグを有効にする必要があります。 対象のコンピューターで Windows の*無料ビルド*が実行されている場合は、グローバルフラグユーティリティ (GFlags) を使用して CSRSS デバッグを有効にする必要があります。

これを行うには、GFlags ユーティリティを起動し、[**システムレジストリ**] オプションボタンを選択して、[ **Win32 サブシステムのデバッグを有効に**する] を選択します。

または、次の GFlags コマンドラインを使用することもできます。

```dbgcmd
gflags /r +20000 
```

または、必要に応じて、GFlags を使用する代わりに、手動でレジストリキーを編集することもできます。 次のレジストリキーを開きます。

```text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager 
```

**GlobalFlag** value エントリ (REG\_DWORD 型) を編集し、ビット0x00020000 を設定します。

GFlags を使用するか、手動でレジストリを編集した後は、変更を有効にするために再起動する必要があります。

### <a name="span-idstarting_ntsdspanspan-idstarting_ntsdspanstarting-ntsd"></a><span id="starting_ntsd"></span><span id="STARTING_NTSD"></span>NTSD の開始

カーネルデバッガーからユーザーモードのデバッガーを制御するため、カーネルデバッグ接続を設定する必要があります。 詳細については、「[デバッグの設定](getting-set-up-for-debugging.md)」を参照してください。

レジストリが適切に構成されたら、次のように NTSD を開始するのが簡単です。

**ntsd--**

続行する方法の詳細については[、「カーネルデバッガーからのユーザーモードデバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)」を参照してください。

シンボルパスは、ホストコンピューター上の場所またはネットワーク上の他の場所に設定する必要があります。 CSRSS をデバッグしているときに、ターゲットコンピューターのネットワーク認証が正常に機能しません。

"In page io error" というメッセージが表示される場合があります。 これは、ハードウェア障害のもう1つの取り組みです。

デバッグセッションが終了すると、CSRSS プロセスがまだ実行されている間、デバッガーは CSRSS からデタッチします。 これにより、CSRSS プロセス自体が終了するのを防ぐことができます。

 

 





