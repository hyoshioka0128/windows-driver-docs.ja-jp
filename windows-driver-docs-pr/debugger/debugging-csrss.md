---
title: CSRSS のデバッグ
description: CSRSS のデバッグ
ms.assetid: 9c3a8498-d9e4-4070-aee8-c038fa1666a4
keywords:
- CSRSS のデバッグ
- CSRSS をデバッグする NTSD
- CSRSS のデバッグ、カーネル デバッガーからユーザー モード デバッガーの制御
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2527c1f4b07f7f73a27fcde1b3eda6d91c27e528
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377187"
---
# <a name="debugging-csrss"></a>CSRSS のデバッグ


## <span id="ddk_debugging_csrss_with_ntsd_dbg"></span><span id="DDK_DEBUGGING_CSRSS_WITH_NTSD_DBG"></span>


クライアント サーバー ランタイム サブシステム (CSRSS) は、Windows 環境の基になる層を制御するユーザー モード プロセスです。 CSRSS 自体をデバッグする必要のある問題を数多くあります。

CSRSS のデバッグが役にも Windows サブシステムが突然で終了するときに、 [**バグ チェック 0xC000021A** ](bug-check-0xc000021a--status-system-process-terminated.md) (ステータス\_システム\_プロセス\_終了)。 この場合、CSRSS のデバッグは失敗を検出、「予期しない」ポイントに到達する前に、。

### <a name="span-idcontrollingntsdfromthekerneldebuggerspanspan-idcontrollingntsdfromthekerneldebuggerspancontrolling-ntsd-from-the-kernel-debugger"></a><span id="controlling_ntsd_from_the_kernel_debugger"></span><span id="CONTROLLING_NTSD_FROM_THE_KERNEL_DEBUGGER"></span>カーネル デバッガーから NTSD を制御します。

CSRSS をデバッグする最も簡単な方法は NTSD を使用して[カーネル デバッガーによる制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)します。

### <a name="span-idenablingcsrssdebuggingspanspan-idenablingcsrssdebuggingspanenabling-csrss-debugging"></a><span id="enabling_csrss_debugging"></span><span id="ENABLING_CSRSS_DEBUGGING"></span>CSRSS のデバッグの有効化

続行する前に、CSRSS のデバッグを有効にする必要があります。 ターゲット コンピューターが実行されている場合、*チェック済みビルド*Windows の CSRSS のデバッグは常に有効にします。 ターゲット コンピューターが実行されている場合、*フリー ビルド*Windows のグローバル フラグ ユーティリティの (GFlags) を通じて CSRSS のデバッグを有効にする必要があります。

これを行うには、GFlags ユーティリティを起動、選択、**システム レジストリ**ボタンをクリックし、選択**Win32 サブシステムのデバッグを有効にする**します。

または、次の GFlags コマンドラインを使用できます。

```dbgcmd
gflags /r +20000 
```

または、GFlags を使用する代わりに、手動でレジストリ キーを編集する場合は、ことができます。 次のレジストリ キーを開きます。

```text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager 
```

編集、 **GlobalFlag**エントリの値 (型 REG の\_DWORD) 0x00020000 ビットを設定します。

GFlags を使用するか、手動でレジストリを編集後の変更を反映する再起動する必要があります。

### <a name="span-idstartingntsdspanspan-idstartingntsdspanstarting-ntsd"></a><span id="starting_ntsd"></span><span id="STARTING_NTSD"></span>NTSD を起動

カーネル デバッガーからユーザー モードのデバッガーを制御するためには、カーネル デバッグ接続を設定する必要があります。 参照してください[を取得する設定をデバッグ用](getting-set-up-for-debugging.md)詳細についてはします。

レジストリが正しく構成されて、次のように NTSD を起動するだけのなります。

**ntsd --**

参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)続行する方法の詳細について。

ホスト コンピューター上の場所またはネットワーク上の他の場所には、シンボル パスを設定する必要があります。 CSRSS のデバッグ中は、ターゲット コンピューターのネットワークの認証は正しく機能しません。

"で、ページの io エラー"メッセージを表示する可能性がありますに注意してください。 これは、ハードウェア障害の別の表れです。

デバッグ セッションの終了時に、デバッガーは、CSRSS プロセスが実行中でも CSRSS からデタッチされます。 CSRSS プロセス自体の終了を回避できます。

 

 





