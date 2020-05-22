---
title: 確認済みのオペレーティングシステムと HAL のインストール (Windows XP および Windows Server 2003)
description: チェック済みのオペレーティング システムと HAL のみのインストール (Windows XP と Windows Server 2003)
ms.assetid: 51175951-9267-4d92-8b47-4dd2155f4e56
keywords:
- チェック済みビルド WDK、インストール
- 無料ビルド WDK
- 製品版ビルド WDK
- HAL WDK
- 部分的にチェックされたビルドの WDK
- WDK チェックビルドの名前
- チェックされたファイルのコピー
- Boot.ini ファイル WDK、チェックされたビルド
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: f4cf103b68090b83c107e9ce97fe8973b69b21f6
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769614"
---
# <a name="installing-just-the-checked-operating-system-and-hal-for-windows-xp-and-windows-server-2003"></a>チェック済みのオペレーティング システムと HAL のみのインストール (Windows XP と Windows Server 2003)

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

## <span id="ddk_installing_just_the_checked_operating_system_and_hal_tools"></span><span id="DDK_INSTALLING_JUST_THE_CHECKED_OPERATING_SYSTEM_AND_HAL_TOOLS"></span>

コンピューターに完全なチェックを行ったビルドをインストールする代わりに、システムの無償ビルドをインストールし、オペレーティングシステムイメージと HAL のチェックされたバージョンをインストールすることができます。 この手順を使用する場合は、ブートローダーを構成して2つのブートオプションを提供できます。 最初のブートオプションは、無料のビルド用です。 2番目のブートオプションは、チェックされたオペレーティングシステムイメージと HAL を使用してシステムを起動しますが、他のすべてのシステムコンポーネントの無料バージョンを使用します。

この方法では、完全なチェックを行ったビルドをインストールする場合と比較して、次のような利点があります。

-   ドライバーにより、オペレーティングシステムと HAL のデバッグチェックの利点が得られます。 同時に、オペレーティングシステムと HAL 以外のシステムコンポーネントの空きバージョンが使用されているため、システム全体のパフォーマンスへの影響が最小限に抑えられています。

-   1回のインストール (つまり、1つのシステムディレクトリ、1つの実行可能コンポーネントのセット、および1つのレジストリパラメーターセット) では、ブート時に決定されたオペレーティングシステムイメージと HAL のチェックされたバージョンまたは無料バージョンのいずれかを使用できます。

オペレーティングシステムイメージと HAL のチェックされたバージョンをインストールするには、 \\ 新しい一意のファイル名を使用して、チェックされた配布メディアから% SystemRoot% system32 ディレクトリに適切なファイルをコピーする必要があります。 次に、システムの起動時にこれらのファイルを使用するオプションを提供するようにシステムに指示する必要があります。 確認済みのオペレーティングシステムと HAL イメージをインストールする場合は、次の重要なガイドラインに注意する必要があります。

-   オペレーティングシステムのイメージと HAL は常に同期しておく必要があります。 したがって、オペレーティングシステムイメージのチェック済みバージョンを使用する場合は、チェックされたバージョンの HAL も使用する必要があります (その逆も同様です)。 システムのオペレーティングシステムイメージと HAL を調整してもシステムを起動できないようにすることができます。

-   無料のビルドのインストール中にインストールされたオペレーティングシステムイメージと HAL の無料バージョンは上書きしないでください。 オペレーティングシステムイメージと HAL の空きバージョンを上書きすると、システムを起動できなくなり、エラーから回復するのが困難になる可能性があります。 そのため、オペレーティングシステムと HAL のチェックされたバージョンを% SystemRoot% system32 ディレクトリにコピーするときは、必ず新しい一意のファイル名を使用して \\ ください。

-   使用する確認済みのディストリビューションが、無償のシステムと同じサービスパック番号であることを確認します。 たとえば、オンになっているオペレーティングシステムイメージと HAL を、無料のビルドシステムの Service Pack 2 がインストールされているシステムにインストールする場合は、使用する確認済みの配布も Service Pack 2 であることを確認してください。

