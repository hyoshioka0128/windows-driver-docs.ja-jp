---
title: Windows デバッガーを使用したマネージド コードのデバッグ
description: Windows デバッガー (WinDbg、CDB、NTSD) を使用して、マネージコードを含むターゲットアプリケーションをデバッグできます。
ms.assetid: eb4cc883-71ac-4a57-8654-07c3120310c0
keywords: デバッグ、デバッグ、Windbg、マネージコードデバッグ、.NET 共通言語ランタイム、共通言語ランタイム、CLR、JIT コンパイラ、Just-in-time code
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33ea3f64ff4334680559a7fc182391e7f3592639
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534467"
---
# <a name="debugging-managed-code-using-the-windows-debugger"></a>Windows デバッガーを使用したマネージド コードのデバッグ

Windows デバッガー (WinDbg、CDB、NTSD) を使用して、マネージコードを含むターゲットアプリケーションをデバッグできます。 マネージコードをデバッグするには、 [sos デバッガー拡張 (sos)](https://docs.microsoft.com/dotnet/framework/tools/sos-dll-sos-debugging-extension)とデータアクセスコンポーネント (mscordacwks) を読み込む必要があります。

Windows デバッガーは、Visual Studio デバッガーとは別のものです。 Windows デバッガーと Visual Studio デバッガーの違いについては、「 [Windows デバッグ](index.md)」を参照してください。

## <a name="introduction-to-managed-code"></a>マネージコードの概要

マネージコードは、Microsoft .NET 共通言語ランタイム (CLR) と共に実行されます。 マネージコードアプリケーションでは、コンパイラによって生成されるバイナリコードは、プラットフォームに依存しない Microsoft 中間言語 (MSIL) に含まれています。

マネージコードを実行すると、ランタイムによって、プラットフォーム固有のネイティブコードが生成されます。 MSIL からネイティブコードを生成するプロセスは、 *just-in-time (JIT) コンパイル*と呼ばれます。 JIT コンパイラが特定のメソッドの MSIL をコンパイルした後、メソッドのネイティブコードはメモリに残ります。 このメソッドが後で呼び出されるときは常に、ネイティブコードが実行され、JIT コンパイラが必要になることはありません。

さまざまなソフトウェアプロデューサーによって製造された複数のコンパイラを使用して、マネージコードをビルドできます。 特に、Microsoft Visual Studio は、C#、Visual Basic、JScript、C++ などのさまざまな言語のマネージコードをマネージ拡張でビルドできます。

CLR は、.NET Framework が更新されるたびに更新されることはありません。 たとえば、.NET Framework のバージョン2.0、3.0、3.5 では、すべて CLR のバージョン2.0 が使用されます。 次の表は、.NET Framework の各バージョンで使用される CLR のバージョンとファイル名を示しています。

| .NET Framework のバージョン | CLR バージョン | CLR ファイル名 |
|------------------------|-------------|--------------|
| 1.1                    | 1.1         | mscorwks.dll |
| 2.0                    | 2.0         | mscorwks.dll |
| 3.0                    | 2.0         | mscorwks.dll |
| 3.5                    | 2.0         | mscorwks.dll |
| 4.0                    | 4.0         | clr.dll      |
| 4.5                    | 4.0         | clr.dll      |

## <a name="debugging-managed-code"></a>マネージド コードのデバッグ

マネージコードをデバッグするには、デバッガーでこれらの2つのコンポーネントを読み込む必要があります。

- データアクセスコンポーネント (DAC) (mscordacwks)
- [SOS デバッガー拡張 (sos)](https://docs.microsoft.com/dotnet/framework/tools/sos-dll-sos-debugging-extension)

**メモ**   .NET Framework のすべてのバージョンでは、DAC のファイル名は mscordacwks であり、SOS デバッグ拡張機能のファイル名は sos です。

### <a name="getting-the-sos-debugging-extension-sosdll"></a>SOS デバッガー拡張 (sos) を取得する

Windows 用デバッグツールの現在のバージョンには、SOS デバッガー拡張 (sos .dll) ファイルは含まれていません。

.NET Framework バージョン2.0 以降では、.NET Framework のインストールに sos が含まれています。

バージョン1の場合。.NET Framework の*x*は、.NET Framework のインストールには含まれていません。 .NET Framework 1 の sos を取得します。*x*では、windows 7 の Windows 7 デバッグツールの32ビット版をダウンロードします。

Windows 用の windows 7 デバッグツールは、windows 7 の Windows SDK に含まれています。これは、次の2つの場所で利用できます。

- [Windows 7 および .NET Framework 4.0 の Windows SDK](https://www.microsoft.com/download/details.aspx?id=8279)
- [Windows 7 および .NET Framework 4.0 (ISO) の Windows SDK](https://www.microsoft.com/download/details.aspx?id=8442)

X64 バージョンの Windows を実行している場合は、32ビットバージョンの SDK を使用するように指定できるように、 [ISO](https://www.microsoft.com/download/details.aspx?id=8442)を使用します。 Sos は、windows 7 の Windows 7 デバッグツールの32ビット版にのみ含まれています。

### <a name="loading-mscordacwksdll-and-sosdll-live-debugging"></a>Mscordacwks と sos を読み込んでいます (ライブデバッグ)

デバッガーとデバッグ中のアプリケーションが同じコンピューター上で実行されているとします。 その後、アプリケーションによって使用されている .NET Framework がコンピューターにインストールされ、デバッガーで使用できるようになります。

デバッガーは、マネージコードアプリケーションが使用している CLR のバージョンと同じバージョンの DAC を読み込む必要があります。 ビット (32 ビットまたは64ビット) も一致する必要があります。 DAC (mscordacwks) には .NET Framework が付属しています。 正しいバージョンの DAC を読み込むには、デバッガーをマネージコードアプリケーションにアタッチし、このコマンドを入力します。

**. cordll-ve-u-l**

出力は次のようになります。

```dbgcmd
CLRDLL: Loaded DLL C:\Windows\Microsoft.NET\Framework64\v4.0.30319\mscordacwks.dll
CLR DLL status: Loaded DLL C:\Windows\Microsoft.NET\Framework64\v4.0.30319\mscordacwks.dll
```

Mscordacwks のバージョンが、アプリケーションが使用している CLR のバージョンと一致することを確認するには、次のコマンドのいずれかを入力して、読み込まれた CLR モジュールに関する情報を表示します。

**lmv mclr** (CLR のバージョン 4.0)

**lmv mscorwks.dll** (CLR のバージョン1.0 または 2.0)

出力は次のようになります。

```dbgcmd
start             end                 module name
000007ff`26710000 000007ff`2706e000   clr        (deferred)             
    Image path: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\clr.dll
...
```

前の例では、CLR (clr .dll) のバージョンが DAC のバージョン (mscordacwks) と一致することに注意してください: v v4.0.30319。 また、両方のコンポーネントが64ビットであることにも注意してください。

[**Cordll**](-cordll--control-clr-debugging-.md)を使用して DAC を読み込むと、sos デバッガー拡張 (sos) が自動的に読み込まれる場合があります。 Sos が自動的に読み込まれない場合は、これらのコマンドのいずれかを使用して、それを読み込むことができます。

**. loadby sos clr** (clr のバージョン 4.0)

**. loadby sos mscorwks.dll** (CLR のバージョン1.0 または 2.0)

[**Loadby**](-load---loadby--load-extension-dll-.md)を使用する代わりに、 **load**を使用することもできます。 たとえば、64ビット CLR のバージョン4.0 を読み込むには、次のようなコマンドを入力します。

**. load C: \\ Windows \\ Microsoft.NET \\ Framework64 \\ v v4.0.30319 \\ sos .dll**

上記の出力では、SOS デバッガー拡張 (sos) のバージョンが CLR のバージョンと DAC: v v4.0.30319 と一致していることがわかります。 また、3つのコンポーネントすべてが64ビットであることにも注目してください。

### <a name="loading-mscordacwksdll-and-sosdll-dump-file"></a>Mscordacwks と sos を読み込んでいます (ダンプファイル)

デバッガーを使用して、別のコンピューターで作成されたダンプファイル (マネージコードアプリケーション) を開くとします。

デバッガーは、マネージコードアプリケーションが他のコンピューターで使用していた CLR のバージョンと同じバージョンの DAC を読み込む必要があります。 ビット (32 ビットまたは64ビット) も一致する必要があります。

DAC (mscordacwks) には .NET Framework が付属していますが、デバッガーを実行しているコンピューターに適切なバージョンの .NET Framework がインストールされていないことを前提としています。 3つのオプションがあります。

- シンボルサーバーから DAC を読み込みます。 たとえば、シンボルパスに Microsoft のパブリックシンボルサーバーを含めることができます。
- デバッガーを実行しているコンピューターに正しいバージョンの .NET Framework をインストールします。
- ダンプファイルを作成したユーザー (別のコンピューター上) から正しいバージョンの mscordacwks を取得し、デバッガーを実行しているコンピューターに手動でコピーします。

ここでは、Microsoft のパブリックシンボルサーバーを使用する方法について説明します。

次のコマンドを入力します。

**. sympath + srv \\ *** (シンボルサーバーをシンボルパスに追加します。)

**! 記号のノイズ**

**. cordll-ve-u-l**

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

前の出力では、デバッガーが、C: \\ Windows \\ Microsoft.NET とシンボルキャッシュ (c: \\ programdata \\ dbg \\ sym) で、ローカルコンピューター上の mscordacwks と sos を最初に検索したことがわかります。 デバッガーがローカルコンピューター上の正しいバージョンのファイルを見つけられなかった場合、そのファイルをパブリックシンボルサーバーから取得します。

Mscordacwks のバージョンが、アプリケーションで使用していた CLR のバージョンと一致することを確認するには、次のコマンドのいずれかを入力して、読み込まれた CLR モジュールに関する情報を表示します。

**lmv-mclr** (CLR のバージョン 4.0)

**lmv** (CLR のバージョン1.0 または 2.0)

出力は次のようになります。

```dbgcmd
start             end                 module name
000007ff`26710000 000007ff`2706e000   clr        (deferred)             
    Image path: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\clr.dll
...
```

前の例では、CLR (clr .dll) のバージョンが DAC の製品バージョン (mscordacwks) と一致することに注意してください: v v4.0.30319。 また、両方のコンポーネントが64ビットであることにも注意してください。

### <a name="using-the-sos-debugging-extension"></a>SOS デバッガー拡張機能の使用

SOS デバッガー拡張が正しく読み込まれたことを確認するには、 [**. chain**](-chain--list-debugger-extensions-.md)コマンドを入力します。

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

SOS デバッガー拡張をテストするには、「 **! SOS. help**」と入力します。 次に、SOS デバッガー拡張機能によって提供されるコマンドのいずれかを試します。 たとえば、! sos を試すことができ**ます。DumpDomain**または **! sos。Threads**コマンド。

### <a name="notes"></a>Notes

マネージコードアプリケーションによって、複数のバージョンの CLR が読み込まれることがあります。 その場合は、読み込む DAC のバージョンを指定する必要があります。 詳細については、「 [**cordll**](-cordll--control-clr-debugging-.md)」を参照してください。
