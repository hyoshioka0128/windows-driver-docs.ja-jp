---
title: Windows のデバッグの概要
description: このセクションでは、Windows デバッグの開始方法について説明します。 デバッガーを使用してクラッシュダンプを分析することが目的の場合は、「Windows デバッガー (WinDbg) を使用したクラッシュダンプ分析」を参照してください。
ms.assetid: 4981928E-A33D-4F60-AAA0-124C360B7E03
ms.date: 08/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: e909a4f85834d90396b0ce5d1c5724061ca15d38
ms.sourcegitcommit: b795323cafe6b38918a33d3ecdf6b1a46215693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2019
ms.locfileid: "70839644"
---
# <a name="getting-started-with-windows-debugging"></a>Windows のデバッグの概要


この記事では、Windows デバッグの開始方法について説明します。 デバッガーを使用してクラッシュダンプを分析することが目的の場合は、「 [WinDbg を使用してクラッシュダンプファイルを分析](crash-dump-files.md)する」を参照してください。

Windows デバッグを開始するには、この記事で説明されているタスクを実行します。

## <a name="1-determine-the-host-and-the-target"></a>1. ホストとターゲットを決定する 

デバッガーは*ホスト*システムで実行され、デバッグするコードは*ターゲット*システムで実行されます。

   **ホスト&lt; ターゲット-------------------------------------------------- &gt;**

![2つの矢印で接続されたホストとターゲット pc](images/targethost1.png)

デバッグ中はプロセッサで命令の実行を停止するのが一般的であるため、通常は2つのコンピューターシステムが使用されます。 場合によっては、仮想マシンを2番目のシステムとして使用できることもあります。 たとえば、デバッグする必要のあるコードと同じ PC で実行されている仮想 PC を使用できる場合があります。 ただし、コードが低レベルのハードウェアに通信している場合は、仮想 PC を使用するのが最善の方法ではない可能性があります。 詳細については、「[仮想マシンのネットワークデバッグの設定-KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)」を参照してください。

## <a name="2-determine-the-type-kernel-mode-or-user-mode"></a>2. カーネルモードまたはユーザーモードの種類を決定します。

次に、カーネルモードとユーザーモードのどちらのデバッグを行うかを決定する必要があります。

*カーネルモード*は、オペレーティングシステムと特権プログラムが実行されるプロセッサアクセスモードです。 カーネルモードのコードには、システムの任意の部分にアクセスするためのアクセス許可があり、ユーザーモードコードのように制限されていません。 カーネルモードのコードは、ユーザーモードまたはカーネルモードで実行されている他のプロセスの任意の部分にアクセスできます。 コア OS 機能と多くのハードウェアデバイスドライバーは、カーネルモードで実行されます。

*ユーザーモード*は、コンピューター上のアプリケーションとサブシステムがで実行するモードです。 ユーザーモードで実行されるプロセスは、独自の仮想アドレス空間内で実行されます。 システムハードウェア、使用するために割り当てられていないメモリ、システムの整合性を損なう可能性があるシステムのその他の部分など、システムの多くの部分に直接アクセスすることが制限されています。 ユーザーモードで実行されるプロセスはシステムおよびその他のユーザーモードプロセスから事実上分離されるため、これらのリソースに干渉することはできません。

ドライバーをデバッグすることが目的の場合は、ドライバーがカーネルモードドライバーであるか、ユーザーモードドライバーであるかを確認します。 Windows Driver Model (WDM) ドライバーとカーネルモードドライバーフレームワーク (KMDF) は両方ともカーネルモードドライバーです。 名前が sugests の場合、ユーザーモードドライバーフレームワーク (UMDF) ドライバーはユーザーモードドライバーです。

問題によっては、コードがどのモードで実行されるかを判断するのが困難な場合があります。 その場合は、1つのモードを選択し、そのモードで使用できる情報を確認する必要があります。 一部の問題では、ユーザーモードとカーネルモードの両方でデバッガーを使用する必要があります。

どのモードでデバッグするかに応じて、さまざまな方法でデバッガーを構成して使用する必要があります。 一部のデバッグコマンドは、両方のモードで同じように動作します。また、モードによって動作が異なるコマンドもあります。

カーネルモードでのデバッガーの使用の詳細については、次の記事を参照してください。
   - [WinDbg の概要 (カーネルモード)](getting-started-with-windbg--kernel-mode-.md) 
   - [ユニバーサルドライバーのデバッグ-ステップバイステップラボ (カーネルモードのエコー)](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md) 
   - [デバッグドライバー-ステップバイステップラボ (Sysvad カーネルモード)](debug-universal-drivers--kernel-mode-.md)。 
    
ユーザーモードでのデバッガーの使用の詳細については、「 [WinDbg の概要 (ユーザーモード)](getting-started-with-windbg.md)」を参照してください。

## <a name="3-choose-your-debugger-environment"></a>3.デバッガー環境の選択

ほとんどの場合、WinDbg は適切に機能しますが、オートメーションや Visual Studio のコンソールデバッガーなど、別のデバッガーを使用することが必要になる場合があります。 詳細については、「[環境のデバッグ](debuggers-in-the-debugging-tools-for-windows-package.md)」を参照してください。

## <a name="4-determine-how-to-connect-the-target-and-host"></a>4。ターゲットとホストの接続方法を決定する

