---
title: チェックされているオペレーティング システムと HAL (Windows XP および Windows Server 2003 を) インストールします。
description: チェック済みのオペレーティング システムと HAL のみのインストール (Windows XP と Windows Server 2003)
ms.assetid: 51175951-9267-4d92-8b47-4dd2155f4e56
keywords:
- チェック ビルド、WDK をインストールします。
- WDK ビルド
- リテール ビルド WDK
- HAL WDK
- 部分的なチェック ビルド WDK
- WDK の名前は、ビルドを確認します。
- チェックされたファイルのコピー
- Boot.ini ファイル チェック WDK ビルドします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e5dd6eaaccd860590e7801278a757461f7b0de0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572421"
---
# <a name="installing-just-the-checked-operating-system-and-hal-for-windows-xp-and-windows-server-2003"></a>チェック済みのオペレーティング システムと HAL のみのインストール (Windows XP と Windows Server 2003)


## <span id="ddk_installing_just_the_checked_operating_system_and_hal_tools"></span><span id="DDK_INSTALLING_JUST_THE_CHECKED_OPERATING_SYSTEM_AND_HAL_TOOLS"></span>


完了チェック ビルドは、コンピューターにインストールではなく、システムの無料のビルドをインストールし、オペレーティング システム イメージと HAL の検証済みのバージョンをインストールできます。 この手順を使用する場合は、2 つのブート オプションを提供するためにブート ローダーを構成できます。 無料のビルドでは、最初のブート オプションで十分です。 2 番目のブート オプションは、チェックされているオペレーティング システム イメージと HAL を使用してシステムを起動が、その他のすべてのシステム コンポーネントの無料版を使用します。

インストール完了のチェック ビルドと比較して、このアプローチには次の利点があります。

-   ドライバーは、オペレーティング システムと HAL デバッグ チェックの利点を取得します。 同時に、オペレーティング システムと HAL 以外のシステム コンポーネントの無料版を使用しているために、システム全体のパフォーマンスに影響が最小限に抑えます。

-   1 つのインストール (とそのため 1 つのシステム ディレクトリ、実行可能ファイルのコンポーネントの 1 つのセットおよびレジストリ パラメーターの 1 つのセット) 使用できるチェックまたはオペレーティング システム イメージと HAL の無料版のいずれかブート時に決定されます。

オペレーティング システム イメージと HAL の検証済みのバージョンをインストールする必要があります、適切なからファイルをコピーがチェックされている配布メディア、%systemroot% を\\system32 ディレクトリの新しい一意のファイル名を使用しています。 システムの起動時にこれらのファイルを使用するオプションを提供するシステムに指示する必要があります。 おく必要がありますに注意してください、次の重要なガイドライン、それ以外の場合の無料のインストールにチェックされているオペレーティング システムと HAL イメージをインストールする場合。

-   オペレーティング システム イメージと HAL 保持する必要が同期常にします。 したがって、オペレーティング システム イメージのチェック済みバージョンを使用する場合、HAL の (その逆) は、チェック済みバージョンも使用する必要があります。 システムのオペレーティング システム イメージと調和 HAL の保持に失敗したシステムは起動できないことができます。

-   無料のビルドのインストール中にインストールされているオペレーティング システム イメージと HAL の無料バージョンを上書きしません。 無料のバージョンを上書き、オペレーティング システム イメージと HAL のシステム、起動できないようにすることができ、エラーから回復するが困難。 そのため、常に注意する %systemroot% にオペレーティング システムと HAL の検証済みのバージョンをコピーするときに、一意の新しいファイル名を使用する\\system32 ディレクトリ。

-   オンの配布を使用するが、無料のシステムのと同じサービス パック番号であることを確認します。 たとえば、無料のビルドのどの Service Pack 2 のシステムがインストールされているシステムで、チェックされているオペレーティング システム イメージと HAL をインストールする場合ことを確認チェックに使用する配布は Service Pack 2 でも。

部分的なチェック ビルドをインストールする手順は次のとおりです。

### <a name="span-idstep1identifyingthefilestoinstallspanspan-idstep1identifyingthefilestoinstallspanstep-1-identifying-the-files-to-install"></a><span id="step_1__identifying_the_files_to_install"></span><span id="STEP_1__IDENTIFYING_THE_FILES_TO_INSTALL"></span>手順 1:インストールするファイルを識別します。

