---
title: INF の検証エラーと警告
description: ドライバーのインストールのエラーと警告は、Microsoft Visual Studio で実行される自動 INF 検証の結果として表示できます。
ms.assetid: E021D8F8-BFDA-4F71-B8EA-0997096761FB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6caa307ecdfe6a720f8f1050c89193a9a6e72040
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902514"
---
# <a name="inf-validation-errors-and-warnings"></a>INF の検証エラーと警告

このトピックでは、ドライバーのインストール エラーを説明しますと、Microsoft Visual Studio 自動 INF 検証の結果として表示される警告の実行またはを実行すると、 [InfVerif](infverif.md)ツール。

INF ファイルの次のエラーは、ドライバーをビルドするときに、WDK 10 では、Visual Studio 2015 以降、エラー一覧 ウィンドウに表示できます。 InfVerif.exe をコマンドラインから実行する場合は、コマンド プロンプトで、または結果の HTML バージョンに、これらのエラーが表示されます。

## <a name="error-guidance"></a>エラーのガイダンス

InfVerif 一般的な次のようにルールを下のエラー番号より重大な問題です。
ほとんどのエラー コードは、警告またはエラーに応じて InfVerif に指定された引数のいずれかにできます。

### <a name="handling-errors"></a>エラーの処理

ハードウェア デベロッパー センター ダッシュ ボードのドライバーのテストに合格するために、すべてのエラーを修正する必要があります。 エラーは、次の条件に関連します。

- INF パーサーは、INF を正しく解釈できません。
- INF パーサーが既定値前提 (あいまいな構文) を行うことによってのみ、INF を解釈できません。
- InfVerif を引数では、ルール セットが (ユニバーサル) などの INF に適用されることを示します

デベロッパー センターでのドライバーを送信する前に警告を修正する必要はありませんが、報告される問題を把握する時間をかけてお勧めします。 特定の警告がわからない場合、INF 可能性がありますいない常に期待どおりに動作します。

通常は警告に関連します。

- そうでない可能性がありますが、有効なシナリオが適切な構文
- 構文は、特定の InfVerif パラメーターに対して有効ですが、ユニバーサルなどの他のモードでエラーが発生します。

場合、[ユニバーサル] 設定に関連する問題がエラーとして表示されます。

- Visual Studio で、ターゲット プラットフォームの設定で、ドライバーをビルドする**ユニバーサル**または**Mobile**します。
- /U フラグを指定して、コマンドラインから InfVerif.exe を実行します。

[ユニバーサル] 設定に関連する問題は、場合に、警告として表示されます。

- Visual Studio で、ターゲット プラットフォームの設定で、ドライバーをビルドする**デスクトップ**します。
- コマンドラインから InfVerif.exe を実行し、/u フラグを指定しません。

## <a name="error-codes"></a>エラー コード

エラー コードは、次の分類があります。