通常、ターゲットシステムとホストシステムはイーサネットネットワークによって接続されます。 初期の導入作業を行っている場合、またはデバイスにイーサネット接続がない場合は、他のネットワーク接続オプションを使用できます。 詳細については、次の記事を参照してください。
   -   [KDNET network カーネルデバッグを自動的に設定する](setting-up-a-network-debugging-connection-automatically.md)
   -   [カーネルモードデバッグの設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
   -   [KDNET network カーネルデバッグの手動設定](setting-up-a-network-debugging-connection.md)
   -   [仮想マシンのネットワークデバッグの設定-KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)

## <a name="5-choose-either-the-32-bit-or-64-bit-debugging-tools"></a>5。32ビットまたは64ビットのデバッグツールのいずれかを選択します。

どのデバッグツール (32 ビットまたは64ビット) を選択するかは、ターゲットおよびホストシステムで実行されている Windows のバージョンと、32ビットまたは64ビットコードをデバッグしているかどうかによって異なります。 詳細については、「 [32 ビットまたは64ビットのデバッグツールの選択](choosing-a-32-bit-or-64-bit-debugger-package.md)」を参照してください。

## <a name="6-configure-symbols"></a>6。シンボルの構成

WinDbg が提供するすべての高度な機能を使用するには、適切なシンボルを読み込む必要があります。 シンボルが適切に構成されていない場合は、シンボルに依存する機能を使用しようとしたときにシンボルが使用できないことを示すメッセージが表示されます。 詳細については、「 [Windows デバッグのシンボル (WinDbg、KD、CDB、NTSD)](symbols.md)」を参照してください。

## <a name="7-configure-source-code"></a>7.ソースコードの構成

目的が独自のソースコードをデバッグする場合は、ソースコードへのパスを構成する必要があります。 詳細については、「[ソースパス](source-path.md)」を参照してください。

## <a name="8-become-familiar-with-debugger-operation"></a>8.デバッガーの操作に慣れる

このドキュメントの「[デバッガーの操作](debugger-operation-win8.md)」セクションでは、さまざまなタスクのデバッガー操作について説明します。 たとえば、デバッガー拡張[dll](loading-debugger-extension-dlls.md)を読み込む方法について説明します。 WinDbg の操作の詳細については、「 [windbg を使用](debugging-using-windbg.md)したデバッグ」を参照してください。

## <a name="9-become-familiar-with-debugging-techniques"></a>9.デバッグ手法について理解を深める

[標準的なデバッグ手法](standard-debugging-techniques.md)は、ほとんどのデバッグシナリオに適用されます。また、ブレークポイントの設定、呼び出し履歴の検査、メモリリークの検出などがあります。 [特殊なデバッグ手法](specialized-debugging-techniques.md)は、特定のテクノロジまたはコードの種類に適用されます。 例として、プラグアンドプレイデバッグ、KMDF デバッグ、RPC デバッグなどがあります。

## <a name="10-use-the-debugger-reference-commands"></a>10.デバッガーの参照コマンドを使用する

時間の経過と共に、デバッガーでの作業にはさまざまなデバッグコマンドを使用します。 デバッガーで、 [ **. HH** (HTML ヘルプファイルを開く)](-hh--open-html-help-file-.md)コマンドを使用して、デバッグコマンドに関するヘルプ情報を表示します。 使用可能なコマンドの詳細については、「[デバッガーリファレンス](debugger-reference.md)」を参照してください。

## <a name="11-use-debugging-extensions-for-specific-technologies"></a>11.特定のテクノロジに対してデバッグ拡張機能を使用する

ドメイン固有のデータ構造の解析を提供する複数のデバッグ拡張機能があります。 詳細については、「特殊化された[拡張機能](specialized-extensions.md)」を参照してください。

## <a name="12-learn-about-related-windows-internals"></a>12.関連する Windows の内部構造について

このドキュメントでは、Windows の内部構造に関する知識を前提としています。 Windows の内部構造 (メモリ使用量、コンテキスト、スレッド、プロセスなど) の詳細については、「 [*windows の内部構造*](https://docs.microsoft.com/en-us/sysinternals/learn/windows-internals)(Mark Russinovich、David ソロモン、Alex Ionescu など)」を参照してください。

## <a name="13-review-additional-debugging-resources"></a>13.その他のデバッグリソースの確認

その他のリソースには、次の書籍とビデオが含まれます。
-  *Windows のデバッグ中:Tarik Soulami による実践的*なデバッグとトレースの戦略
-   Mario Hewardt と Daniel Pravat による*高度な Windows デバッグ*
-   [デフラグツール](https://channel9.msdn.com/Shows/Defrag-Tools)、約 13 ~ 29、WinDbg について


## <a name="see-also"></a>関連項目

-   [WinDbg の概要 (カーネルモード)](getting-started-with-windbg--kernel-mode-.md)
-   [WinDbg の概要 (ユーザーモード)](getting-started-with-windbg.md)
-   [32ビットまたは64ビットのデバッグツールの選択](choosing-a-32-bit-or-64-bit-debugger-package.md)
-   [デバッグ環境](debuggers-in-the-debugging-tools-for-windows-package.md)
-   [デバッグの設定 (カーネルモードとユーザーモード)](getting-set-up-for-debugging.md)
-   [ユニバーサルドライバーのデバッグ-ステップバイステップラボ (カーネルモードのエコー)](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)
-   [デバッグドライバー-ステップバイステップラボ (Sysvad カーネルモード)](debug-universal-drivers--kernel-mode-.md)
