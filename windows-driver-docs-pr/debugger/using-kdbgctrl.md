---
title: KDbgCtrl の使用
description: KDbgCtrl の使用
ms.assetid: 386e8861-dd55-440c-9309-7e8cf6c27690
keywords:
- KDbgCtrl
- KDbgCtrl, basic use
- による DbgPrint のバッファー、バッファー サイズを変更します。
- バッファーによる DbgPrint KDbgCtrl ユーティリティ
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: ee250977198e420ec2a818d18e9953f4efcf9193
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581188"
---
# <a name="using-kdbgctrl"></a>KDbgCtrl の使用


カーネル デバッグ対象のコンピューターから接続を制御する KDbgCtrl (カーネル デバッグ コントロール、kdbgctrl.exe) ツールを使用できます。

このツールを使用するには、ターゲット コンピューターで Windows Server 2003 または Windows の以降のバージョンが実行されている必要があります。

KDbgCtrl には、5 つの設定を制御できます。完全なカーネル デバッグ、自動のカーネル デバッグ、ユーザー モード エラーの処理、ブロックのカーネル デバッグ、およびによる DbgPrint バッファーのサイズ。

KDbgCtrl を使用するには、必要がありますが既に有効にするカーネルの最後の起動前に、ターゲット コンピューターのブート設定でのデバッグします。 KDbgCtrl は、これが行われていない場合のカーネル デバッグを有効にするのには使用できません。 参照してください[ブート デバッグを有効にするパラメーター](https://msdn.microsoft.com/library/windows/hardware/ff542279)のこれらの詳細については、設定を起動します。

### <a name="span-idfullkerneldebuggingspanspan-idfullkerneldebuggingspanfull-kernel-debugging"></a><span id="full_kernel_debugging"></span><span id="FULL_KERNEL_DEBUGGING"></span>完全なカーネル デバッグ

完全なカーネル デバッグを有効にすると、ホスト コンピューターで実行されているカーネル デバッガーは、ターゲット コンピューターに分割できます。 対象のコンピュータは、カーネル モードの例外が発生する場合、カーネル デバッガーに中断されます。 など、ホストをターゲットからメッセージ**による DbgPrint**出力、シンボルの読み込みメッセージ、およびリダイレクト ユーザー モード デバッガーも使用できます。

この設定が無効になっている場合は、ターゲット ホスト コンピューターからすべてのシグナルが無視されます。

完全なカーネル デバッグは、既定で有効です。 現在の設定値を確認するには、使用**kdbgctrl-c**します。 この設定を無効にするには、 **kdbgctrl-d**します。 この設定を有効にするには、 **kdbgctrl-e**します。

使用することができます、現在の設定を確認し、バッチ ファイル内での実行を制御する場合、 **kdbgctrl cx**コマンド。 詳細については、このコマンドは、次を参照してください。 [ **KDbgCtrl コマンド ライン オプション**](kdbgctrl-command-line-options.md)します。

### <a name="span-idautomatickerneldebuggingspanspan-idautomatickerneldebuggingspanautomatic-kernel-debugging"></a><span id="automatic_kernel_debugging"></span><span id="AUTOMATIC_KERNEL_DEBUGGING"></span>自動のカーネル デバッグ

完全なカーネルのデバッグが有効になっている場合、自動カーネル デバッグの現在の設定から素材--のすべての通信が許可されています。

完全なカーネル デバッグを無効にすると、自動カーネル デバッグが有効になっている、対象のコンピュータのみがデバッグ接続を開始できます。

この場合は、カーネル モードの例外のみ、ブレークポイント、またはその他のカーネル モード イベントが発生接続を確立します。 接続は確立されません**による DbgPrint**出力、シンボルの読み込みメッセージ、リダイレクトされたユーザー モード デバッガーの入力と出力、またはその他のようなメッセージ--これらに送信されるのではなくによる DbgPrint のバッファーに格納しますカーネル デバッガーです。

例外またはイベントにより、ターゲット、カーネル デバッガーを中断するかどうかは、完全なカーネル デバッグは自動的にオンになります、実行した場合と同様**kdbgctrl-e**します。

既定では自動でカーネル デバッグが無効になっています (ただし、完全なカーネル デバッグを無効にもしない限り、素材ではありません)。 現在の設定値を確認するには、使用**kdbgctrl ca**します。 この設定を無効にするには、 **kdbgctrl-da**します。 この設定を有効にするには、 **kdbgctrl ea**します。

### <a name="span-idusermodeerrorhandlingspanspan-idusermodeerrorhandlingspanuser-mode-error-handling"></a><span id="user_mode_error_handling"></span><span id="USER_MODE_ERROR_HANDLING"></span>ユーザー モードのエラー処理

ユーザー モード エラーの処理を有効にすると、一部のユーザー モード イベントは、カーネル デバッガーを中断する対象のコンピュータになります。

具体的には、すべて**int 3** - デバッガーでコードに挿入されたブレークポイントなどを中断または呼び出し**DbgBreakPoint** --カーネル デバッガーにブレークが発生します。 ただし、アクセス違反--0 除算などの標準的な例外--は通常は送信されませんカーネル デバッガーにします。

ユーザー モード デバッガーがプロセスに既に結び付けられている、このデバッガーは、すべてのユーザー モードのエラーをキャプチャし、カーネル デバッガーには、alterted はできません。 さまざまなユーザー モードのエラー ハンドラーの優先順位を付け、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。

ユーザー モード エラーの処理関数を完全なカーネル デバッグまたは自動でカーネル デバッグする必要があります有効にするも。

既定では、ユーザー モード エラーの処理を有効になっています。 現在の設定値を確認するには、使用**kdbgctrl-cu**します。 この設定を無効にするには、 **kdbgctrl-du**します。 この設定を有効にするには、 **kdbgctrl eu**します。

### <a name="span-idblockingkerneldebuggingspanspan-idblockingkerneldebuggingspanblocking-kernel-debugging"></a><span id="blocking_kernel_debugging"></span><span id="BLOCKING_KERNEL_DEBUGGING"></span>カーネル デバッグをブロック

場合によっては、カーネルのデバッグ対象のコンピュータを設定するをターゲット コンピューターが起動した後に、カーネルがまでデバッグを有効にする可能性があります。 カーネル デバッグをブロックしているを行うことができます。

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。
> テストが完了すると、これらのセキュリティ機能を再度有効にし、適切なセキュリティ機能を無効にするテスト PC を管理します。

カーネル デバッグをブロックするには、次のようなコマンドを使用して、ターゲット コンピューターを設定します。

```console
bcdedit /debug on
bcdedit /dbgsettings 1394 channel:32 /start DISABLE /noumex
```

対象のコンピュータを再起動するは、デバッグ、カーネルの準備しますが、カーネル デバッグと、ユーザー モード エラーの処理が無効になります。 その時点では、ホスト コンピューターでは、ターゲット コンピューターに接続できません、バグ チェックは、カーネル デバッガーによってキャッチされないと、ユーザー モード例外では、カーネル デバッガーを中断は発生しません。

準備ができたら、次のコマンドを入力して (ターゲット コンピューターの再起動) なしのカーネル デバッグを有効にできます。

```console
kdbgctrl -db
kdbgctrl -e
```

後で、次のコマンドを入力してカーネル デバッグを無効にすることができます。

```console
kdbgctrl -d
kdbgctrl -eb
```

使用することができます**kdbgctrl cb**カーネル デバッグがブロックされているかどうかを確認します。

### <a name="span-idthedbgprintbuffersizespanspan-idthedbgprintbuffersizespanthe-dbgprint-buffer-size"></a><span id="the_dbgprint_buffer_size"></span><span id="THE_DBGPRINT_BUFFER_SIZE"></span>による DbgPrint のバッファー サイズ

による DbgPrint バッファーは、ターゲット コンピューターが、カーネル デバッガーに送信されるメッセージを格納します。

完全なカーネル デバッグを有効にすると、これらのメッセージは、カーネル デバッガーで自動的に表示されます。 ただし、これらのメッセージをバッファーに格納する場合、このオプションが無効になっています。 時間の後で、カーネル デバッグを有効にする、カーネル デバッガーに接続して使用して、、 [ **! による dbgprint** ](-dbgprint.md)拡張機能をこのバッファーの内容を参照してください。 このバッファーの詳細については、「による DbgPrint バッファーを参照してください。

による DbgPrint バッファーの既定のサイズは、Windows、および 32 KB の空きビルドを Windows のチェック ビルド時に 4 KB です。 現在のバッファー サイズを決定するには使用**kdbgctrl cdb**します。 バッファー サイズを変更する **kdbgctrl sdb * * * サイズ*ここで、*サイズ*新しいバッファーのサイズを指定します。 構文の詳細については、次を参照してください。 [ **KDbgCtrl コマンド ライン オプション**](kdbgctrl-command-line-options.md)します。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

現在のすべての設定を表示するには、次のコマンドを使用します。

```console
kdbgctrl -c -ca -cu -cb -cdb 
```

既定の設定を復元するには、次のコマンドを使用します。

```console
kdbgctrl -e -da -eu -db -sdb 0x1000 
```

例外にのみ接続されたように、ホスト コンピューターをロックアウトするには、次のコマンドを使用します。

```console
kdbgctrl -d -ea -eu 
```

すべてのカーネル デバッグを無効にするには、次のコマンドを使用します。

```console
kdbgctrl -d -da 
```

すべてのカーネル デバッグを無効にする場合、による DbgPrint バッファーのサイズを大きくたい場合がありますもします。 これは、後で表示する必要がある場合に、すべてのメッセージを保存することを保証します。 メモリのメガバイト数がある場合は、次のコマンドを使用する場合があります。

```console
kdbgctrl -sdb 0x100000 
```

 

 





