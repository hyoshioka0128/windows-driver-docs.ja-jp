---
title: KDbgCtrl の使用
description: KDbgCtrl の使用
ms.assetid: 386e8861-dd55-440c-9309-7e8cf6c27690
keywords:
- KDbgCtrl
- KDbgCtrl、基本的な用途
- DbgPrint バッファー、変更 (バッファーサイズを)
- DbgPrint バッファー、KDbgCtrl ユーティリティ
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: c85a8138f6fceaadcbb8340123cbc198ac992afb
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209656"
---
# <a name="using-kdbgctrl"></a>KDbgCtrl の使用


KDbgCtrl (カーネルデバッグコントロール、kdbgctrl .exe) ツールを使用すると、ターゲットコンピューターからカーネルデバッグ接続を制御できます。

このツールを使用するには、対象のコンピューターで windows Server 2003 以降のバージョンの Windows が実行されている必要があります。

KDbgCtrl は、完全なカーネルデバッグ、自動カーネルデバッグ、ユーザーモードエラー処理、カーネルデバッグのブロック、および DbgPrint バッファーのサイズの5つの異なる設定を制御できます。

KDbgCtrl を使用するには、最後に起動する前に対象コンピューターのブート設定でカーネルデバッグを有効にしておく必要があります。 この操作が行われていない場合、KDbgCtrl を使用してカーネルデバッグを有効にすることはできません。 これらのブート設定の詳細については[、「ブートパラメーター」を](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-enable-debugging)参照してデバッグを有効にしてください。

### <a name="span-idfull_kernel_debuggingspanspan-idfull_kernel_debuggingspanfull-kernel-debugging"></a><span id="full_kernel_debugging"></span><span id="FULL_KERNEL_DEBUGGING"></span>完全なカーネルデバッグ

完全なカーネルデバッグが有効になっていると、ホストコンピューター上で実行されているカーネルデバッガーが対象のコンピューターに侵入する可能性があります。 カーネルモードの例外が発生した場合、ターゲットコンピューターはカーネルデバッガーに侵入します。 ターゲットからホストへのメッセージ ( **Dbgprint**出力、シンボル読み込みメッセージ、リダイレクトされたユーザーモードデバッガーなど) も使用できます。

この設定を無効にした場合、ホストコンピューターからのすべての信号はターゲットによって無視されます。

既定では、完全なカーネルデバッグが有効になっています。 現在の設定値を確認するには、 **kdbgctrl-c**を使用します。 この設定を無効にするには、 **kdbgctrl-d**を使用します。 この設定を有効にするには、 **kdbgctrl-e**を使用します。

現在の設定を確認し、それを使用してバッチファイル内の実行を制御する場合は、 **kdbgctrl-cx**コマンドを使用できます。 このコマンドの詳細については、「 [**Kdbgctrl のコマンドラインオプション**](kdbgctrl-command-line-options.md)」を参照してください。

### <a name="span-idautomatic_kernel_debuggingspanspan-idautomatic_kernel_debuggingspanautomatic-kernel-debugging"></a><span id="automatic_kernel_debugging"></span><span id="AUTOMATIC_KERNEL_DEBUGGING"></span>カーネルの自動デバッグ

完全なカーネルデバッグが有効になっている場合、カーネルの自動デバッグの現在の設定は問題でであり、すべての通信が許可されます。

完全なカーネルデバッグが無効になっており、カーネルの自動デバッグが有効になっている場合は、ターゲットコンピューターのみがデバッグ接続を開始できます。

この場合、カーネルモードの例外、ブレークポイント、またはその他のカーネルモードイベントのみが接続を確立します。 この接続は、 **dbgprint**出力、シンボル読み込みメッセージ、リダイレクトされたユーザーモードのデバッガーの入力と出力、またはその他の同様のメッセージに対して確立されません。これらは、カーネルデバッガーに送信されるのではなく、dbgprint バッファーに格納されます。

例外またはイベントによってターゲットがカーネルデバッガーに分割されると、 **kdbgctrl-e**を実行した場合と同様に、完全なカーネルデバッグが自動的に有効になります。

既定では、自動カーネルデバッグは無効になっています (ただし、完全なカーネルデバッグも無効になっている場合を除き、これは問題でです)。 現在の設定値を確認するには、 **kdbgctrl-ca**を使用します。 この設定を無効にするには、 **kdbgctrl + da**を使用します。 この設定を有効にするには、 **kdbgctrl-ea**を使用します。

### <a name="span-iduser_mode_error_handlingspanspan-iduser_mode_error_handlingspanuser-mode-error-handling"></a><span id="user_mode_error_handling"></span><span id="USER_MODE_ERROR_HANDLING"></span>ユーザーモードのエラー処理

ユーザーモードのエラー処理が有効になっていると、一部のユーザーモードイベントによって対象のコンピューターがカーネルデバッガーで中断されます。

