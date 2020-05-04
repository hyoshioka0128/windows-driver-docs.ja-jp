---
title: INF Version セクション
description: 慣例として、[バージョン] セクションは INF ファイルに最初に表示されます。 すべての INF ファイルにこのセクションが必要です。
ms.assetid: 53e30950-28a3-4ae3-a351-a917b02c84a5
keywords:
- INF バージョンセクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Version Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e5956126ab226f00f3c6108e5520960f02b40dc
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223094"
---
# <a name="inf-version-section"></a>INF Version セクション


慣例として、[**バージョン**] セクションは INF ファイルに最初に表示されます。 すべての INF ファイルにこのセクションが必要です。

```inf
[Version]
 
Signature="signature-name"
[Class=class-name]
[ClassGuid={nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}]
[Provider=%INF-creator%]
[ExtensionId={xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}]
[LayoutFile=filename.inf [,filename.inf]... ]  (Windows 2000 and Windows XP)
[CatalogFile=filename.cat]
[CatalogFile.nt=unique-filename.cat]
[CatalogFile.ntx86=unique-filename.cat]
[CatalogFile.ntia64=unique-filename.cat]  (Windows XP and later versions of Windows)
[CatalogFile.ntamd64=unique-filename.cat]  (Windows XP and later versions of Windows)
[CatalogFile.ntarm=unique-filename.cat]  (Windows 8 and later versions of Windows)
[CatalogFile.ntarm64=unique-filename.cat]  (Windows XP and later versions of Windows)

DriverVer=mm/dd/yyyy,w.x.y.z
[PnpLockDown=0|1] (Windows Vista and later versions of Windows)
[DriverPackageDisplayName=%driver-package-description%]
[DriverPackageType=PackageType]
```

## <a name="entries"></a>エントリ


<a href="" id="signature--signature-name-"></a>**Signature = "**<em>signature-name</em>**"**  
**$WINDOWS NT $** または **$Chicago $** である必要があります。 これは、この INF が有効なオペレーティングシステムを示します。 これらの署名値の意味は次のとおりです。

| シグネチャの値  | 意味                       |
|------------------|-------------------------------|
| **$Windows NT $** | すべての Windows オペレーティングシステム |
| **$Chicago $**    | すべての Windows オペレーティングシステム |

 

外側のドル記号 ($) が必要ですが、これらの文字列では大文字と小文字が区別されません。 *署名名*がこれらの文字列値のいずれでもない場合、ファイルは有効な INF として受け入れられません。

一般に、Windows では、これらの署名値を区別しません。 これらのいずれかを指定する必要がありますが、どちらを指定するかは関係ありません。 INF ファイルを読み取っているユーザーが目的のオペレーティングシステムを特定できるように、適切な値を指定する必要があります。

クラスインストーラーによっては、署名値の指定方法に関する追加要件があります。 このような要件が存在する場合は、この Windows Driver Kit (WDK) のデバイスの種類に固有のセクションで説明されています。

INF は、 *Ddinstall*セクションにシステム定義の拡張機能を追加することによって os 固有のインストール情報を提供する必要があります。これには、*署名名*が<strong>NT $</strong>または **$Chicago $**$Windows ます。 (これらの拡張機能の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください)。

<a href="" id="class-class-name"></a>**Class =**<em>クラス名</em>  
任意の標準タイプのデバイスについて、この INF ファイルを使用してインストールされるデバイスの種類の[デバイスセットアップクラス](device-setup-classes.md)の名前を指定します。 この名前は、通常、 *Devguid. h*に記載されている、 **Net**や**Display**などのシステム定義のクラス名の1つです。 詳細については、「[システムによって提供されるデバイスセットアップクラス](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))」を参照してください。

INF でクラスが指定されている場合は **、** その**classguid**エントリに対応するシステム定義の guid 値も指定する必要があります。 定義済みのデバイスセットアップクラスのデバイスに一致する GUID 値を指定すると、システムセットアップコードが INF 検索を最適化するのに役立つため、デバイスとそのドライバーをより速くインストールできます。

