---
title: 32 ビットまたは 64 ビット デバッグ ツールの選択
description: Windows のツールのデバッグをインストールするときに、ツール一式を 32 ビットと 64 ビット一連のツールの両方を取得します。
ms.assetid: 26aaaf11-1005-4ae7-8f27-4ae0812faa81
keywords:
- 32 ビットのデバッガー パッケージ
- デバッグ ツールの 32 ビット
- 64 ビットのデバッガー パッケージ
- 64 ビット デバッグ ツール
- インストールでは、32 ビットおよび 64 ビット パッケージの選択
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03a46eb6a8bab5fb69584bb7c983c499ea3d4783
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559682"
---
# <a name="choosing-the-32-bit-or-64-bit-debugging-tools"></a>32 ビットまたは 64 ビット デバッグ ツールの選択


Windows のツールのデバッグをインストールするときに、ツール一式を 32 ビットと 64 ビット一連のツールの両方を取得します。 Microsoft Visual Studio を使用する場合[デバッグ環境](debuggers-in-the-debugging-tools-for-windows-package.md)、Visual Studio が自動的に適切なデバッグ ツールを選択するため、設定 32 ビットまたは 64 ビットを使用するかどうかを考慮する必要はありません。

他のデバッグ環境 (WinDbg、KD、CDB、または NTSD) のいずれかを使用する場合は、自分で選択を行う必要があります。 を使用するデバッグ ツールのセットを判断するには、ホスト コンピューターとホスト コンピューターが Windows の 32 ビットまたは 64 ビット バージョンを実行しているかどうかで実行されているプロセッサの型を認識する必要があります。

デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*対象のコンピュータ*します。

### <a name="span-idhostcomputerrunninga32-bitversionofwindowsspanspan-idhostcomputerrunninga32-bitversionofwindowsspanspan-idhostcomputerrunninga32-bitversionofwindowsspanhost-computer-running-a-32-bit-version-of-windows"></a><span id="Host_computer_running_a_32-bit_version_of_Windows"></span><span id="host_computer_running_a_32-bit_version_of_windows"></span><span id="HOST_COMPUTER_RUNNING_A_32-BIT_VERSION_OF_WINDOWS"></span>Windows の 32 ビット バージョンを実行しているホスト コンピューター

ホスト コンピューターで Windows の 32 ビット バージョンが実行されている場合は、32 ビットのデバッグ ツールを使用します。 (このような状況は、x86 ベースおよび x64 ベースの両方のターゲットに適用されます)。

### <a name="span-idx64-basedhostcomputerrunninga64-bitversionofwindowsspanspan-idx64-basedhostcomputerrunninga64-bitversionofwindowsspanspan-idx64-basedhostcomputerrunninga64-bitversionofwindowsspanx64-based-host-computer-running-a-64-bit-version-of-windows"></a><span id="x64-based_host_computer_running_a_64-bit_version_of_Windows"></span><span id="x64-based_host_computer_running_a_64-bit_version_of_windows"></span><span id="X64-BASED_HOST_COMPUTER_RUNNING_A_64-BIT_VERSION_OF_WINDOWS"></span>Windows の 64 ビット バージョンを実行している x64 ベースのホスト コンピューター

ホスト コンピューターが x64 ベース プロセッサを使用して、Windows の 64 ビット バージョンを実行している場合は、次の規則が適用されます。

-   ダンプ ファイルを分析する場合は、デバッグ ツールの 32 ビットまたは 64 ビット デバッグ ツールを使用することができます。 (重要ではありません、ダンプ ファイルがあるかどうかユーザー モード ダンプのファイルまたはカーネル モードのダンプ ファイルでは、また重要ではありません、ダンプ ファイルが x86 ベースまたは x64 ベースのプラットフォームで行われたかどうか。)

-   ライブのカーネル モードのデバッグを実行する場合は、デバッグ ツールの 32 ビットまたは x64 デバッグ ツールのいずれかを使用することができます。 (このような状況は、x86 ベースおよび x64 ベースの両方のターゲットに適用されます)。

-   デバッガーと同じコンピューターで実行されているライブ ユーザー モード コードをデバッグする場合は、64 ビットのコードと WOW64 で実行されている 32 ビット コードをデバッグするため、64 ビット ツールを使用します。 32 ビットまたは 64 ビット モードのデバッガーを設定するには、使用、 [ **.effmach** ](-effmach--effective-machine-.md)コマンド。

-   別のターゲット コンピューターで実行されているライブの 32 ビット ユーザー モード コードをデバッグする場合は、32 ビットのデバッグ ツールを使用します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Windows デバッグ](index.md)

 

 