具体的には、デバッガーによってコードに挿入されたブレークポイントや**Dbgbreakpoint ポイント**の呼び出しなど、すべての**int 3**割り込みがカーネルデバッガーを中断します。 ただし、一般的な例外 (アクセス違反や0による除算など) は、通常、カーネルデバッガーに送信されません。

ユーザーモードのデバッガーが既にプロセスにアタッチされている場合、このデバッガーはすべてのユーザーモードエラーをキャプチャし、カーネルデバッガーは alterted されません。 さまざまなユーザーモードエラーハンドラーの優先順位のランク付けについては、「[事後分析デバッグの有効化](enabling-postmortem-debugging.md)」を参照してください。

ユーザーモードのエラー処理を機能させるには、完全なカーネルデバッグまたは自動カーネルデバッグの両方を有効にする必要があります。

ユーザーモードのエラー処理は、既定で有効になっています。 現在の設定値を確認するには、 **kdbgctrl-cu**を使用します。 この設定を無効にするには、 **kdbgctrl-du**を使用します。 この設定を有効にするには、 **kdbgctrl-eu**を使用します。

### <a name="span-idblocking_kernel_debuggingspanspan-idblocking_kernel_debuggingspanblocking-kernel-debugging"></a><span id="blocking_kernel_debugging"></span><span id="BLOCKING_KERNEL_DEBUGGING"></span>ブロック (カーネルデバッグを)

場合によっては、対象のコンピューターをカーネルデバッグ用にセットアップし、対象のコンピューターが起動するまでカーネルデバッグを有効にすることが必要になる場合があります。 これは、カーネルデバッグをブロックすることによって行うことができます。

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。
> セキュリティ機能が無効になっている場合は、テストが完了し、テスト PC を適切に管理するときに、これらのセキュリティ機能を再び有効にします。

カーネルデバッグをブロックするには、次のようなコマンドを使用して、対象のコンピューターを設定します。

```console
bcdedit /debug on
bcdedit /dbgsettings 1394 channel:32 /start DISABLE /noumex
```

ターゲットコンピューターを再起動すると、カーネルデバッグ用に準備されますが、カーネルデバッグとユーザーモードエラー処理は無効になります。 その時点で、ホストコンピューターはターゲットコンピューターに接続できません。また、カーネルデバッガーによってバグチェックが検出されず、ユーザーモードの例外によってカーネルデバッガーが中断されることはありません。

準備ができたら、次のコマンドを入力して、(対象のコンピューターを再起動せずに) カーネルデバッグを有効にすることができます。

```console
kdbgctrl -db
kdbgctrl -e
```

次のコマンドを入力すると、後でカーネルデバッグを無効にすることができます。

```console
kdbgctrl -d
kdbgctrl -eb
```

**Kdbgctrl-cb**を使用して、カーネルデバッグがブロックされているかどうかを確認できます。

### <a name="span-idthe_dbgprint_buffer_sizespanspan-idthe_dbgprint_buffer_sizespanthe-dbgprint-buffer-size"></a><span id="the_dbgprint_buffer_size"></span><span id="THE_DBGPRINT_BUFFER_SIZE"></span>DbgPrint バッファーサイズ

DbgPrint バッファーには、対象のコンピューターがカーネルデバッガーに送信したメッセージが格納されます。

完全なカーネルデバッグが有効になっている場合、これらのメッセージは自動的にカーネルデバッガーに表示されます。 ただし、このオプションが無効になっている場合、これらのメッセージはバッファーに格納されます。 後でカーネルデバッグを有効にし、カーネルデバッガーに接続して、 [**! dbgprint**](-dbgprint.md)拡張機能を使用してこのバッファーの内容を確認することができます。 このバッファーの詳細については、「DbgPrint Buffer」を参照してください。

Windows の無料ビルドでは、DbgPrint バッファーの既定のサイズは 4 KB です。 現在のバッファーサイズを確認するには、 **kdbgctrl + cdb**を使用します。 バッファーサイズを変更するには、**kdbgctrl-sdb * * * size*を使用します。 *size*は新しいバッファーサイズを指定します。 構文の詳細については、「 [**Kdbgctrl のコマンドラインオプション**](kdbgctrl-command-line-options.md)」を参照してください。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

現在のすべての設定を表示するには、次のコマンドを使用します。

```console
kdbgctrl -c -ca -cu -cb -cdb 
```

既定の設定を復元するには、次のコマンドを使用します。

```console
kdbgctrl -e -da -eu -db -sdb 0x1000 
```

例外にのみ接続されるようにホストコンピューターをロックアウトするには、次のコマンドを使用します。

```console
kdbgctrl -d -ea -eu 
```

すべてのカーネルデバッグを無効にするには、次のコマンドを使用します。

```console
kdbgctrl -d -da 
```

すべてのカーネルデバッグを無効にする場合は、DbgPrint バッファーのサイズを大きくすることもできます。 これにより、後で表示する必要がある場合に備えて、すべてのメッセージが保存されます。 メモリが 1 mb になると、次のコマンドを使用できます。

```console
kdbgctrl -sdb 0x100000 
```

 

 