部分的なチェック ビルドをインストールする最初の手順では、オペレーティング システム イメージと HAL ファイル システムに無料のビルドをインストールするために使用されたのバージョンを決定します。

HAL イメージ、オペレーティング システムのいくつかの異なるバージョンは、オペレーティング システムの NT ベースの配布中に提供されます。 プロセッサや他のシステム ハードウェアのさまざまな組み合わせをサポートするためにこれらの異なるバージョンが存在します。 インストール手順はどのオペレーティング システム イメージと HAL のイメージを使用して、該当するファイルのコピーをシステムの %systemroot% に配布メディアから自動的に識別する、オペレーティング システム ソフトウェアがインストールされているときに\\system32 ディレクトリ。

インストールされているオペレーティング システム イメージ ファイルは、1 つまたは複数のプロセッサがサポートされるかどうかと物理アドレス拡張 (PAE) をサポートするかどうかによって異なります (4 GB を超える物理メモリのシステムでアクティブなは、PAE です)。 配布メディア上のファイル名は次のとおりです。

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
4 GB の物理メモリをユニプロセッサ x86 アーキテクチャ システム。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa.exe  
PAE サポート ユニプロセッサ x86 アーキテクチャ システム。

<span id="NTKRNLMP.EXE"></span>ntkrnlmp.exe  
4 GB の物理メモリをマルチプロセッサの x86 アーキテクチャ システム。

<span id="NTKRPAMP.EXE"></span>ntkrpamp.exe  
PAE のサポートしているマルチプロセッサの x86 アーキテクチャ システム。

同様に、これには、HAL のいくつかの異なる名前があります。

システムのインストール中には、インストール手順は、適切なオペレーティング システム イメージと HAL をシステムにインストールを決定します。 選択したファイルは %systemroot% にコピーされます\\固定で、既知の名前を使用して、インストール中に、system32 ディレクトリ。 これらの固定名の使用すると、ブート時にこれらのファイルを検索してローダーを簡単になります。 これらのファイルの固定名は次のとおりです。

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
X86 オペレーティング システム イメージと物理メモリの以下の 4 GB のシステムです。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa.exe  
X86 オペレーティング システム イメージの物理メモリと 4 GB 以上のシステムです。

<span id="HAL.DLL"></span>hal.dll  
読み込み可能な HAL イメージです。

場合によっては、システムのハードウェア構成によって 1 つ以上のファイルの名前を変更できますを適切な固定名に注意してください。 それ以外の場合は、配布メディア上のファイル名は、固定の必要なファイル名と同じです。

チェックされているオペレーティング システム イメージと HAL をインストールするには、まずシステムのインストール中に、システムにコピーされたイメージの元の名前を確認する必要があります。 これを実行するには、ファイルの %systemroot% を調べる\\修復\\setup.log します。 これを使用して表示するには、その属性を変更する必要があるため、隠しファイルは、 **dir**コマンド。

Setup.log ファイルは %systemroot% に配布メディアからコピーされたファイルを一覧表示\\システムのインストール プロセス中に、system32 ディレクトリ。

Setup.log ファイルの例は次のとおりです。

```
[Paths]
TargetDirectory = "\WINNT"
TargetDevice = "\Device\Harddisk0\Partition1"
SystemPartitionDirectory = "\"
SystemPartition = "\Device\Harddisk0\Partition1"
[Signature]
Version = "WinNt5.1"
[Files.SystemPartition]
NTDETECT.COM = "NTDETECT.COM","f41f"
ntldr = "ntldr","3e8b5"
arcsetup.exe = "arcsetup.exe","379db"
arcldr.exe = "arcldr.exe","2eca9"
[Files.WinNt]
\WINNT\system32\drivers\kbdclass.sys = "kbdclass.sys","e259"
\WINNT\system32\drivers\mouclass.sys = "mouclass.sys","7e78"
\WINNT\system32\drivers\uhcd.sys = "uhcd.sys","10217"
\WINNT\system32\drivers\usbd.sys = "usbd.sys","5465"
(...several similar lines omitted...)
\WINNT\system32\framebuf.dll = "framebuf.dll","10c84"
\WINNT\system32\hal.dll = "halmacpi.dll","2bedf"
\WINNT\system32\ntkrnlpa.exe = "ntkrpamp.exe","1d66a6"
\WINNT\system32\ntoskrnl.exe = "ntkrnlmp.exe","1ce5c5"
\WINNT\inf\mdmrpci.inf = "mdmrpci.inf","96a3"
```

