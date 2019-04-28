---
title: デバッグの中断
description: デバッグの中断
ms.assetid: fc17d0b2-3ef5-4e10-a6a3-51f7011fddcf
keywords:
- デバッグの中断
- デバッグの中断、ターゲットを制御します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b28b6aaf40ae0dde309755303c61321ca8cc7b3b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374375"
---
# <a name="debug--break"></a>Debug | Break (デバッグ | 中断)


## <span id="ddk_debug_break_dbg"></span><span id="DDK_DEBUG_BREAK_DBG"></span>


をクリックして**中断**上、**デバッグ**デバッガーに、ターゲットの実行と戻り値の制御を停止するメニュー。

ユーザー モードでは、このコマンドは、プロセスとデバッガーの制御を回復できるように、そのスレッドを停止します。 カーネル モードでは、このコマンドは、ターゲット コンピューターに分割します。

デバッガーがアクティブな間は、このコマンドを使用することもできます。 このような状況で、コマンドが時間の長い切り捨て[デバッガー コマンド ウィンドウ](debugger-command-window.md)が表示されます。

**Break**コマンドを ctrl キーを押しながら BREAK キーを押してまたはクリックすると、 **Break (Ctrl + Break)** ボタン (![改ボタンのスクリーン ショット](images/tbbreak.png))、ツールバーの。

### <a name="span-idaltdelspanspan-idaltdelspanaltdel"></a><span id="ALT_DEL"></span><span id="alt_del"></span>ALT + DEL

使用することができます**ALT + DEL**を送信する、**中断**します。 **ALT + DEL**と同様に機能**Break (Ctrl + Break)。**

### <a name="span-idusermodeeffectsspanspan-idusermodeeffectsspanuser-mode-effects"></a><span id="user_mode_effects"></span><span id="USER_MODE_EFFECTS"></span>ユーザー モードの効果

ユーザー モードで、 **Break**コマンドは、デバッガーを中断するターゲット アプリケーションを実行します。 デバッガーにアクティブになる、ターゲット アプリケーションが停止して、デバッガー コマンドを入力することができます。

デバッガーがアクティブで既に場合**中断**対象アプリケーションには影響しません。 ただし、このコマンドを使用すると、デバッガー コマンドを終了します。 長い表示を要求し、任意数を表示したくない場合など**中断**は、表示を終了し、デバッガーのコマンド プロンプトに戻ります。

WinDbg を使用したリモート デバッグを実行している場合は、ホスト コンピューターのキーボードに Break キー キーを押すことができます。 ターゲット コンピューターのキーボードからの離別を発行する場合は、x86 ベースのコンピューター CTRL + C を使用します。

コマンド プロンプトを開き、デバッグ対象アプリケーションがビジー状態のときに F12 キーを押すことができます。 ターゲット アプリケーションの windows のいずれかをクリックし、ターゲット コンピューターで f12 キーを押します。

### <a name="span-idkernelmodeeffectsspanspan-idkernelmodeeffectsspankernel-mode-effects"></a><span id="kernel_mode_effects"></span><span id="KERNEL_MODE_EFFECTS"></span>カーネル モードの効果

カーネル モードで、 **Break**コマンドにより、デバッガーを中断する対象のコンピュータ。 このコマンドは、ターゲット コンピューターをロックし、デバッガーを起動します。

実行されているシステムをデバッグする場合は、最初のコマンド プロンプトを開き、ホスト キーボードで Break キーを押す必要があります。

デバッガーがアクティブで既に場合**中断**ターゲット コンピューターには影響しません。 ただし、このコマンドを使用すると、デバッガー コマンドを終了します。 長い表示を要求し、任意数を表示したくない場合など**中断**は、表示を終了し、デバッガーのコマンド プロンプトに戻ります。

使用することも**中断**を長いディスプレイやターゲット コンピューターがビジー状態の場合、デバッガー コマンドを生成するときにコマンド プロンプトを開きます。 X86 ベースのコンピューターをデバッグする場合は、効果は同じターゲット キーボードの CTRL キーを押しながら C キーを押すこともできます。

SYSRQ キー (または拡張キーボードの ALT + SYSRQ キーを押して) は似ています。 このキーは、すべてのプロセッサ上のホストまたはターゲットのキーボードから動作します。 ただし、このキーは、前に少なくとも 1 回の CTRL + C を押してプロンプトを開いていた場合にのみ機能します。

SYSRQ キーを無効にするには、レジストリを編集します。 HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス\\i8042prt\\パラメーター レジストリ キーをという名前の値を作成する**BreakOnSysRq** DWORD 0x0 と等しく設定します。 次に、コンピューターを再起動します。 コンピューターを再起動した後、ターゲット コンピューターのキーボードで SYSRQ キーを押すことができ、カーネル デバッガーを損なうことはありません。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

KD、CDB で対応するキーは[ **CTRL + C**](ctrl-c--break-.md)します。 プログラムの実行を制御する他の方法の詳細については、次を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

 

 





