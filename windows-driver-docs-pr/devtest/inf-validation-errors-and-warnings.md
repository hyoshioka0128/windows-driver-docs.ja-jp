---
title: INF の検証エラーと警告
description: Microsoft Visual Studio が実行する自動 INF 検証の結果として、ドライバーのインストールエラーと警告が表示されることがあります。
ms.assetid: E021D8F8-BFDA-4F71-B8EA-0997096761FB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d8fd642761e39cf25d6f9c1f56a6888fc6cd1a8
ms.sourcegitcommit: 3794904c6f741bdc407dfe22341080646602f972
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "80807612"
---
# <a name="inf-validation-errors-and-warnings"></a>INF の検証エラーと警告

このトピックでは、Microsoft Visual Studio が実行する自動 INF 検証の結果として、または[InfVerif](infverif.md)ツールを実行したときに表示されるドライバーのインストールエラーと警告について説明します。

INF ファイルの次のエラーは、ドライバーをビルドするときに、WDK 10 では、Visual Studio 2015 以降、エラー一覧 ウィンドウに表示できます。 コマンドラインから InfVerif を実行している場合、ツールは、コマンドプロンプト、または結果の HTML バージョンでこれらのエラーを表示します。

## <a name="error-guidance"></a>エラーのガイダンス

InfVerif は、エラー番号が低いことを示す一般的な規則に従って、問題が深刻になっています。
ほとんどのエラーコードは、InfVerif に指定された引数に応じて、警告またはエラーのいずれかになります。

### <a name="handling-errors"></a>エラーの処理

ハードウェアデベロッパーセンターのダッシュボードでドライバーのテストに合格するには、すべてのエラーを修正する必要があります。 エラーは、次の条件に関連します。

- Inf パーサーは INF を正常に解釈できません
- INF パーサーは、既定値の想定 (あいまいな構文) を作成することによってのみ INF を解釈できます。
- InfVerif の引数は、規則セットを INF (Universal など) に適用する必要があることを示します。

開発センターでドライバーを送信する前に警告を修正する必要はありませんが、報告されている問題を理解するために時間を取ることをお勧めします。 特定の警告を把握していない場合、INF が期待どおりに動作しない可能性があります。

警告は通常、次のものに関連しています。

- 構文が正しくない可能性がありますが、有効なシナリオがあります。
- 指定された InfVerif パラメーターに対して有効な構文ですが、他のモード (Universal など) ではエラーです。

ユニバーサル設定に関連する問題は、次の場合にエラーとして表示されます。

- Visual Studio では、ターゲットプラットフォームを**Universal**または**Mobile**に設定して、ドライバーをビルドします。
- コマンドラインから InfVerif を実行し、/u フラグを指定します。

ユニバーサル設定に関連する問題は、次の場合に警告として表示されます。

- Visual Studio では、ターゲットプラットフォームを**Desktop**に設定してドライバーをビルドします。
- コマンドラインから InfVerif を実行し、/u フラグを指定しないでください。

## <a name="error-codes"></a>エラー コード

エラーコードは次のように分類されます。

