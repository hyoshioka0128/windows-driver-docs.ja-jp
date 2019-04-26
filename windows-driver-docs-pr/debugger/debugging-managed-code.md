---
title: Windows デバッガーを使用したマネージド コードのデバッグ
description: Windows デバッガー (WinDbg、CDB、NTSD) をマネージ コードを含む対象アプリケーションをデバッグするを使用することができます。
ms.assetid: eb4cc883-71ac-4a57-8654-07c3120310c0
keywords: デバッグ、デバッグ、Windbg、マネージ コードのデバッグ、.NET 共通言語ランタイム、共通言語ランタイム、CLR、JIT コンパイラ、JITted コード
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8edea69504ef1085bb2df54934350426a28e1a01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350608"
---
# <a name="debugging-managed-code-using-the-windows-debugger"></a>Windows デバッガーを使用したマネージド コードのデバッグ


Windows デバッガー (WinDbg、CDB、NTSD) をマネージ コードを含む対象アプリケーションをデバッグするを使用することができます。 マネージ コードのデバッグに読み込む必要がある、 [SOS デバッガー拡張 (sos.dll)](https://go.microsoft.com/fwlink/p/?linkid=223345)およびデータ アクセス コンポーネント (mscordacwks.dll)。

Windows デバッガーは、Visual Studio デバッガーとは別です。 Windows デバッガーと Visual Studio デバッガーの違いについては、次を参照してください。 [Windows デバッグ](index.md)します。

## <a name="span-idintroduction-to-managed-codespanspan-idintroductiontomanagedcodespanintroduction-to-managed-code"></a><span id="introduction-to-managed-code"></span><span id="INTRODUCTION_TO_MANAGED_CODE"></span>マネージ コードの概要


Microsoft .NET 共通言語ランタイム (CLR) とマネージ コードが実行されます。 マネージ コード アプリケーションでは、コンパイラが生成するバイナリ コードはで Microsoft Intermediate Language (MSIL)、プラットフォームに依存しません。

マネージ コードを実行すると、ランタイムは、プラットフォーム固有のネイティブ コードを生成します。 MSIL からネイティブ コードを生成するプロセスと呼ばれます *- イン タイム (JIT) コンパイル*します。 特定のメソッドの MSIL には、JIT コンパイラがコンパイル後、メソッドのネイティブ コードは、メモリに残ります。 たびに、このメソッドは、後で呼び出されると、ネイティブ コードが実行され、JIT コンパイラが関与する必要はありません。

さまざまなソフトウェアの製作者によって製造するいくつかのコンパイラを使用して、マネージ コードをビルドすることができます。 具体的には、Microsoft Visual Studio がなど複数のさまざまな言語からマネージ コードをビルドできますC#、Visual Basic、JScript、および C++ マネージ拡張とします。

.NET Framework が更新されるたびに、CLR は更新されません。 たとえば、バージョン 2.0、3.0、および .NET Framework CLR のすべての使用バージョン 2.0 の 3.5。 次の表は、バージョンと .NET Framework の各バージョンによって使用されている CLR のファイル名を示します。

| .NET framework のバージョン | CLR のバージョン | CLR のファイル名 |
|------------------------|-------------|--------------|
| 1.1                    | 1.1         | mscorwks.dll |
| 2.0                    | 2.0         | mscorwks.dll |
| 3.0                    | 2.0         | mscorwks.dll |
| 3.5                    | 2.0         | mscorwks.dll |
| 4.0                    | 4.0         | clr.dll      |
| 4.5                    | 4.0         | clr.dll      |

 

## <a name="span-iddebugging-managedcodespanspan-iddebuggingmanagedcodespandebugging-managed-code"></a><span id="debugging-managed_code"></span><span id="DEBUGGING_MANAGED_CODE"></span>マネージ コードのデバッグ


マネージ コードをデバッグするには、デバッガーはこれら 2 つのコンポーネントを読み込む必要があります。

-   データ アクセス コンポーネント (DAC) (mscordacwks.dll)
-   [SOS デバッガー拡張 (sos.dll)](https://go.microsoft.com/fwlink/p/?linkid=223345)

**注**  すべてのバージョンの .NET Framework では、DAC のファイル名は、mscordacwks.dll、SOS デバッグ拡張機能のファイル名は sos.dll を読み込みます。

 

### <a name="span-idgetting-the-sos-debugging-extensionspanspan-idgettingthesosdebuggingextensionspangetting-the-sos-debugging-extension-sosdll"></a><span id="getting-the-sos-debugging-extension"></span><span id="GETTING_THE_SOS_DEBUGGING_EXTENSION"></span>SOS デバッガー拡張 (sos.dll) を取得します。

SOS デバッガー拡張 (sos.dll) ファイルは、現在のバージョンの Windows のツールをデバッグには含まれません。

.NET Framework バージョン 2.0 以降では、sos.dll が .NET Framework のインストールに含まれています。

バージョン 1。*x* .NET Framework の sos.dll 記載されていない .NET Framework のインストール。 .NET Framework 1 sos.dll を取得します。*x*Windows 7 のデバッグ ツールの Windows の 32 ビット バージョンをダウンロードします。

Windows 7 のデバッグ ツールの Windows はこれら 2 つの場所で提供される、Windows SDK for Windows 7 に含まれます。

-   [Windows SDK for Windows 7 および .NET Framework 4.0](https://go.microsoft.com/fwlink/p?LinkId=320327)
-   [Windows SDK for Windows 7 および .NET Framework 4.0 (ISO)](https://go.microsoft.com/fwlink/p?LinkId=320328)

X64 を実行している場合のバージョンの Windows を使用して、 [ISO](https://go.microsoft.com/fwlink/p?LinkID=320328)サイト、SDK の 32 ビット バージョンが必要なことを指定できるようにします。 Sos.dll は、Windows 7 のデバッグ ツールの Windows の 32 ビット バージョンにのみ含まれます。

### <a name="span-idloadingmscordacwksdllandsosdlllivedebuggingspanspan-idloadingmscordacwksdllandsosdlllivedebuggingspanspan-idloadingmscordacwksdllandsosdlllivedebuggingspanloading-mscordacwksdll-and-sosdll-live-debugging"></a><span id="Loading_mscordacwks.dll_and_sos.dll__live_debugging_"></span><span id="loading_mscordacwks.dll_and_sos.dll__live_debugging_"></span><span id="LOADING_MSCORDACWKS.DLL_AND_SOS.DLL__LIVE_DEBUGGING_"></span>読み込み mscordacwks.dll と sos.dll (ライブ デバッグ)

デバッガーとデバッグ中のアプリケーションが同じコンピューターで実行されていることを想定しています。 アプリケーションで使用されている .NET Framework がコンピューターにインストールされているし、デバッガーを使用します。

デバッガーでは、マネージ コード アプリケーションを使用している CLR のバージョンと同じである、DAC のバージョンを読み込む必要があります。 ビット (32 ビットまたは 64 ビット) にも一致する必要があります。 DAC (mscordacwks.dll) .NET Framework が付属します。 正しいバージョンの DAC を読み込むには、マネージ コード アプリケーションにデバッガーをアタッチし、このコマンドを入力します。

**.cordll -ve -u -l**

出力は次のようになります。

```dbgcmd
CLRDLL: Loaded DLL C:\Windows\Microsoft.NET\Framework64\v4.0.30319\mscordacwks.dll
CLR DLL status: Loaded DLL C:\Windows\Microsoft.NET\Framework64\v4.0.30319\mscordacwks.dll
```

Mscordacwks.dll のバージョンが、アプリケーションを使用している CLR のバージョンと一致することを確認するには、読み込まれた CLR モジュールに関する情報を表示するには、次のコマンドのいずれかを入力します。

**lmv mclr** (用、CLR のバージョン 4.0)

**lmv mscorwks** (バージョン 1.0 または 2.0 CLR の) の

出力は次のようになります。

```dbgcmd
start             end                 module name
000007ff`26710000 000007ff`2706e000   clr        (deferred)             
    Image path: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\clr.dll
...
```

前の例では、CLR (clr.dll) のバージョンが DAC (mscordacwks.dll) のバージョンと一致することに注意してください: v4.0.30319 します。 両方のコンポーネントが 64 ビットにも注目してください。

使用すると[ **.cordll** ](-cordll--control-clr-debugging-.md) DAC を読み込むには、SOS デバッガー拡張 (sos.dll) を自動的に読み込まれます場合があります。 Sos.dll を自動的に読み込まれますが場合、は、読み込むことをこれらのコマンドのいずれかを使用できます。

**.loadby sos clr** (用、CLR のバージョン 4.0)

**.loadby sos mscorwks** (バージョン 1.0 または 2.0 CLR の) の

使用する代替手段として[ **.loadby**](-load---loadby--load-extension-dll-.md)、使用することができます **.load**します。 たとえば、64 ビット CLR のバージョン 4.0 を読み込むには、次のようなコマンドを入力します。

**.load c:\\Windows\\Microsoft.NET\\Framework64\\v4.0.30319\\sos.dll**

上記の出力で SOS デバッガー拡張 (sos.dll) のバージョンが、CLR および DAC のバージョンと一致することに注意してください: v4.0.30319 します。 次の 3 つのすべてのコンポーネントが 64 ビットにも注目してください。

### <a name="span-idloadingmscordacwksdllandsosdlldumpfilespanspan-idloadingmscordacwksdllandsosdlldumpfilespanspan-idloadingmscordacwksdllandsosdlldumpfilespanloading-mscordacwksdll-and-sosdll-dump-file"></a><span id="Loading_mscordacwks.dll_and_sos.dll__dump_file_"></span><span id="loading_mscordacwks.dll_and_sos.dll__dump_file_"></span><span id="LOADING_MSCORDACWKS.DLL_AND_SOS.DLL__DUMP_FILE_"></span>Mscordacwks.dll と sos.dll (ダンプ ファイル) の読み込み

デバッガーを使用する (マネージ コード アプリケーション) の別のコンピューターで作成されたダンプ ファイルを開くとします。

デバッガーでは、マネージ コード アプリケーションが他のコンピューターを使用して CLR のバージョンと同じである、DAC のバージョンを読み込む必要があります。 ビット (32 ビットまたは 64 ビット) にも一致する必要があります。

DAC (mscordacwks.dll) が付属して、.NET Framework が、デバッガーを実行しているコンピューターにインストールされている .NET Framework の正しいバージョンがないことを仮定します。 3 つのオプションがあります。

-   シンボル サーバーから DAC を読み込みます。 たとえば、シンボル パスでマイクロソフトのパブリック シンボル サーバーを含めることができます。
-   デバッガーを実行しているコンピューターに .NET Framework の正しいバージョンをインストールします。
-   (別のコンピューター) にダンプ ファイルを作成したユーザーから mscordacwks.dll の正しいバージョンを取得し、手動でデバッガーを実行しているコンピューターにコピーします。

ここで Microsoft のパブリック シンボル サーバーを使用してについて説明します。

これらのコマンドを入力します。

**.sympath + srv\\*** (シンボル サーバーの追加シンボル パスにします)。

**! ノイズの多い sym**

**.cordll -ve -u -l**

出力は次のようになります。

```dbgcmd
CLRDLL: Unable to get version info for 'C:\Windows\Microsoft.NET
   \Framework64\v4.0.30319\mscordacwks.dll', Win32 error 0n87

SYMSRV:  C:\ProgramData\dbg\sym\mscordacwks_AMD64_AMD64_4.0.30319.18010.dll
   \5038768C95e000\mscordacwks_AMD64_AMD64_4.0.30319.18010.dll not found

SYMSRV:  mscordacwks_AMD64_AMD64_4.0.30319.18010.dll from 
   https://msdl.microsoft.com/download/symbols: 570542 bytes - copied         
...
SYMSRV:  C:\ProgramData\dbg\sym\SOS_AMD64_AMD64_4.0.30319.18010.dll
   \5038768C95e000\SOS_AMD64_AMD64_4.0.30319.18010.dll not found

SYMSRV:  SOS_AMD64_AMD64_4.0.30319.18010.dll from 
   https://msdl.microsoft.com/download/symbols: 297048 bytes - copied         
...
Automatically loaded SOS Extension
...
```

上記の出力で、デバッガーが mscordacwks.dll と c: ローカル コンピューター上の sos.dll を最初に検索を確認できます\\Windows\\Microsoft.NET およびシンボルのキャッシュ (c:\\ProgramData\\dbg\\sym)。 デバッガー、ローカル コンピューター上のファイルの正しいバージョンが見つかりませんでした、ときに、それらから取得、パブリック シンボル サーバー。

Mscordacwks.dll のバージョンが、アプリケーションが使用している CLR のバージョンと一致することを確認するには、読み込まれた CLR モジュールに関する情報を表示するには、次のコマンドのいずれかを入力します。

**lmv mclr** (用、CLR のバージョン 4.0)

**lmv mscorwks** (バージョン 1.0 または 2.0 CLR の) の

出力は次のようになります。

```dbgcmd
start             end                 module name
000007ff`26710000 000007ff`2706e000   clr        (deferred)             
    Image path: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\clr.dll
...
```

前の例では、CLR (clr.dll) のバージョンが DAC (mscordacwks.dll) のバージョンと一致することに注意してください: v4.0.30319 します。 両方のコンポーネントが 64 ビットにも注目してください。

### <a name="span-idusingthesosdebuggingextensionspanspan-idusingthesosdebuggingextensionspanspan-idusingthesosdebuggingextensionspanusing-the-sos-debugging-extension"></a><span id="Using_the_SOS_Debugging_Extension_"></span><span id="using_the_sos_debugging_extension_"></span><span id="USING_THE_SOS_DEBUGGING_EXTENSION_"></span>SOS デバッガー拡張を使用します。

SOS デバッガー拡張が正しく読み込まれたことを確認するには、入力、 [ **.chain** ](-chain--list-debugger-extensions-.md)コマンド。

```dbgcmd
0:000> .chain
Extension DLL search Path:
...
Extension DLL chain:
    C:\ProgramData\dbg\sym\SOS_AMD64_AMD64_4.0.30319.18010.dll\...
        ...
    dbghelp: image 6.13.0014.1665, API 6.2.6, built Wed Dec 12 03:02:43 2012
...
```

SOS デバッガー拡張をテストするには、入力 **! sos.help**します。 SOS デバッグ拡張機能によって提供されるコマンドのいずれかを再試行してください。 たとえば、試して **! sos します。DumpDomain**または **! sos します。スレッド**コマンド。

### <a name="span-idnotesspanspan-idnotesspanspan-idnotesspannotes"></a><span id="Notes"></span><span id="notes"></span><span id="NOTES"></span>ノート

場合があります、マネージ コード アプリケーションでは、CLR の 1 つ以上のバージョンを読み込みます。 その場合は、読み込みに DAC のバージョンを指定する必要があります。 詳細については、次を参照してください。 [ **.cordll**](-cordll--control-clr-debugging-.md)します。

 

 