サンプルの setup.log ファイルで 2 つのオペレーティング システム イメージ ファイルがコピーされたことを確認できます、 \\winnt\\system32 ディレクトリ (は %systemroot%\\system32) のインストール時にします。 ファイル ntkrpamp.exe は ntkrnlpa.exe に配布メディアからコピーされ、ファイル ntkrnlmp.exe は ntoskrnl.exe に配布メディアからコピーされます。 このサンプルからも確認できる HAL ファイル (で、%systemroot% 内の固定名 hal.dll\\system32 ディレクトリ) 一覧が元の名前します。

**警告**   HAL の一部のファイルがある一見同様の名前。 たとえば、一般的に使用される 2 つの Hal halacpi.dll と halapic.dll です。 お使いのシステムの HAL の正しいバージョンを使用するように注意します。 間違った HAL を選択すると、システムが起動できないが発生します。

 

### <a name="span-idstep2copyingthecheckedfilesspanspan-idstep2copyingthecheckedfilesspanstep-2-copying-the-checked-files"></a><span id="step_2__copying_the_checked_files"></span><span id="STEP_2__COPYING_THE_CHECKED_FILES"></span>手順 2:チェックされたファイルのコピー

システムのインストール中に使用されていたファイルの名前がわかったら、システムにこれらのファイルの検証済みのバージョンをコピーできます。 チェックされている配布 kit で特定したファイルを検索します。 %Systemroot% にこれらのファイルをコピー\\、一意の新しいファイル名を与えて、システムの system32 ディレクトリ。 これらのファイルのコピーは、8.3 名前付け規則に従う必要があります。 一意、8.3 形式に準拠したファイル名を確認する方法は .chk にその元のファイル タイプ (.dll または .exe) からファイルの種類の名前を変更するがコピーされるとき。 そのため、例を使用して、手順 1 で、ファイルをコピーするチェックされている配布キットから、次のように。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">チェックされている分布の元のファイル名の場合。</th>
<th align="left">SystemRoot%\system32 で次のファイル名をコピーしてください。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ntkrnlmp.exe</p></td>
<td align="left"><p>ntkrnlmp.chk</p></td>
</tr>
<tr class="even">
<td align="left"><p>ntkrpamp.exe</p></td>
<td align="left"><p>ntkrpamp.chk</p></td>
</tr>
<tr class="odd">
<td align="left"><p>halmapic.dll</p></td>
<td align="left"><p>halmapic.chk</p></td>
</tr>
</tbody>
</table>

 

チェックされているディストリビューションの一部のファイルは、圧縮形式で提供されます。 これらのファイルは、そのファイルの種類の最後の文字として、アンダー スコア文字で示されます。 たとえば、チェック ビルド配布キットのファイル halapic.dll を検索する場合は、ファイル halapic.dl を検索、\_、これは、正しいファイルを圧縮形式でします。

チェックされた分布から圧縮されたファイルを圧縮解除するには、展開ユーティリティを使用して (%systemroot%\\system32\\expand.exe)。 たとえば、halapic.dl を展開する\_halapic.chk として拡張されたファイルの名前しは、コマンド プロンプト ウィンドウから次のコマンドを使用することができます。

```
> expand halapic.dl_ halapic.chk
```

### <a name="span-idstep3editingbootinispanspan-idstep3editingbootinispanstep-3-editing-bootini"></a><span id="step_3__editing_boot_ini"></span><span id="STEP_3__EDITING_BOOT_INI"></span>手順 3:Boot.ini の編集

%Systemroot% にチェックされたファイルをコピーしたら\\system32 ディレクトリの場合は、これらのチェックされたファイルの使用を開始する、システム起動時のオプションを作成する必要があります。 これを実行するには、boot.ini ファイルを編集します。

一般的な手順については、[boot.ini ファイルを編集](editing-the-boot-ini-file.md)を参照してください。

この特定のケースでは、オペレーティング システム イメージとインストールされている HAL のチェックを行うバージョンでシステムを起動できるようにする新しい起動時のオプションを作成する必要があります。