- [INF ファイルの構文 (1100-1299)](#syntax-in-the-inf-file-1100-1299)
- [Universal INF (1300-1319)](#universal-inf-1300-1319)
- [インストール (2000-2999)](#installation-2000-2999)

すべてのエラーコードが以下に記載されているわけではありません。これは、自己明らかな意味を持つものです。 1000-1099 の範囲のエラーは、基本的な構文エラーであるため、自己認識型と見なされます。

## <a name="syntax-in-the-inf-file-1100-1299"></a>INF ファイルの構文 (1100-1299)

InfVerif failure はドライバーの送信に失敗することを意味しますが、ドライバーのインストールが引き続き成功する場合があります。
これは、ドライバーをインストールするときに、INF ファイルにエラーがあると、Windows によって設定の既定値も試行されるためです。
この範囲のエラーが原因でドライバーのインストールが失敗することはありませんが、この範囲のエラーは OS バージョンまたは SKU によって動作が変わる可能性があることを示しています。
ドライバーが正常にインストールされた場合、これらのエラー*は*、ドライバーが正常にインストールされない状況があることを示します。

<table>
<thead>
<tr>
<th>エラー コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>1100: DriverStore の Copyfile 名が一致しません</strong></td>
<td>このエラーは、ファイルが元のドライバーストア名と場所から、ドライバーストア内の別の名前と場所にコピーまたは名前が変更された場合に発生します。  次に、例を示します。
<pre>
[SourceDisksFiles]
DriverFile.sys=1,x64  

[DestinationDirs]
CopyFileSection=13,SubDirectory  
  
[CopyFileSection]
DriverFile.sys
</pre>
ドライバーストアは、元のドライバーパッケージのディレクトリ構造を保持します。  上記のコードでは、DriverFile .sys の元の場所は<i>inf location</i>\x64 ですが、CopyFiles ディレクティブは<i>inf</i>の場所 \ subdirectoryに配置します。  コピーの一部としてファイル名を変更した場合も、同じエラーが表示されます。</td>
</tr>
<tr>
<td><strong>1203: セクションが見つかりません</strong></td>
<td>たとえば、次の INF 構文ではエラー1203が発生します。
<pre>
[MyInstallSection]
CopyFiles=driverFile.sys
</pre>
このエラーは、 <strong>CopyFiles</strong>ディレクティブにセクション名 (コピーするファイルの一覧を指定) が必要であるために報告されます。 ただし、 <strong>CopyFiles</strong>ディレクティブではファイル名を指定できます。 セクション名とファイル名を区別するには、次に示すように、ファイル名の先頭に @ トークンを付けます。
<pre>
[MyInstallSection]
CopyFiles=@driverFile.sys
</pre>
</td>
</tr>
<tr>
<td><strong>1204: プロバイダーを Microsoft にすることはできません</strong></td>
<td>[Version] セクションの Provider フィールドで、Microsoft を指定することはできません。
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
<td><strong>1205: セクション [Driver_files] は [Directive1] および [Directive2] ディレクティブから参照されています</td>
<td>この警告は、2つの異なるディレクティブが同じセクションを指している場合に生成されます。
  <p>ほとんどの場合、これは実際にはエラーになりますが、条件がオンになっている場合でも1205が報告されることに注意してください。</td>
</tr>
<tr>
<td><strong>1212: [DefaultInstall] と [Manufacturer] の両方を含めることはできません</strong></td>
<td>1つの INF に [DefaultInstall] と [Manufacturer] の両方を含めることはできません。  両方で作成された Inf では、2つのセクションのいずれかを削除する必要があります。
</td>
</tr>
<tr>
<td><strong>1220: 含まれている INF で定義されているセクションを直接参照できません</strong></td>
<td>INF ファイルがインクルードされた INF の<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section">Ddinstall</a>セクションを参照している場合は、[<strong>要求</strong>] ディレクティブを使用する必要があります。 含まれている INF からセクションを参照するその他のディレクティブでは、エラー1220が発生します。
<p>この例では、.INF の install セクションによって、同等のインストールセクションの B-tree が参照されます。</p>
<p>.INF には次のものが含まれます。</p>
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
<p>B. INF には次のものが含まれます。</p>
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
<p><strong>要求</strong>ディレクティブは、現在のインストールセクションで処理するために、同等のインストールセクションを参照する必要があります。 たとえば、ニーズ ディレクティブ [InstallSectionA.Services] は をポイントする必要があります、します。別のサービスでは、セクションをインストールします。 また、<strong>必要に応じ</strong>てディレクティブを使用して、同じ INF の別の ddinstall セクションの動作を含めることもできます。 その他の種類のセクションで <strong>要求</strong>するディレクティブを使用すると、望ましくない動作が発生する可能性があります。</p></td>
</tr>
<tr>
<td><strong>1221: サービスレジストリを変更できません。 HKR を使用する必要があります</strong></td>
<td>このエラーは、INF ファイルがサービスレジストリキー内の場所を参照していることを示します。たとえば <strong>HKLM\SYSTEM\CurrentControlSet\Services&lt;em&gt;サービス名</em></strong>です。 サービスキーにアクセスする場合は、代わりに相対ルート (<strong>Hkr</strong>) を使用して、レジストリ値をデバイスまたはドライバーインスタンスに関連付ける必要があります。
<p><strong>Hkr</strong>を使用すると、デバイスがインストールされるまでレジストリ値は存在しません。</p></td>
</tr>
<tr>
<td><strong>1230: ファイル ' xxxx ' が [SourceDisksFiles] セクションにありません。</strong></td>
<td>これは、ファイルがドライバーパッケージの一部として指定されているが、INF を基準としたファイルのソースの場所が [SourceDisksFiles] セクションで指定されていないことを示します。
<pre>
[SourceDisksFiles]
filename=disk id
</pre>
このエラーは、[SourceDisksFiles] のアーキテクチャ修飾バージョン ([SourceDisksFiles. amd64] など) が指定されている場合に頻繁に発生しますが、INF でサポートされているすべてのアーキテクチャに [SourceDisksFiles] セクションがあるわけではありません。</td>
</tr>
<tr>
<td><strong>1233: 署名に必要なディレクティブがありません</strong></td>
<td>[バージョン] セクションでは、ドライバーパッケージの署名を受信するために、CatalogFile ディレクティブ (および関連付けられているカタログファイル) を指定する必要があります。
<pre>
CatalogFile=wudf.cat
</pre>
</td>
</tr>
<tr>
<td><strong>1235: 文字列トークンが [文字列] に定義されていません</strong></td>
<td>指定された文字列トークンには、[Strings] セクションに定義がありません。 たとえば、INF ファイルでは、AddReg ディレクティブで指定された<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive"><strong>AddReg</strong></a> <em>セクション</em>に<em>% REG_DWORD%</em>が指定されていますが、対応する REG_DWORD = 0x00010001 は<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section">[文字列]</a>セクションにありません。
<p>このエラーは、INF ファイルで環境変数を含むレジストリ値が指定されている場合に頻繁に発生します。 次に、例を示します。</p>
<pre>
[MyAddReg]
HKR,,DllPath,%SystemRoot%\System32\myDll.sys
</pre>
この行により、INF パーサーは、リテラル "% SystemRoot%" をレジストリに格納するのではなく、[文字列] セクションからトークン "SystemRoot" を見つけようとします。  文字列置換を実行するのではなく、リテラル値% SystemRoot% を使用するには、エスケープシーケンス%% を使用します。
<pre>
[MyAddReg]
HKR,,DllPath,%%SystemRoot%%\System32\myDll.sys
</pre>
</td>
</tr>
<tr>
<td><strong>1285: Microsoft 定義のクラスに [ClassInstall32] セクションを指定できません。</strong></td>
<td>Windows 10 の場合、IHV 提供の Inf では、Microsoft が定義したクラスの INF で [ClassInstall32] を使用することは許可されていません。
</td>
</tr>
<tr>
<td><strong>1296: 指定されたサービスはハードウェアに関連付けられていません</strong></td>
<td>Windows 10 バージョン1809以降では、これが警告からエラーに変わりました。  、.定義されているターゲット OS ごとにサービスセクションが必要です。  これは、1809だけでなく、すべての Inf に適用されます。  

サービスがなく、受信トレイドライバーサービスに依存していたためにこのセクションを含めなかった場合は、の作成が必要になることがあります。要求とインクルードステートメントを使用して、受信トレイ INF のサービスを参照するサービスセクション。  

たとえば、INF ファイルには次のようなものがあります。このエラーを解決するには、各 OS ターゲットのサービスセクション。

<pre>
[XXXXXXXX.Install.NTx86.Services]
Include=filename.inf
Needs=inf-section-name.Services
</pre>

関数ドライバーを必要としないデバイスの場合、NULL ドライバーは次のように指定できます。
<pre>
AddService = ,2
</pre>

<b>これは、INF が非機能デバイスをインストールして、ドライバーを必要としない場合にのみ使用してください。</b>

たとえば、フィルタードライバーのみを必要とし、関数ドライバーではないデバイスには、次の2つの AddService ディレクティブがあります。
<pre>
AddService = MyFilterDriver,, My-Service-Install-Section 
AddService = ,2
</pre>

</td>
</tr>
<tr>
<td><strong>1297: デバイスドライバーはどのデバイスにもインストールされません。これが目的の場合は、プリミティブドライバーを使用してください。</strong></td>
<td>これは、INF ファイルがデバイスドライバであることを示していますが、デバイスドライバとして使用されていません。 これにより、ドライバーストアによるドライバーの処理方法で問題が発生する可能性があります。 意図しない場合は、INF を調べて、ハードウェア Id が正しく指定されていることを確認してください。 ドライバーをデバイスにインストールすることを意図していない場合は、それをプリミティブドライバーに変換します。  詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/develop/creating-a-primitive-driver#converting-from-a-device-driver-inf">デバイスドライバー INF からの変換</a>」を参照してください。
</td>
</tr>
</tbody>
</table>

## <a name="universal-inf-1300-1319"></a>Universal INF (1300-1319)

>[!IMPORTANT]
>ドライバーの INF ファイルは、エラーまたは警告が 13*xx*の範囲でエラー番号と共に表示されない場合に、ユニバーサルです。

次のエラーと警告は、INF のようなものに関連しています。

<table>
<thead>
<tr>
<th>エラー/警告コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>1300: レガシ Xxx が見つかりました</strong><em>Xxx</em></td>
<td>非推奨のセクションや、 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-logconfig-directive"><strong>Logconfig</strong></a>や<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section"><strong>ddinstall</strong></a>などのディレクティブを使用すると、このエラーが表示されます。</td>
</tr>
<tr>
<td><strong>1301: レガシ</strong><em>Xxx</em><strong>操作</strong><em>xxx</em>が見つかりました</td>
<td>非推奨のセクションや、 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-logconfig-directive"><strong>Logconfig</strong></a>や<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section"><strong>ddinstall</strong></a>などのディレクティブを使用すると、このエラーが表示されます。</td>
</tr>
<tr>
<td>1302:<em>xxx</em>の従来の<em>Xxx</em><strong>操作</strong><strong>が見つかりました</strong></td>
<td>このエラーは、サービスの削除やファイルの削除など、操作がドライバーパッケージの外部に影響を与える場合に発生します。</td>
</tr>
<tr>
<td><strong>1303: 共同インストーラーを定義する従来の操作が見つかりました</strong></td>
<td>エラー1303は、AddReg 操作で共同インストーラーが指定されていることを示します。 次に、例を示します。
<pre>
AddReg = HKR,,CoInstallers32,0x00010000,"MyCoinstaller.dll"
</pre>
</td>
</tr>
<tr>
<td><strong>1304: 非相対キーを使用したレガシ操作が見つかりました</strong></td>
<td>エラー1304は、レジストリ操作が HKR 以外のレジストリルートを使用していることを示します。</td>
</tr>
<tr>
<td><strong>1305: 追加可能な複数の sz 値を使用してレガシ操作が見つかりました</strong></td>
<td>エラー1305は、INF が<strong>REG_MULTI_SZ</strong>から値を削除するか、既存の<strong>REG_MULTI_SZ</strong>に値を追加することを示します。</td>
</tr>
<tr>
<td><strong>1306: システムターゲットパス以外のレガシ操作が見つかりました</strong></td>
<td>エラー1306は、% SystemRoot% の下にないターゲットがファイルのコピーによって指定されていることを示します。</td>
</tr>
<tr>
<td><strong>1310-1312: 要求ディレクティブのセクション拡張が正しくありません</strong></td>
<td>ディレクティブは、必要なセクションを参照するセクションに効率的にコピー/貼り付けする必要があります。  ベースライン検証として、InfVerif はセクションの拡張を比較します。  これは、[DDInstall. Services] では、他の [DDInstall. Services] セクションでのみ、必要なディレクティブを使用できることを意味します。</td>
</tr>
<tr>
<td><strong>1313-1314: インクルードディレクティブがありません</strong></td>
<td>要求ディレクティブを使用する各セクションでは、ターゲットセクションを含む INF を参照するために、対応するインクルードディレクティブが必要です。  以前は、Include ディレクティブが別の INF セクションにある場合は、必要なディレクティブが有効になっていました。</td>
</tr>
<tr>
<td><strong>133x: 機能エラー</strong></td>
<td>複数のレジストリセクションが1つのグローバルキーに書き込まれます。 たとえば、異なるサービス構成、グローバルレジストリキーが異なるデータ値に設定されている、または異なるソースファイルを参照している対象ファイルがある場合、各セクションにサービスを設定できます。</td>
</tr>
</tbody>
</table>

## <a name="installation-2000-2999"></a>インストール (2000-2999)

2000-2999 の範囲の問題は、警告として表示されます。 使用できる値は次のとおりです。

<table>
<thead>
<tr>
<th>エラー コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>2083: セクションが参照または使用されていません</strong></td>
<td>この警告は、INF ファイルが参照されていないセクションを提供していることを示します。 ドライバーがインストールされている場合、警告で参照されているセクションの内容は評価されません。</td>
</tr>
<tr>
<td><strong>2222: レガシディレクティブは無視されます。</strong></td>
<td>この警告は、INF が非推奨のディレクティブを指定していることを示します。 ドライバーがインストールされている場合、セクションを参照するディレクティブは評価されません。 たとえば、 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-logconfig-directive"><strong>INF LogConfig ディレクティブ</strong></a>ディレクティブはサポートされなくなったので、次のセクションではこの警告が発生します。
<pre>
[InstallSection.LogConfigOverride]
LogConfig=LogConfigSection
...
</pre>
推奨されない INF ディレクティブの詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-directives">Inf ディレクティブ</a>」を参照してください。</td>
</tr>
<tr>
<td><strong>2223: セクションには、アーキテクチャの装飾が必要です</strong></td>
<td>この警告は、アーキテクチャの装飾のない<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section"><strong>モデルセクション</strong></a>を指定する Inf の<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section"><strong>製造元セクション</strong></a>が inf ファイルに含まれていることを示します。 たとえば、次の INF 構文では、警告2223が発生します。
<pre>
[Manufacturer]
%MfgName% = InstallSection

[InstallSection]
...
</pre>
ドライバーをインストールすると、上記の INF 構文の既定値は x86 になります。
<p>代わりに、サポートされているすべてのアーキテクチャを宣言し、それぞれに対応する install セクションを提供します。</p>
<pre>
[Manufacturer]
%MfgName% = InstallSection, NTX86, NTAMD64

[InstallSection.NTAMD64]
...

[InstallSection.NTX86]
...
</pre>
INF ファイルで、x86 と装飾されていないセクションの装飾されたセクションが指定されている場合、ドライバーをインストールするときに、デコレートされていないセクションは無視されます。</td>
</tr>
</tbody>
</table>
