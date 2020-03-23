---
title: Windows のデバッグの概要
description: このセクションでは、Windows のデバッグの開始方法について説明します。 デバッガーを使用してクラッシュ ダンプを分析することが目的の場合は、Windows デバッガー (WinDbg) を使用したクラッシュ ダンプの分析に関するページを参照してください。
ms.assetid: 4981928E-A33D-4F60-AAA0-124C360B7E03
ms.date: 08/23/2018
ms.localizationpriority: high
ms.openlocfilehash: 9e62ff14ef3e006c85bf880a1f27ed885a655bbf
ms.sourcegitcommit: 29d9e97439f19d2c5a090006640e4e5659e56412
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2020
ms.locfileid: "78335959"
---
# <a name="getting-started-with-windows-debugging"></a>Windows のデバッグの概要


この記事では、Windows のデバッグの開始方法について説明します。 デバッガーを使用してクラッシュ ダンプを分析することが目的の場合は、「[WinDbg を使用してクラッシュ ダンプ ファイルを分析する](crash-dump-files.md)」を参照してください。

Windows のデバッグを開始するには、この記事で説明されているタスクを完了します。

## <a name="1-determine-the-host-and-the-target"></a>1.ホストとターゲットを決定する 

デバッガーは "*ホスト*" システムで実行され、デバッグするコードは "*ターゲット*" システムで実行されます。

   **ホスト &lt;--------------------------------------------------&gt; ターゲット**

![二重の矢印で結び付けられたホスト PC とターゲット PC](images/targethost1.png)

プロセッサでの命令の実行は、デバッグ時には停止されるのが一般的であるため、通常は 2 台のコンピューター システムが使用されます。 場合によっては、仮想マシンを 2 台目のシステムとして使用できることもあります。 たとえば、デバッグする必要のあるコードと同じ PC で実行されている仮想 PC を使用できる場合があります。 ただし、コードが低レベルのハードウェアと通信している場合は、仮想 PC を使用するのは最善の方法ではない可能性があります。 詳細については、「[仮想マシンのネットワーク デバッグの設定 - KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)」を参照してください。

## <a name="2-determine-the-type-kernel-mode-or-user-mode"></a>2.種類 (カーネルモードまたはユーザーモード) を決定する

次に、カーネルモードとユーザーモードのどちらでデバッグを行うかを決定する必要があります。

"*カーネル モード*" は、オペレーティング システムと特権プログラムが実行されるプロセッサアクセス モードです。 カーネルモード コードには、システムの任意の部分にアクセスするためのアクセス許可があり、ユーザーモード コードのように制限されていません。 カーネルモード コードでは、ユーザー モードまたはカーネル モードのいずれかで実行されている他のプロセスの任意の部分にアクセスできます。 コア OS 機能の大部分と多くのハードウェア デバイス ドライバーは、カーネル モードで実行されます。

"*ユーザー モード*" は、コンピューター上でアプリケーションとサブシステムが実行されるモードです。 ユーザー モードで実行されるプロセスは、独自の仮想アドレス空間内で実行されます。 これらは、システムの多くの部分に直接アクセスすることが制限されています。これには、システム ハードウェア、使用するために割り当てられていないメモリ、システムの整合性を損なう可能性があるシステムのその他の部分などが含まれます。 ユーザー モードで実行されるプロセスは、システムおよびその他のユーザーモード プロセスから事実上分離されるため、これらのリソースに干渉することはできません。

ドライバーをデバッグすることが目的の場合は、ドライバーがカーネルモード ドライバーなのか、ユーザーモード ドライバーなのかを確認します。 Windows Driver Model (WDM) ドライバーとカーネルモード ドライバー フレームワーク (KMDF) は、どちらもカーネルモード ドライバーです。 名前が示すように、ユーザー モード ドライバー フレームワーク (UMDF) ドライバーはユーザーモード ドライバーです。

問題によっては、コードがどのモードで実行されるかを判断するのが困難な場合があります。 その場合は、1 つのモードを選択し、そのモードで入手可能な情報を確認する必要があります。 一部の問題では、ユーザー モードとカーネル モードの両方でデバッガーを使用する必要があります。

どのモードでデバッグするかに応じて、異なる方法でデバッガーを構成して使用する必要があります。 両方のモードで同じように動作するデバッグ コマンドもあれば、モードによって動作が異なるコマンドもあります。

カーネル モードでのデバッガーの使用の詳細については、次の記事を参照してください。
   - [WinDbg の概要 (カーネル モード)](getting-started-with-windbg--kernel-mode-.md) 
   - [ユニバーサル ドライバーのデバッグ - ステップ バイ ステップ ラボ (Echo カーネル モード)](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md) 
   - [ドライバーのデバッグ - ステップ バイ ステップ ラボ (Sysvad カーネルモード)](debug-universal-drivers--kernel-mode-.md)。 
    
ユーザー モードでのデバッガーの使用の詳細については、「[WinDbg の概要 (ユーザー モード)](getting-started-with-windbg.md)」を参照してください。

## <a name="3-choose-your-debugger-environment"></a>3.デバッガー環境を選択する

WinDbg は、ほとんどの状況で適切に機能しますが、別のデバッガー (自動化や Visual Studio のコンソール デバッガーなど) を使用することが必要になる場合があります。 詳細については、「[デバッグ環境](debuggers-in-the-debugging-tools-for-windows-package.md)」を参照してください。

## <a name="4-determine-how-to-connect-the-target-and-host"></a>4.ターゲットとホストの接続方法を決定する

