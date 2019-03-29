---
title: 仮想アドレスによるメモリへのアクセス
description: 仮想アドレスによるメモリへのアクセス
ms.assetid: 13e97cba-c4a4-4240-99b3-88a7537b0ca8
keywords:
- メモリへのアクセス、仮想アドレス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3610080427c4c3ec3defce989d4689e994690468
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581136"
---
# <a name="accessing-memory-by-virtual-address"></a>仮想アドレスによるメモリへのアクセス


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


メモリ アドレスまたはアドレス範囲にアクセスするには、いくつかのコマンドを使用することができます。 Visual Studio と WinDbg 用意してユーザー インターフェイス要素 (およびそのコマンド) を表示およびメモリの編集を行えます。 詳細については、次を参照してください。[表示と編集のメモリと Visual Studio でのレジスタ](viewing-memory--variables--and-registers-in-visual-studio.md)と[表示と編集のメモリ WinDbg で](memory-window.md)します。

次のコマンドでは、読み取るしたり、さまざまな形式でメモリを記述することができます。 これらの形式には、16 進数のバイト数、単語 (単語、ダブル ワード、およびクアッド単語)、整数 (short、long、およびクアッド整数と符号なし整数)、浮動小数点数 (10 バイト、16 バイト、32 バイト、64 バイトおよび実数)、および ASCII 文字が含まれます。

-   [ **D\* (表示メモリ)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドは、指定されたメモリ アドレスまたは範囲の内容を表示します。

-   [ **E\* (値を入力)** ](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)コマンドでは、指定されたメモリ アドレスに値を書き込みます。

専門的なデータ型を処理するために、次のコマンドを使用できます。

-   [ **Dt (表示の種類)** ](dt--display-type-.md)さまざまなデータ型し、は、デバッグ中のアプリケーションによって作成されたデータ構造を表示します。 コマンドを検索します。 このコマンドは汎用性の高いであり、多くのバリエーションとオプション。

-   [ **DS (表示文字列)、ds** ](ds--ds--display-string-.md)コマンド表示文字列を ANSI\_文字列、または UNICODE\_文字列データの構造体。

-   [ **Dl (リンクされたリストを表示)** ](dl--display-linked-list-.md)コマンドを追跡し、リンクの一覧が表示されます。

-   [ **D\*s (表示語およびシンボル)** ](dds--dps--dqs--display-words-and-symbols-.md)ダブル ワードまたはクアッド単語シンボル情報が含まれ、データおよびシンボル情報を表示するコマンドを検索します。

-   [ **! アドレス**](-address.md)拡張機能コマンドでは、特定のアドレスにあるメモリのプロパティに関する情報を表示します。

次のコマンドを使用すると、メモリ範囲を操作します。

-   [ **M (メモリの移動)** ](m--move-memory-.md)コマンドは、別に 1 つのメモリの範囲の内容を移動します。

-   [ **F (塗りつぶしメモリ)** ](f--fp--fill-memory-.md)範囲がいっぱいになるまで繰り返しコマンドでは、メモリの範囲にパターンを書き込みます。

-   [ **C (メモリの比較)** ](c--compare-memory-.md)コマンドは、2 つのメモリ範囲の内容を比較します。

-   [ **S (メモリの検索)** ](s--search-memory-.md)コマンド メモリ範囲内の指定したパターンの検索やメモリの範囲内に存在する ASCII または Unicode 文字を検索します。

-   [ **.Holdmem (保留およびメモリの比較)** ](-holdmem--hold-and-compare-memory-.md)コマンドは、別の 1 つのメモリ範囲を比較します。

ほとんどの場合は、これらのコマンドは、現在の基数でのパラメーターを解釈します。 したがって、追加する必要があります**0 x**現在基数は 16 ではない場合、16 進数のアドレスの前にします。 ただし、これらのコマンドの表示出力は、現在の基数に関係なく、16 進形式で通常です。 (出力の詳細については、個々 のコマンドのトピックを参照してください)。[メモリ ウィンドウ](memory-window.md)10 進数形式で整数と実際の数値を表示し、16 進数形式でその他の形式を表示します。

既定の基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。 簡単に数値を変換する 1 つのベースから間を使用して、 [**でしょうか。(式の評価)** ](---evaluate-expression-.md)コマンドまたは[ **(番号の形式の表示) .formats** ](-formats--show-number-formats-.md)コマンド。

ユーザー モードのデバッグを実行している場合は、仮想アドレスの意味は、現在のプロセスによって決まります。 カーネル モードのデバッグを実行している場合は、仮想アドレスの意味は、デバッガーによって制御できます。 詳細については、次を参照してください。[プロセス コンテキスト](changing-contexts.md#process-context)します。

 

 