部分チェックされたビルドをインストールする手順は次のとおりです。

### <a name="span-idstep_1__identifying_the_files_to_installspanspan-idstep_1__identifying_the_files_to_installspanstep-1-identifying-the-files-to-install"></a><span id="step_1__identifying_the_files_to_install"></span><span id="STEP_1__IDENTIFYING_THE_FILES_TO_INSTALL"></span>手順 1: インストールするファイルの識別

部分チェックされたビルドをインストールする最初の手順は、システムに無料ビルドをインストールするために使用されたオペレーティングシステムイメージと HAL ファイルのバージョンを判断することです。

NT ベースのオペレーティングシステム配布メディアには、オペレーティングシステムと HAL イメージのいくつかの異なるバージョンが用意されています。 これらの異なるバージョンは、プロセッサとその他のシステムハードウェアのさまざまな組み合わせをサポートするために用意されています。 オペレーティングシステムソフトウェアがインストールされると、インストール手順によって、使用するオペレーティングシステムイメージと HAL イメージが自動的に特定され、配布メディアからシステムの% SystemRoot% system32 ディレクトリに適切なファイルがコピーされ \\ ます。

インストールされるオペレーティングシステムイメージファイルは、1つまたは複数のプロセッサがサポートされているかどうか、および物理アドレス拡張 (PAE) がサポートされているかどうかによって異なります (PAE は 4 GB を超える物理メモリを持つシステムでアクティブです)。 配布メディアのファイル名は次のとおりです。

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
4 GB 以下の物理メモリを搭載したユニプロセッサ x86 アーキテクチャシステム。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa  
PAE がサポートされているユニプロセッサ x86 アーキテクチャシステム。

<span id="NTKRNLMP.EXE"></span>ntkrnlmp  
4 GB 以下の物理メモリを搭載したマルチプロセッサ x86 アーキテクチャシステム。

<span id="NTKRPAMP.EXE"></span>ntkrpq  
PAE がサポートされているマルチプロセッサ x86 アーキテクチャシステム。

同様に、HAL にはいくつかの異なる名前があります。

システムのインストール時に、インストール手順によって、システムにインストールする適切なオペレーティングシステムイメージと HAL が決定されます。 選択したファイルは、インストール時に、 \\ 固定の既知の名前を使用して% SystemRoot% system32 ディレクトリにコピーされます。 これらの固定名を使用することにより、ローダーは起動時にこれらのファイルを簡単に見つけることができます。 これらのファイルの固定名は次のとおりです。

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
4 GB 以下の物理メモリを搭載した x86 システムのオペレーティングシステムイメージ。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa  
4 GB を超える物理メモリを搭載した x86 システムのオペレーティングシステムイメージ。

<span id="HAL.DLL"></span>hal.dll  
読み込み可能の HAL イメージ。

場合によっては、システムのハードウェア構成によっては、1つまたは複数のファイルの名前が適切な固定名に変更されることがあります。 また、配布メディアのファイル名が、必要な固定ファイル名と同じである場合もあります。

チェックしたオペレーティングシステムイメージと HAL をインストールするには、システムのインストール時にシステムにコピーされたイメージの元の名前を最初に決定する必要があります。 これを実行するには、ファイル% SystemRoot% \\ repair \\ setup .log を調べます。 これは隠しファイルであるため、 **dir**コマンドを使用して表示するには、その属性を変更する必要があります。

セットアップ .log ファイルには、 \\ システムのインストールプロセス中に、配布メディアから% SystemRoot% system32 ディレクトリにコピーされたファイルが一覧表示されます。

セットアップ .log ファイルの例を次に示します。

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