通常、ターゲット システムとホスト システムはイーサネット ネットワークによって接続されています。 初期の起動作業を行っている場合、またはデバイスにイーサネット接続がない場合は、他のネットワーク接続オプションを使用できます。 詳しくは、次の記事をご覧ください。
   -   [KDNET ネットワーク カーネル デバッグの自動設定](setting-up-a-network-debugging-connection-automatically.md)
   -   [カーネルモード デバッグの設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
   -   [KDNET ネットワーク カーネル デバッグの手動設定](setting-up-a-network-debugging-connection.md)
   -   [仮想マシンのネットワーク デバッグの設定 - KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)

## <a name="5-choose-either-the-32-bit-or-64-bit-debugging-tools"></a>5.32 ビットまたは 64 ビットのいずれかのデバッグ ツールを選択する

32 ビットまたは 64 ビットのどちらのデバッグ ツールを選択するかは、ターゲット システムとホスト システムで実行されている Windows のバージョンと、32 ビットまたは 64 ビットのどちらのコードをデバッグしているかによって異なります。 詳細については、「[32 ビットまたは 64 ビット デバッグ ツールの選択](choosing-a-32-bit-or-64-bit-debugger-package.md)」を参照してください。

## <a name="6-configure-symbols"></a>6.シンボルを構成する

WinDbg で提供されている高度な機能のすべてを使用するには、適切なシンボルを読み込む必要があります。 シンボルが適切に構成されていない場合は、シンボルに依存する機能を使用しようとしたときに、そのシンボルが使用できないことを示すメッセージが表示されます。 詳細については、「[Windows デバッグ用シンボル (WinDbg、KD、CDB、NTSD)](symbols.md)」を参照してください。

## <a name="7-configure-source-code"></a>7.ソース コードを構成する

独自のソース コードをデバッグすることが目的の場合は、そのソース コードへのパスを構成する必要があります。 詳細については、「[ソース パス](source-path.md)」を参照してください。

## <a name="8-become-familiar-with-debugger-operation"></a>8.デバッガーの操作に慣れる

このドキュメントの「[デバッガーの操作](debugger-operation-win8.md)」セクションでは、さまざまなタスクのデバッガー操作について説明しています。 たとえば、「[デバッガー拡張機能 DLL の読み込み](loading-debugger-extension-dlls.md)」では、デバッガー拡張機能を読み込む方法について説明しています。 WinDbg の操作の詳細については、「[WinDbg を使用したデバッグ](debugging-using-windbg.md)」を参照してください。

## <a name="9-become-familiar-with-debugging-techniques"></a>9.デバッグ手法について理解を深める

[標準的なデバッグ手法](standard-debugging-techniques.md)は、ほとんどのデバッグ シナリオに適用されます。例として、ブレークポイントの設定、呼び出し履歴の検査、メモリ リークの検出などがあります。 [特殊なデバッグ手法](specialized-debugging-techniques.md)は、特定のテクノロジまたはコードの種類に適用されます。 例として、プラグ アンド プレイのデバッグ、KMDF のデバッグ、RPC のデバッグなどがあります。

## <a name="10-use-the-debugger-reference-commands"></a>10.デバッガーの参照コマンドを使用する

そのうちに、デバッガーでの作業にさまざまなデバッグ コマンドを使用するようになります。 デバッグ コマンドに関するヘルプ情報を表示するには、デバッガーで [ **.hh** (HTML ヘルプ ファイルを開く)](-hh--open-html-help-file-.md) コマンドを使用します。 使用可能なコマンドの詳細については、「[デバッガー リファレンス](debugger-reference.md)」を参照してください。

## <a name="11-use-debugging-extensions-for-specific-technologies"></a>11.特定のテクノロジに対してデバッグ拡張機能を使用する

ドメイン固有のデータ構造の解析を提供する複数のデバッグ拡張機能があります。 詳細については、「[特殊な拡張機能](specialized-extensions.md)」を参照してください。

## <a name="12-learn-about-related-windows-internals"></a>12.関連する Windows の内部構造を知る

このドキュメントでは、Windows の内部構造に関する知識があることを前提としています。 Windows の内部構造 (メモリ使用量、コンテキスト、スレッド、プロセスなど) の詳細については、『[*Windows Internals*](https://docs.microsoft.com/sysinternals/learn/windows-internals)』(Mark Russinovich、David Solomon、Alex Ionescu 著) などのその他のリソースをご確認ください。

## <a name="13-review-additional-debugging-resources"></a>13.その他のデバッグに関するリソースを確認する

その他のリソースには、次の書籍とビデオが含まれます。
-  *Inside Windows Debugging:Practical Debugging and Tracing Strategies* (Tarik Soulami 著)
-   *Advanced Windows Debugging*(Mario Hewardt、Daniel Pravat 著)
-   [Defrag Tools](https://channel9.msdn.com/Shows/Defrag-Tools) (デフラグ ツール) のエピソード 13 から 29、WinDbg について


## <a name="see-also"></a>関連項目

-   [WinDbg の概要 (カーネル モード)](getting-started-with-windbg--kernel-mode-.md)
-   [WinDbg の概要 (ユーザー モード)](getting-started-with-windbg.md)
-   [32 ビットまたは 64 ビット デバッグ ツールの選択](choosing-a-32-bit-or-64-bit-debugger-package.md)
-   [デバッグ環境](debuggers-in-the-debugging-tools-for-windows-package.md)
-   [デバッグの設定 (カーネルモードとユーザーモード)](getting-set-up-for-debugging.md)
-   [ユニバーサル ドライバーのデバッグ - ステップ バイ ステップ ラボ (Echo カーネル モード)](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)
-   [ドライバーのデバッグ - ステップ バイ ステップ ラボ (Sysvad カーネルモード)](debug-universal-drivers--kernel-mode-.md)