行を探し、 **\[オペレーティング システム\]** Windows インストールを指す boot.ini のセクション。 2 つ目のコピーを作成し、コピーした行の末尾に、次のパラメーターを追加します。

```
/kernel=KernelFile /hal=HalFile 
```

場所*KernelFile*チェックされている配布 kit では、以前にコピーしたオペレーティング システム イメージ ファイルのチェック済みバージョンの名前を指定し、 *HalFile*のチェック済みバージョンの名前を指定します、チェックされている配布キットからコピーしておいた HAL します。

オペレーティング システムを記述する行が含まれている場合、 **/PAE**パラメーター、PAE サポートにより、オペレーティング システム イメージのチェック済みバージョンを使用することを確認します。 オペレーティング システムを記述する行がないかどうか、 **/PAE**パラメーター、PAE サポートなしチェック済みバージョンのオペレーティング システムのイメージを使用します。

のどの行では、無料のビルドと、どの行が部分的なチェック ビルドを識別できるように、新しい行に、引用符で囲まれたテキストを変更することも必要があります。

このような boot.ini ファイルの例は次のとおりです。

```
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(1)\WINNT
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINNT="Microsoft Windows 2000 Professional" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINNT="Windows 2000 Checked" /fastdetect /kernel=ntoskrnl.chk /hal=halacpi.chk
```

カーネル デバッガーを使用してチェックのビルドを使用する場合は、適切なデバッグ関連のパラメーターも追加する必要があります。 (、 **/Kernel**と **/hal**パラメーター デバッグが自動的に有効にしないでください)。詳細については、[boot.ini ファイルを編集](editing-the-boot-ini-file.md)を参照してください。

変更を行った後は、変更を保存し、エディターを終了します。 次に、このシステムを起動する新しいオペレーティング システムのブート オプションが表示されますがチェックされているオペレーティング システム イメージと HAL を選択することができます。

### <a name="span-idinstallingadditionalcheckedfilesspanspan-idinstallingadditionalcheckedfilesspaninstalling-additional-checked-files"></a><span id="installing_additional_checked_files"></span><span id="INSTALLING_ADDITIONAL_CHECKED_FILES"></span>追加のチェックされたファイルをインストールします。

チェックされているオペレーティング システムと HAL をインストールしたら、チェックされている追加のコンポーネントをインストールするオプションがあります。 いくつかの主要コンポーネントのインストール、無料のバージョンをチェックされている配布メディアから対応するチェックと置き換えることができます。 これは、役に立ちます、たとえば、他のデバイスのスタック内に存在するドライバーを記述するとき。 上と下、スタック内のドライバーをドライバーの無料バージョンに置き換えることでは、追加のエラーがこれらのコンポーネントのチェックを有効になります。 迅速かつ簡単には、ドライバーの問題を特定できます。

チェックの対応する無料のドライバーを置換するときに、簡単にシステムによって提供されるドライバー コンポーネントを別のイメージを提供する方法はありません。 したがって、チェックされているドライバーとシステムに無料のドライバーを置換すると、チェックされているドライバーを使用しますか、無料またはチェックされているバージョンのオペレーティング システム イメージと HAL が開始されるとします。 そのため、無料のドライバーを後で復元するようにチェックされている、対応するを置換するすべてのドライバーの元の無料バージョンの名前を変更 (またはコピー) をする可能性があります。

最後に、いつでも変更すること、標準のファイル システム ディレクトリのいずれかに存在するのいずれかに注意してください (%systemroot% など\\system32) Windows ファイル保護 (WFP) は、WFP が最初に無効になっていない場合に、元の状態のファイルを復元します。 デバッガーがシステムに接続されている場合、次のレジストリ値を変更することで一時的に WFP を無効にすることができます。

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon
SFCDisable:REG_DWORD:2
```

設定**SFCDisable** 2 の値に、WFP を次回の起動時に (のみ) を無効にします。 0 (既定値) の値には、WFP が有効になります。 WFP の機能については、Microsoft Windows SDK を参照してください。 WFP のレジストリ設定の詳細については、[Microsoft サポート技術情報記事 Q222473](https://go.microsoft.com/fwlink/p/?linkid=38360)を参照してください。

 

 