サンプルのセットアップログファイルには、インストール中に2つのオペレーティングシステムイメージファイルが \\ winnt \\ system32 ディレクトリ (% SystemRoot% \\ system32) にコピーされていることがわかります。 ファイル ntkntkrnlpa は、配布メディアからにコピーされ、ntkrnlmp ファイルがディストリビューションメディアから ntoskrnl.exe にコピーされています。 このサンプルでは、HAL ファイル (% SystemRoot% system32 ディレクトリの固定名の hal.dll) は、 \\ もともと halmacpi という名前でした。

**警告**   一部の HAL ファイルには、似た名前の一見があります。 たとえば、halacpi と halapic は2つの一般的に使用される Hal です。 システムに適したバージョンの HAL を使用するように注意してください。 間違った HAL を選択すると、システムが起動できなくなります。

 

### <a name="span-idstep_2__copying_the_checked_filesspanspan-idstep_2__copying_the_checked_filesspanstep-2-copying-the-checked-files"></a><span id="step_2__copying_the_checked_files"></span><span id="STEP_2__COPYING_THE_CHECKED_FILES"></span>手順 2: チェックしたファイルのコピー

システムのインストール中に使用されたファイルの名前がわかったので、これらのファイルのチェックされたバージョンをシステムにコピーできます。 確認した配布キットで特定したファイルを検索します。 次に、これらのファイルをシステムの% SystemRoot% system32 ディレクトリにコピーし \\ て、新しい一意のファイル名を指定します。 これらのファイルのコピーは、8.3 の名前付け規則に従う必要があります。 8.3 に準拠した一意のファイル名を保証する方法の1つとして、ファイルの種類の名前を元のファイルの種類 (.dll または .exe) から .chk に変更する方法があります。 したがって、手順 1. の例を使用して、次のように、チェックされた配布キットからファイルをコピーします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">確認した配布の元のファイル名が次のようになっている場合:</th>
<th align="left">次のファイル名にコピーします。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ntkrnlmp</p></td>
<td align="left"><p>ntkrnlmp</p></td>
</tr>
<tr class="even">
<td align="left"><p>ntkrpq</p></td>
<td align="left"><p>ntkrpq amp</p></td>
</tr>
<tr class="odd">
<td align="left"><p>halmapic</p></td>
<td align="left"><p>halmapic</p></td>
</tr>
</tbody>
</table>

 

チェックされた配布の一部のファイルは、圧縮された形式で提供されます。 これらのファイルは、ファイルの種類の最後の文字としてアンダースコア文字で示されます。 たとえば、チェックされたビルド配布キットで halapic ファイルを検索する場合、ファイル halapic は \_ 正しいファイルですが、圧縮形式であることがわかります。

チェックされた配布から圧縮ファイルを圧縮解除するには、Expand ユーティリティ (% SystemRoot% \\ system32 \\ expand .exe) を使用します。 たとえば、halapic を展開 \_ し、拡張されたファイルの名前を halapic にするには、コマンドプロンプトウィンドウから次のコマンドを実行します。

```
> expand halapic.dl_ halapic.chk
```

### <a name="span-idstep_3__editing_boot_inispanspan-idstep_3__editing_boot_inispanstep-3-editing-bootini"></a><span id="step_3__editing_boot_ini"></span><span id="STEP_3__EDITING_BOOT_INI"></span>手順 3: boot.ini を編集する

チェックされたファイルを% SystemRoot% system32 ディレクトリにコピーした後 \\ 、これらのチェックされたファイルの使用をシステムが開始できるようにするブート時オプションを作成する必要があります。 これを実行するには、boot.ini ファイルを編集します。

一般的な手順については、「boot.ini[ファイルの編集](editing-the-boot-ini-file.md)」を参照してください。

このような場合は、新しいブート時オプションを作成する必要があります。このオプションを使用すると、インストールしたオペレーティングシステムイメージと HAL のチェック対象バージョンを使用してシステムを起動できます。

