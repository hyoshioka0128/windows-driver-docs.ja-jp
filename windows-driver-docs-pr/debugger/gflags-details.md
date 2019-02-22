---
title: GFlags の詳細
description: GFlags の詳細
ms.assetid: 97faa63d-b876-4973-812f-f3bdd57c1778
keywords:
- GFlags、詳細情報
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69d6a1b8ef059eb022b24dc5d844dafd57d70200
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549817"
---
# <a name="gflags-details"></a>GFlags の詳細


## <span id="ddk_gflags_details_dtools"></span><span id="DDK_GFLAGS_DETAILS_DTOOLS"></span>


GFlags ができ、Windows レジストリと内部の設定を編集することによってシステムの機能を無効にします。 このセクションでは、GFlags の操作の詳細を説明し、GFlags を最も効率的に使用するためのヒントが含まれています。

### <a name="span-idgeneralinformationspanspan-idgeneralinformationspangeneral-information"></a><span id="general_information"></span><span id="GENERAL_INFORMATION"></span>一般的な情報

-   コマンドラインで、GFlags ダイアログ ボックスを表示する次のように入力します。 **gflags** (パラメーターなし) を使用します。

-   レジストリまたはカーネル モードでは、フラグを設定する Windows Server 2003 および Windows の以前のバージョンでは、コンピューターの Administrators グループのメンバーをする必要があります。 ただし、ユーザーをゲスト アカウントの最小のアクセスは GFlags ダイアログ ボックスからプログラムを起動できます。

-   GFlags システム レベルのレジストリ設定はレジストリには、すぐに表示が有効になりません、システムを再起動するまで。

-   GFlags イメージ ファイルのレジストリ設定はレジストリには、すぐに表示が有効になりませんプロセスを再起動するまで。

-   GFlags ダイアログ ボックスで、デバッガーと起動の機能は、特定のプログラムです。 のみ設定できますに 1 つのイメージ ファイルを一度に。

### <a name="span-idflagdetailsspanspan-idflagdetailsspanflag-details"></a><span id="flag_details"></span><span id="FLAG_DETAILS"></span>フラグの詳細

-   すべてのフラグをクリアするには、-FFFFFFFF に、フラグを設定します。 0 に、フラグを設定すると、現在のフラグ値に 0 が追加されます。

-   Windows イメージ ファイルのすべてのフラグをクリアし、削除 FFFFFFFF (0 xffffffff) にイメージ ファイルのフラグを設定すると、 **GlobalFlag**イメージ ファイルのレジストリ キー エントリ。 イメージ ファイルのレジストリ キーが保持されます。

### <a name="span-iddialogboxandcommandlinespanspan-iddialogboxandcommandlinespandialog-box-and-command-line"></a><span id="dialog_box_and_command_line"></span><span id="DIALOG_BOX_AND_COMMAND_LINE"></span>ダイアログ ボックスとコマンドライン

GFlags、便利なダイアログ ボックスを使用するか、コマンドラインから実行できます。 ほとんどの機能が、次の例外の両方の形式で利用できます。

**ダイアログ ボックスのみ**

-   起動します。 指定したフラグを使用してプログラムを起動します。

-   デバッガーでプログラムを実行します。

-   [特別なプール](special-pool.md)Windows Vista より前のシステムにします。 Windows Vista および Windows の以降のバージョンでは、コマンドラインまたは Gflags ダイアログ ボックスで、特別なプール機能を構成できます。

**コマンドラインのみ**

-   ユーザー モードのスタック トレースのデータベースのサイズを設定 (/tracedb)。

-   ページ ヒープの検証オプションを設定します。

### <a name="span-idregistryinformationspanspan-idregistryinformationspanregistry-information"></a><span id="registry_information"></span><span id="REGISTRY_INFORMATION"></span>レジストリ情報

セッション間で保存されている GFlags 設定は、レジストリに格納されます。 クエリまたはこれらの値を変更するのには、レジストリ Api、Regedit、または reg.exe を使用できます。 次の表では、設定とレジストリの格納場所の種類を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>システム全体の設定 (&quot;レジストリ&quot;)</p></td>
<td align="left"><p>Hkey_local_machine \system\currentcontrolset\control\session Manager&lt;強力な&gt;GlobalFlag</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>プログラムに固有の設定 (&quot;イメージ ファイル&quot;) コンピューターのすべてのユーザー。</p></td>
<td align="left"><p>Hkey_local_machine \software\microsoft\windows nt \currentversion\image File Execution Options&lt;em&gt;ImageFileName</em>&lt;強力な&gt;GlobalFlag</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>特定のプログラムの自動終了設定 (&quot;サイレント プロセス終了&quot;) コンピューターのすべてのユーザー。</p></td>
<td align="left"><p>Hkey_local_machine \software\microsoft\windows NT\CurrentVersion\SilentProcessExit&lt;em&gt;ImageFileName</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>コンピューターのすべてのユーザーのイメージ ファイルをページ ヒープのオプション</p></td>
<td align="left"><p>Hkey_local_machine \software\microsoft\windows nt \currentversion\image File Execution Options&lt;em&gt;ImageFileName</em>&lt;強力な&gt;PageHeapFlags</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ユーザー モードのスタック トレースのデータベース サイズ (<strong>tracedb</strong>)</p></td>
<td align="left"><p>Hklm \software\microsoft\windows nt \currentversion\image File Execution Options&lt;em&gt;ImageFileName</em>&lt;強力な&gt;StackTraceDatabaseSizeInMb</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>ユーザー データベースの作成モード スタック トレース (ust、0x1000) のイメージ ファイル</p></td>
<td align="left"><p>Windows イメージ ファイル名を USTEnabled レジストリ エントリの値に追加します (hklm \software\microsoft\windows nt \currentversion\image File Execution Options&lt;強力な&gt;USTEnabled</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可能であれば大きなページを使用してイメージを読み込む</p></td>
<td align="left"><p>Hklm \software\microsoft\windows nt \currentversion\image File Execution Options&lt;em&gt;ImageFileName</em>&lt;強力な&gt;UseLargePages</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>特別なプール</p>
<p>(カーネルの特別なプール タグ)</p></td>
<td align="left"><p>HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management&lt;strong&gt;PoolTag</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>確認の開始/終了を確認します</p></td>
<td align="left"><p>Hklm \system\currentcontrolset\control\session \memory Management\PoolTagOverruns します。 <strong>開始確認</strong>オプション値を 0 に設定します。 <strong>終了の確認</strong>オプション値を 1 に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>イメージ ファイルをデバッガー</p></td>
<td align="left"><p>Hklm \software\microsoft\windows nt \currentversion\image File Execution Options&lt;em&gt;ImageFileName</em>&lt;強力な&gt;デバッガー</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>オブジェクト参照のトレース</p></td>
<td align="left"><p>Hklm \system\currentcontrolset\control\session Manager\Kernel&lt;強力な&gt;ObTraceProcessName</strong>、 <strong>ObTracePermanent</strong>と<strong>ObTracePoolTags</strong></p></td>
</tr>
</tbody>
</table>

 

 

 