INF がデバイスの新しいセットアップクラスをシステムに追加する場合、システムによって提供されるクラスとは異なる、大文字と小文字を区別しない一意の*クラス名*の値を指定する必要があります *。* *クラス名*文字列の長さは32文字以下でなければなりません。 INF では、 **classguid**エントリに対して新たに生成された guid 値を指定する必要があります。 「 [**INF ClassInstall32」**](inf-classinstall32-section.md)も参照してください。

このエントリは、定義済みのデバイスセットアップクラスまたは新しいデバイスセットアップクラスの下に新しいデバイスドライバーをインストールしない INF には関係ありません。

**注**  このエントリは、プラグアンドプレイ (PnP) マネージャーを使用してインストールされるデバイスドライバーに必要です。

 

<a href="" id="classguid--nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn-"></a>**Classguid = {**<em>nnnnnnnn</em>**-***nnnn***--***nnnn******nnnn***nnnn-**<em>nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn</em>**}**  
[デバイスセットアップクラス](device-setup-classes.md)GUID を指定します。 GUID 値は、ここに示すように書式設定されます。各*n*は16進数字です。

この GUID 値は、レジストリ内のデバイスセットアップクラスサブキーを指定します.. **.\\**この INF ファイルからインストールされたデバイスのドライバーのレジストリ情報の書き込みに使用するクラスツリー。 また、このクラス固有の GUID 値は、デバイスの種類およびクラス固有のプロパティページプロバイダー (存在する場合) のデバイスクラスインストーラーも識別します。

新しい[デバイスセットアップクラス](device-setup-classes.md)の場合、INF は新しく生成された**classguid**値を指定する必要があります。 Guid を作成する方法の詳細については、「 [Using guid In Drivers](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-guids-in-drivers)」を参照してください。 「デバイスセットアップクラス」も参照してください。

**注**  このエントリは、PnP マネージャーを介してインストールされるデバイスドライバーに必要です。

**Extensionid**= {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx} 拡張機能の INF を作成するときに、拡張機能 ID の GUID を指定します。 GUID 値は、ここに示すように書式設定されます。各*x*は16進数字です。

拡張機能 INF の初期バージョンを作成する場合、INF は新しく生成された**Extensionid**値を指定する必要があります。 ただし、既存の拡張機能の INF を更新する場合、 **Extensionid**は同じままにしておく必要があります。これにより、同じデバイスインスタンスに同時にインストールされる可能性がある独立した拡張機能の inf として扱われるのではなく、拡張機能 inf の複数の関連バージョンが相互にバージョン管理されます。 拡張機能の inf を作成する方法の詳細については、「[拡張機能の Inf ファイルの使用](using-an-extension-inf-file.md)」を参照してください。

**メモ** このエントリは、および`Class = Extension` `ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}`を指定することによって識別される拡張機能 INF を作成する場合にのみ必要です。

**Classver =**<em>major</em>**。**<em>マイナー</em>

プリンターなどのデバイスクラスによって明示的に要求されない限り、システム使用のために予約されています。 たとえば、「 [V4 DRIVER INF](../print/v4-driver-inf.md)」を参照してください。


<a href="" id="provider--inf-creator-"></a>**プロバイダー =%**<em>INF-作成者</em>**%**  
INF ファイルのプロバイダーを識別します。 通常、これは、後で**%** INF ファイルの[**文字列**](inf-strings-section.md)セクションで拡張される<em>OrganizationName</em> **%** トークンとして指定されます。 プロバイダー名の最大文字数は LINE_LEN です。

たとえば、システムに用意されている INF ファイルでは、通常、 <strong>%</strong> *inf クリエーター*を<strong>%</strong>msft<strong>%</strong>と指定し、[**文字列**](inf-strings-section.md)セクションに msft<strong>% = "</strong>Microsoft<strong>"</strong>を定義しています。

**注**  このエントリは、PnP マネージャーを介してインストールされるデバイスドライバーに必要です。

 



<a href="" id="catalogfile-filename-cat"></a>**Catalogfile =**<em>ファイル名</em>**. cat**  
カタログ () を指定します。*cat*) デバイス/ドライバの配布メディアに含まれるファイル。