Windows インストールを参照する boot.ini の [ ** \[ オペレーティングシステム \] ** ] セクションで、行を見つけます。 2番目のコピーを作成し、コピーした行の末尾に次のパラメーターを追加します。

```
/kernel=KernelFile /hal=HalFile 
```

ここで、は、チェックされた配布キットから以前にコピーしたオペレーティングシステムイメージファイルの*チェックされ*たバージョンの名前です。 *HalFile*は、チェックを行った配布キットから既にコピーした HAL のチェック対象バージョンの名前です。

オペレーティングシステムを説明する行に **/pae**パラメーターが含まれている場合は、オペレーティングシステムイメージのチェックされたバージョンを必ず使用してください。 オペレーティングシステムを説明する行に **/pae**パラメーターがない場合は、オペレーティングシステムイメージのチェックされたバージョンを使用します。

また、新しい行の引用符で囲まれたテキストも変更する必要があります。これにより、どの行がフリービルドであり、どの行が部分チェックされたビルドであるかを識別できるようになります。

このような boot.ini ファイルの例を次に示します。

```
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(1)\WINNT
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINNT="Microsoft Windows 2000 Professional" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINNT="Windows 2000 Checked" /fastdetect /kernel=ntoskrnl.chk /hal=halacpi.chk
```

カーネルデバッガーでチェックしたビルドを使用する場合は、適切なデバッグ関連のパラメーターも追加する必要があります。 ( **/Kernel**パラメーターと **/hal**パラメーターは、デバッグを自動的に有効にしません)。詳細については、「boot.ini[ファイルの編集](editing-the-boot-ini-file.md)」を参照してください。

変更が完了したら、変更を保存し、エディターを終了します。 次回このシステムを起動したときに、選択したオペレーティングシステムイメージと HAL を選択できる新しいオペレーティングシステムブートオプションが表示されます。

### <a name="span-idinstalling_additional_checked_filesspanspan-idinstalling_additional_checked_filesspaninstalling-additional-checked-files"></a><span id="installing_additional_checked_files"></span><span id="INSTALLING_ADDITIONAL_CHECKED_FILES"></span>追加のチェックされたファイルのインストール

確認済みのオペレーティングシステムと HAL がインストールされたら、追加のチェックされたコンポーネントをインストールすることができます。 いくつかの重要なコンポーネントのインストール済みの無料版を、チェックされている配布メディアの対応するバージョンに置き換えることができます。 これは、たとえば、他のデバイスのスタック内に存在するドライバーを作成する場合などに便利です。 スタック内のドライバーの上位および下位にあるドライバーの無料バージョンを置き換えることで、これらのコンポーネントで追加のエラーチェックを有効にすることができます。 これにより、ドライバーの問題をより迅速かつ簡単に識別できるようになります。

フリードライバを対応するチェックを行う場合、システムによって提供されるドライバコンポーネントの代替イメージを簡単に提供する方法はありません。 このため、空きドライバーをシステムのチェックされたドライバーに置き換えると、オペレーティングシステムイメージと HAL の空きまたはチェックが開始されたときに、チェックされたドライバーが使用されます。 そのため、後で無料のドライバーを復元できるように、置き換えられるドライバーの元の無料バージョンの名前を変更する (またはコピーする) ことをお勧めします。

最後に、システムディレクトリのいずれかに存在する標準ファイル (% SystemRoot% system32 など) のいずれかを変更するたびに、 \\ wfp が最初に無効にされない限り、そのファイルは元の状態に復元されることに注意してください。 デバッガーがシステムにアタッチされている場合は、次のレジストリ値を変更することによって、WFP を一時的に無効にすることができます。

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon
SFCDisable:REG_DWORD:2
```

**SFCDisable**を2の値に設定すると、次回のブートでは WFP が無効になります (のみ)。 値 0 (既定値) を指定すると、WFP が有効になります。 WFP の機能の詳細については、Microsoft Windows SDK を参照してください。

 

 