- [INF ファイル (1100 1299) 内の構文](#syntax-in-the-inf-file-1100-1299)
- [ユニバーサル INF (1319 1300)](#universal-inf-1300-1319)
- [インストール (2000 ~ 2999)](#installation-2000-2999)

すべてのエラー コードは、簡単明瞭な意味を持つ多くのように、以下に示します。 1000 1099 範囲内のエラーは基本的な構文エラーは、現在と見なされます。

## <a name="syntax-in-the-inf-file-1100-1299"></a>INF ファイル (1100 1299) 内の構文

ドライバーの送信エラーの意味 InfVerif 障害中にドライバーのインストールはまだ成功する可能性があります。
これは、ため、エラーが INF ファイルに存在する場合は、ドライバーをインストールすると、Windows もときに、設定の既定値です。
Windows では、エラーが原因で、この範囲は、ドライバーのインストールは失敗しませんが、この範囲のエラーは、OS バージョンまたは SKU に応じて動作を変更する可能性があることを示します。
ドライバーが正常にインストールする場合、これらのエラーを示すを*は*状況で、ドライバーが正しくインストールしない場合があります。

<table>
<thead>
<tr>
<th>エラー コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>1100:DriverStore Copyfile 名が一致しません</strong></td>
<td>このエラーは、ファイルをコピーしたり、元のドライバー ストアの名前と場所から別の名前と、ドライバー ストア内の場所に名前を変更すると発生します。  以下に例を示します。
<pre>
[SourceDisksFiles]
DriverFile.sys=1,x64  

[DestinationDirs]
CopyFileSection=13,SubDirectory  
  
[CopyFileSection]
DriverFile.sys
</pre>
ドライバー ストアは、元のドライバー パッケージのディレクトリ構造を保持します。  DriverFile.sys の元の場所は、上記のコードで<i>INF 場所</i>\x64 が CopyFiles ディレクティブが配置で<i>INF 場所</i>\SubDirectory。  同じエラーは、コピーの一部として、ファイルの名前が変更されたかどうかは表示されます。</td>
</tr>
<tr>
<td><strong>1203:セクションが見つかりません</strong></td>
<td>たとえば、INF、次の構文では、エラー 1203 が発生します。
<pre>
[MyInstallSection]
CopyFiles=driverFile.sys
</pre>
ため、このエラーが報告された、 <strong>CopyFiles</strong>ディレクティブ (をコピーするファイルの一覧を指定する) セクション名が必要ですが。 ただし、 <strong>CopyFiles</strong>ディレクティブは、ファイル名を指定できます。 ファイル名を付けるセクション名とファイル名を区別するために、次に示すようにトークン @。
<pre>
[MyInstallSection]
CopyFiles=@driverFile.sys
</pre>
</td>
</tr>
<tr>
<td><strong>1204:プロバイダーが Microsoft にすることはできません。</strong></td>
<td>[バージョン] セクションで、[プロバイダー] フィールドには、Microsoft を指定できません。
<pre>
[Version]
Signature="$Windows NT$"
Class=Sample
ClassGuid={78A1C341-4539-11d3-B88D-00C04FAD5171}
Provider="Microsoft"
</pre>
</td>
</tr>
<tr>
<td><strong>1205:[Directive1] から参照セクション [Driver_files] と [Directive2] ディレクティブ</td>
<td>同じセクションに 2 つの異なるディレクティブがポイントされるたびに、この警告が生成されます。
  <p>いるほとんどの場合は、実際には、エラー、場合によっては 1205 報告される場合でも、条件が意図的に注意してください。</td>
</tr>
<tr>
<td><strong>1212:[DefaultInstall] 両方を含めることはできませんと [Manufacturer]</strong></td>
<td>1 つの INF [DefaultInstall] 両方を含めることはできませんと [Manufacturer]。  Inf の両方で作成されたは、2 つのセクションの 1 つを削除する必要があります。
</td>
</tr>
<tr>
<td><strong>1220:含まれる、INF で定義されているセクションを直接参照することはできません。</strong></td>
<td>INF ファイルを参照する場合、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547344">DDInstall</a>セクションに含まれる INF では、使用する必要があります、<strong>必要がある</strong>ディレクティブ。 含まれる INF セクションを参照するその他のディレクティブは、エラー 1220 になります。
<p>この例では、A.INF のインストール セクションは、B.INF、同等のインストール」セクションを参照します。</p>
<p>A.INF が含まれます。</p>
<div class="code">
<pre>
A.INF
[InstallSectionA]
Include = B.INF
Needs = InstallSectionB
AddReg = AddRegB ; WARNING 1220

[InstallSectionA.Services]
Include = B.INF
Needs = InstallSectionB.Services
</pre>
<p>B.INF が含まれます。</p>
<pre>
B.INF
[InstallSectionB]
AddReg = AddRegB
[InstallSectionB.Services]
...

[AddRegB]
...
</pre>
</div>
<p><strong>必要がある</strong>ディレクティブは、現在のインストール セクションで処理するのと同じインストール セクションを参照する必要があります。 たとえば、ニーズ ディレクティブ [InstallSectionA.Services] は をポイントする必要があります、します。別のサービスでは、セクションをインストールします。 <strong>必要がある</strong>ディレクティブを使用して同じ INF の別の DDInstall セクションの動作を追加することも可能性があります。 使用して、<strong>必要がある</strong>望ましくない動作セクションの他の種類でのディレクティブがあります。</p></td>
</tr>
<tr>
<td><strong>1221:サービスのレジストリ キーを変更することはできません、HKR を使用する必要があります</strong></td>
<td>このエラーは、INF ファイルなど、サービスのレジストリ キー内の場所を参照することを示します<strong>hklm \system\currentcontrolset\services&lt;em&gt;サービス名</em></strong>します。 サービス キーにアクセスするときは、相対的なルートを代わりに使用する必要があります (<strong>HKR</strong>) に、レジストリ値をデバイスまたはドライバーのインスタンスに関連付けます。
<p>使用すると<strong>HKR</strong>レジストリ値は、デバイスがインストールされるまでには表示されません。</p></td>
</tr>
<tr>
<td><strong>1230:ファイル [SourceDisksFiles] セクションの下には、"xxxx"がありません。</strong></td>
<td>これは、ファイルが、ドライバー パッケージの一部として指定されましたが、[SourceDisksFiles] セクションでは、INF、ファイルのソースの場所は指定されていないことを示します。
<pre>
[SourceDisksFiles]
filename=disk id
</pre>
[SourceDisksFiles] のアーキテクチャで修飾されたバージョンが指定されている場合に、このエラーを頻繁に発生ことに注意してください ([SourceDisksFiles.amd64] など、INF でサポートされているすべてのアーキテクチャが [SourceDisksFiles] セクション。</td>
</tr>
<tr>
<td><strong>1233:署名のために必要なディレクティブがありません。</strong></td>
<td>[バージョン] セクションでは、ドライバー パッケージの署名を受信する CatalogFile ディレクティブ (と関連するカタログ ファイル) を指定する必要があります。
<pre>
CatalogFile=wudf.cat
</pre>
</td>
</tr>
<tr>
<td><strong>1235:[文字列] で定義されていない文字列トークン</strong></td>
<td>[文字列] セクションでは、指定した文字列のトークンの定義がありません。 たとえば、INF ファイルを指定します<em>%reg_dword</em>で、<em>追加レジストリ セクション</em>で指定された、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff546320"> <strong>AddReg</strong> </a>ディレクティブがあります。対応するありません REG_DWORD = で 0x00010001、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547485">[文字列]</a>セクション。
<p>このエラーは、INF ファイルを環境変数を含むレジストリ値を指定する場合に頻繁に発生します。 以下に例を示します。</p>
<pre>
[MyAddReg]
HKR,,DllPath,%SystemRoot%\System32\myDll.sys
</pre>
この行は、"%systemroot%"レジストリ内のリテラル"%systemroot%"の保存の動作目的ではなく、[文字列] セクションからトークンを検索しようとする INF パーサーをによりします。  文字列置換を実行するのではなく、リテラル値の %systemroot% を使用するには、エスケープ シーケンスを使用して %% です。
<pre>
[MyAddReg]
HKR,,DllPath,%%SystemRoot%%\System32\myDll.sys
</pre>
</td>
</tr>
<tr>
<td><strong>1285:Microsoft によって定義されたクラスの [ClassInstall32] セクションを指定することはできません。</strong></td>
<td>時点で、Windows 10、IHV が指定した Inf は許可されません [ClassInstall32] を使用する任意の Microsoft によるクラスの INF で。
</td>
</tr>
<tr>
<td><strong>1296:指定されたサービスのハードウェアに関連付けられていません。</strong></td>
<td>Windows 10、バージョンは 1809、以降と、エラーが発生する警告から変更がこれです。  します。サービスのセクションでは、定義されている各ターゲット OS 必要があります。  これはよい方法でありは 1809 だけでなくすべての Inf に適用されます。  

以前いない含める場合このセクションで、サービスはありませんでしたし、受信トレイのドライバー サービスに依存しているため、しを作成しなければならないのです。サービスのセクションで、ニーズを使用して受信トレイ INF のサービスを参照し、ステートメントが含まれています。  

例:INF ファイルに次の必要があります。このエラーを解決するには、各 OS ターゲット セクションをサービスします。

<pre>
[XXXXXXXX.Install.NTx86.Services]
Include=filename.inf
Needs=inf-section-name.Services
</pre>

関数のドライバーを必要としないデバイスの場合は、NULL ドライバーとしては、次のように指定できます。
<pre>
AddService = ,2.
</pre>
<b>のみ、INF がドライバーを必要としませんを指定する非機能的なデバイスをインストールする場合は、これを使用します。</b>
</td>
</tr>
</tbody>
</table>

## <a name="universal-inf-1300-1319"></a>ユニバーサル INF (1319 1300)

>[!IMPORTANT]
>ドライバーの INF ファイルが得られなかった場合は、エラーや警告はエラー番号の範囲 13 の場合は、ユニバーサル*xx*します。

INF 構成機能には、次のエラーと警告が関連します。

<table>
<thead>
<tr>
<th>エラー/警告コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>1300:見つかったレガシ</strong><em>Xxx</em></td>
<td>セクションでは非推奨またはディレクティブをなど、使用する場合、このエラーが表示されます<a href="https://msdn.microsoft.com/library/windows/hardware/ff547448"> <strong>LogConfig</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff547321"> <strong>DDInstall.CoInstallers</strong></a>します。</td>
</tr>
<tr>
<td><strong>1301:見つかったレガシ</strong><em>Xxx</em><strong>操作</strong><em>Xxx</em></td>
<td>セクションでは非推奨またはディレクティブをなど、使用する場合、このエラーが表示されます<a href="https://msdn.microsoft.com/library/windows/hardware/ff547448"> <strong>LogConfig</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff547321"> <strong>DDInstall.CoInstallers</strong></a>します。</td>
</tr>
<tr>
<td><strong>1302:見つかったレガシ</strong><em>Xxx</em><strong>操作</strong><em>Xxx</em></td>
<td>このエラーは、サービスを削除するか、ファイルを削除するように、ドライバー パッケージに外部の何か、操作に影響する場合に発生します。</td>
</tr>
<tr>
<td><strong>1303:Co-installer を定義する従来の操作が見つかりません</strong></td>
<td>エラー 1303 は AddReg 操作が、共同インストーラーを指定することを示します。 例:
<pre>
AddReg = HKR,,CoInstallers32,0x00010000,"MyCoinstaller.dll"
</pre>
</td>
</tr>
<tr>
<td><strong>1304:非相対キーを使用して従来の操作が見つかりません</strong></td>
<td>エラー 1304 では、レジストリの操作が HKR 以外のレジストリ ルートを使用することを示します。</td>
</tr>
<tr>
<td><strong>1305:追加可能なマルチ sz 値を使用して従来の操作が見つかりません</strong></td>
<td>エラー 1305 は、INF がからの値を削除することを示します、 <strong>REG_MULTI_SZ</strong>を既存の値を追加または<strong>REG_MULTI_SZ</strong>します。</td>
</tr>
<tr>
<td><strong>1306:システム以外のターゲット パスを持つ従来の操作が見つかりません</strong></td>
<td>エラー 1306 では、ファイルのコピーが %systemroot% ではないターゲットを指定することを示します。</td>
</tr>
<tr>
<td><strong>1310-1312:ニーズ ディレクティブの正しくないセクションの拡張機能</strong></td>
<td>必要なディレクティブは、参照元セクションに必要なセクションのコピー/貼り付けを効果的に実行します。  基準計画の検証としては、InfVerif はセクションの拡張機能を比較します。  つまり、[DDInstall.Services] が [DDInstall.Services] セクションでは他の上でニーズ ディレクティブを使用できますのみこと。</td>
</tr>
<tr>
<td><strong>1313-1314:不足しているディレクティブが含まれています</strong></td>
<td>ニーズ ディレクティブを使用する各セクションでは、ターゲット セクションが含まれている INF を参照する対応する Includes ディレクティブが必要があります。  以前に別の INF セクション Include ディレクティブがあった場合、ニーズのディレクティブは有効になります。</td>
</tr>
<tr>
<td><strong>133 x:機能のエラー</strong></td>
<td>複数のレジストリ セクションは、1 つのグローバル キーに書き込みます。 たとえば、さまざまなセクションでは、さまざまなサービスの構成に設定されたサービス グローバル レジストリ キーのセットを別のデータ値、またはコピー先ファイルが別のソース ファイルを指定する可能性があります。</td>
</tr>
</tbody>
</table>

## <a name="installation-2000-2999"></a>インストール (2000 ~ 2999)

2000 ~ 2999 範囲内での問題は、警告として表示されます。 使用可能な値は、次に示します。

<table>
<thead>
<tr>
<th>エラー コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>2083:セクションを参照または使用</strong></td>
<td>この警告は、INF ファイルで参照されていないセクションを提供することを示します。 ドライバーがインストールされている場合、警告で参照されているセクションの内容は評価されません。</td>
</tr>
<tr>
<td><strong>2222:従来のディレクティブは無視されます。</strong></td>
<td>この警告は、INF が非推奨のディレクティブを指定することを示します。 ドライバーがインストールされているときに、セクションを参照するディレクティブは評価されません。 たとえば、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547448"> <strong>INF LogConfig ディレクティブ</strong></a>ディレクティブは現在サポートされていません、ため、この警告で、次のセクションの結果します。
<pre>
[InstallSection.LogConfigOverride]
LogConfig=LogConfigSection
...
</pre>
ディレクティブは非推奨する INF の詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547388">INF ディレクティブ</a>します。</td>
</tr>
<tr>
<td><strong>2223:セクションは、アーキテクチャの装飾である必要があります。</strong></td>
<td>この警告は、INF ファイルが含まれていることを示します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547454"> <strong>INF 製造元セクション</strong></a>を指定する、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547456"><strong>モデル セクション</strong></a>なしでアーキテクチャの装飾。 たとえば、次の INF 構文が、警告になります。 2223。
<pre>
[Manufacturer]
%MfgName% = InstallSection

[InstallSection]
...
</pre>
ドライバーをインストールするときに上記の INF 構文の既定値は x86 にです。
<p>代わりに、サポートされているすべてのアーキテクチャを宣言し、各インストールの対応するセクションを指定します。</p>
<pre>
[Manufacturer]
%MfgName% = InstallSection, NTX86, NTAMD64

[InstallSection.NTAMD64]
...

[InstallSection.NTX86]
...
</pre>
INF ファイルでは、x86 の装飾セクションと非装飾のセクションを指定した場合、ドライバーをインストールするときに非装飾のセクションは無視されます。</td>
</tr>
</tbody>
</table>