[ドライバーパッケージ](driver-packages.md)がデジタル署名のために Microsoft に送信されると、whql によってパッケージにデジタル署名がテストおよび割り当てられた後、ドライバーパッケージの[カタログファイル](catalog-files.md)が提供されます。 IHV または OEM ドライバーパッケージのテストと署名の詳細については、「 [WHQL リリース署名](whql-release-signature.md)」を参照してください。 カタログファイルは、INF の[**Sourcedisksfiles**](inf-sourcedisksfiles-section.md)セクションまたは[**CopyFiles**](inf-copyfiles-directive.md)ディレクティブには記載されていません。 Windows では、カタログファイルが INF ファイルと同じ場所にあることを前提としています。

システムが提供する INF ファイルには、 **Catalogfile =** エントリがありません。これは、オペレーティングシステムが、システムによって提供されるすべての*xxx.cat*ファイルに対して、そのような inf の署名を検証するためです。

<a href="" id="catalogfile-nt-unique-filename-cat--"></a>**Catalogfile. nt =**<em>一意-filename</em>**. cat** |  

<a href="" id="catalogfile-ntx86-unique-filename-cat--"></a>**Ntx86 =**<em>一意-filename</em>**. cat** |  

<a href="" id="catalogfile-ntia64-unique-filename-cat--"></a>**Ntia64 =**<em>一意-filename</em>**. cat** |  

<a href="" id="catalogfile-ntamd64-unique-filename-cat"></a>**Ntamd64 =**<em>一意-filename</em>**. cat**  

<a href="" id="catalogfile-ntarm-unique-filename-cat"></a>**Catalogfile. ntarm =**<em>一意-filename</em>**. cat**  

<a href="" id="catalogfile-ntarm64-unique-filename-cat"></a>**Ntarm64 =**<em>一意-filename</em>**. cat**  


と共に、別の INF ライターによって決定された一意のファイル名を指定します。カタログファイルの*cat*拡張。 これらの省略可能なエントリを省略した場合、WDM デバイス/ドライバーのインストールを検証するために、指定された**Catalogfile =**<em>filename.cat</em>が使用されます。

修飾された Catalogfile の場合は **。*xxx*xxx= **エントリが、装飾の**バージョン**セクションに装飾されていない**catalogfile =** エントリと共に存在する場合、非装飾エントリは、デバイスのインストール、ドライバーのインストール、またはその両方を、装飾エントリが指定されていないプラットフォーム上で検証するための*filename.cat*を識別することを前提としています。

**Catalogfile =** および**catalogfile**を持つクロスプラットフォームデバイスドライバーの INF ファイル。<em>xxx</em> **=** エントリは、このような cat ファイルごとに一意の IHV/OEM によって決定された名前を指定する必要があります。

システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

**注**  同じ .cat ファイルを、サポートされているすべてのプラットフォームで使用できるため、このエントリの使用は必須でも推奨されません。 ただし、ドライバーパッケージ用のプラットフォーム固有の .cat ファイルを作成する場合は、このエントリを使用する必要があります。

 

<a href="" id="driverver-mm-dd-yyyy--w-x-y-z-"></a>**DriverVer =** **mm/dd/yyyy**,**w. x-y. z**  
このエントリは、この INF ファイルによってインストールされるドライバーのバージョン情報を指定します。 Windows 2000 以降では、このエントリは必須です。

このエントリを指定する方法の詳細については、「 [**INF DriverVer ディレクティブ**](inf-driverver-directive.md)」を参照してください。


<a href="" id="pnplockdown-0-1"></a>**PnpLockDown = 0**|**1**  
プラグアンドプレイ (PnP) で、[ドライバーパッケージの](driver-packages.md)INF ファイルによって指定されたファイルをアプリケーションが直接変更できないようにするかどうかを指定します。 **PnpLockDown**ディレクティブが1に設定されている場合、PnP では、アプリケーションが INF の**CopyFiles**ディレクティブでコピーされたファイルを直接変更できないようにします。 それ以外の場合、ディレクティブが INF ファイルに含まれていないか、ディレクティブの値がゼロに設定されていると、管理者特権を持つアプリケーションは、これらのファイルを直接変更できます。 このように保護されているドライバーファイルは、*サードパーティによって保護*されているドライバーファイルと呼ばれます。

