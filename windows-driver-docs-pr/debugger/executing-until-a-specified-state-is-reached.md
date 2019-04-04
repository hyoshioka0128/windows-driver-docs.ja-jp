---
title: 実行されるまで、指定された状態に到達します。
description: 実行されるまで、指定された状態に到達します。
ms.assetid: 0657a7bf-4d72-4248-9e45-d79d51b91139
keywords:
- 達するまで、指定した状態を実行します。
- ブレークポイント、実行を制御するために使用
- ブレークポイントと擬似レジスタ
- スクリプト ファイル、実行を制御するために使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b49c5dee6c4e08093349fc75ae19f3686104a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531318"
---
# <a name="executing-until-a-specified-state-is-reached"></a>実行されるまで、指定された状態に到達します。


## <span id="ddk_determining_the_acl_of_an_object_dbg"></span><span id="DDK_DETERMINING_THE_ACL_OF_AN_OBJECT_DBG"></span>


指定した状態に到達するまでの実行にターゲットをいくつかの方法はあります。

### <a name="span-idusingabreakpointtocontrolexecutionspanspan-idusingabreakpointtocontrolexecutionspanusing-a-breakpoint-to-control-execution"></a><span id="using_a_breakpoint_to_control_execution"></span><span id="USING_A_BREAKPOINT_TO_CONTROL_EXECUTION"></span>コントロールの実行にブレークポイントを使用します。

1 つのメソッドでは、ブレークポイントを使用します。 最も単純なブレークポイントは、プログラム カウンターが、指定したアドレスに達すると、実行を停止します。 複雑なブレークポイントを実行できます。

-   このアドレスは、特定のスレッドによって実行される場合にのみトリガーされます。

-   トリガーできず、前に指定された数のこのアドレスを通過を許可します。

-   自動的にトリガーされると、指定したコマンドを発行または

-   そのメモリの読み取りまたは書き込みをするときにトリガーされる、非実行可能ファイルのメモリ内の指定されたアドレスをご覧ください。

詳細設定をブレークポイントを制御する方法については、[を使用してブレークポイント](using-breakpoints.md)を参照してください。

指定した状態に達するまでを実行するより複雑な方法は、使用する、*条件付きブレークポイント*します。 この種のブレークポイントは、特定のアドレスに設定されていますが、指定した条件が保持している場合にのみトリガーされます。 詳細については、[、条件付きブレークポイント](setting-a-conditional-breakpoint.md)を参照してください。

### <a name="span-idbreakpointsandpseudoregistersspanspan-idbreakpointsandpseudoregistersspanbreakpoints-and-pseudo-registers"></a><span id="breakpoints_and_pseudo_registers"></span><span id="BREAKPOINTS_AND_PSEUDO_REGISTERS"></span>ブレークポイントと擬似レジスタ

目的の状態を指定することが役立ちますを使用する*自動の擬似レジスタ*します。 これらは、デバッガーによって制御できるように、さまざまな対象の状態に関連する値を参照する変数です。

たとえば、次のブレークポイントを使用して、 **$thread**擬似レジスタは、現在のスレッドの値と等しくは常にします。 コマンドを使用すると、現在のスレッドの値に解決します。 使用して **$thread**の引数として、 **/t**のパラメーター、 [ **bp (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)コマンドではブレークポイントを作成します。毎回トリガーする**NtOpenFile**が発行した時点でアクティブなスレッドによって呼び出される、 **bp**コマンド。

```dbgcmd
kd> bp /t @$thread nt!ntopenfile
```

他のスレッドを呼び出すと、このブレークポイントはトリガーされません**NtOpenFile**します。

自動の擬似レジスタの一覧は、[擬似レジスタ構文](pseudo-register-syntax.md)を参照してください。

### <a name="span-idusingascriptfiletocontrolexecutionspanspan-idusingascriptfiletocontrolexecutionspanusing-a-script-file-to-control-execution"></a><span id="using_a_script_file_to_control_execution"></span><span id="USING_A_SCRIPT_FILE_TO_CONTROL_EXECUTION"></span>スクリプト ファイルを使用して、実行を制御するには

指定した状態に達するまでを実行する別の方法では、再帰的に、各イテレーションで、目的の状態をテスト自体を呼び出すことをスクリプト ファイルを作成します。

通常、このスクリプト ファイルが含まれます、 [ **.if** ](-if.md)と[ **.else** ](-else.md)トークンです。 などのコマンドを使用できます[ **t (トレース)** ](t--trace-.md)を 1 つの手順を実行し、対象の条件をテストします。

まで実行する場合など、 **eax**レジスタには 0x1234 値が含まれていますと呼ばれるスクリプト ファイルを作成できます*eaxstep*次の行を格納しています。

```dbgcmd
.if (@eax == 1234) { .echo 1234 } .else { t "$<eaxstep" }
```

デバッガー コマンド ウィンドウから次のコマンドを発行します。

```dbgcmd
t "$<eaxstep"
```

これは、 **t**コマンドは 1 つの手順を実行し、引用符で囲まれたコマンドを実行します。 このコマンドは[  **$ &lt; (スクリプト ファイルを実行)**](-----------------------a---run-script-file-.md)、実行に使用する、 *eaxstep*ファイル。 スクリプト ファイルの値をテストする**eax**、実行、 **t**コマンド、および、呼び出し自体を再帰的にします。 これまで、 **eax** equals 0x1234、この時点での登録、 [ **.echo (エコー コメント)** ](-echo--echo-comment-.md)コマンドでは、デバッガー コマンド] ウィンドウ、および実行するメッセージを出力します。停止します。

スクリプト ファイルの詳細については、「[スクリプト ファイルを使用する](using-script-files.md)と[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

 

 