PnP ドライバーのインストールの整合性を確保するために、アプリケーションでは、ドライバーパッケージの INF ファイルによってコピーされるドライバーファイルを直接変更しないようにする必要があります。 アプリケーションでは、PnP ドライバーを更新するために Windows によって提供されるデバイスのインストールメカニズムのみを使用する必要があります。

Windows Vista 以降では、ドライバーパッケージで**PnpLockDown**を1に設定して、アプリケーションがドライバーファイルを直接変更できないようにする必要があります。 ただし、ドライバーパッケージをアンインストールする既存のアプリケーションによっては、ドライバーファイルが直接削除される場合があります。 これらのアプリケーションとの互換性を維持するには、このようなドライバーパッケージの**PnpLockDown**ディレクティブを0に設定する必要があります。

**注**  windows Vista 以降のバージョンの windows では、ドライバーをインストールするために inf ファイルに**PnpLockDown**ディレクティブが含まれている必要はありませんが、今後のバージョンの windows では、pnp[ドライバーパッケージ](driver-packages.md)の inf ファイルに**PnpLockDown**ディレクティブが含まれていることが必要になる場合があります。

 

<a href="" id="driverpackagedisplayname--driver-package-description-"></a><strong>Driverpackagedisplayname =%</strong>driver-description<strong>%</strong>  
非推奨になりました。 以前はドライバーインストールフレームワーク (DIFx) によって使用されていました。 DIFx の廃止の詳細については、「 [Difx のガイドライン](difx-guidelines.md)」を参照してください。

<a href="" id="driverpackagetype-packagetype"></a>**Driverpackagetype =** *packagetype*  
非推奨になりました。 以前はドライバーインストールフレームワーク (DIFx) によって使用されていました。 DIFx の廃止の詳細については、「 [Difx のガイドライン](difx-guidelines.md)」を参照してください。

<a name="remarks"></a>解説
-------

[ドライバーパッケージ](driver-packages.md)が Microsoft Windows Hardware Quality LAB (WHQL) テストに合格すると、whql は .cat カタログファイルを IHV または OEM に返し*ます*。 各 *.cat*ファイルには、ドライバーパッケージのデジタル暗号化された署名が含まれています。 IHV または OEM は、これらの *.cat*ファイルを inf**バージョン**セクションに一覧表示し、配布メディアのファイルを inf ファイルと同じ場所に指定する必要があります。 *.Cat*ファイルは圧縮されていない必要があります。

**注:**    INF**バージョン**セクションに少なくとも1つの**catalogfile**または **catalogfile. nt * * * xxx*エントリが含まれていない場合、ドライバーは未署名として扱われ、 [**DriverVer**](inf-driverver-directive.md)ディレクティブに記載されている日付は Windows によって表示されません。

 

詳細については、「[ドライバーの署名](signing-drivers-for-public-release--windows-vista-and-later-.md)」を参照してください。

<a name="examples"></a>例
--------

次の例は、単純なデバイスドライバー INF の一般的な**バージョン**セクションを示しています。その後、このサンプル**バージョン**セクションで指定されているエントリによって暗黙的に指定される必要な[**Sourcedisksnames**](inf-sourcedisksnames-section.md)セクションと[**sourcedisksnames**](inf-sourcedisksfiles-section.md)セクションを示します。

```inf
[Version]
Signature="$Windows NT$"
Class=SCSIAdapter
ClassGUID={4D36E97B-E325-11CE-BFC1-08002BE10318}
Provider=%INF_Provider%
CatalogFile=aha154_ntx86.cat
DriverVer=01/29/2010

[SourceDisksNames]
;
; diskid = description[, [tagfile] [, <unused>, subdir]]
;
1 = %Floppy_Description%,,,\WinNT

[SourceDisksFiles.x86]
;
; filename_on_source = diskID[, [subdir][, size]]
;
aha154x.sys = 1,\x86

; ...

[Strings]
INF_Provider="Adaptec"
Floppy_Description = "Adaptec Drivers Disk"
; ...
```

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**文字列**](inf-strings-section.md)

 

 






