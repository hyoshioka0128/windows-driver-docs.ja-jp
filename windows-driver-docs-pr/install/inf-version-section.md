---
title: INF Version セクション
description: 規則により、バージョン セクションでは INF ファイルで最初に表示します。 すべての INF ファイルには、このセクションが必要です。
ms.assetid: 53e30950-28a3-4ae3-a351-a917b02c84a5
keywords:
- バージョンの INF セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Version Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca8002a496726dc802953871c560a8f6d6ea69f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325810"
---
# <a name="inf-version-section"></a>INF Version セクション


慣例により、**バージョン**INF ファイルにセクションが最初に表示します。 すべての INF ファイルには、このセクションが必要です。

```ini
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


<a href="" id="signature--signature-name-"></a>**Signature="**<em>signature-name</em>**"**  
必要があります **$Windows NT$** または **$Chicago$** します。 これは、この INF は有効なオペレーティング システムを示します。 これらのシグネチャの値には、次の意味があります。

| 署名の値  | 説明                       |
|------------------|-------------------------------|
| **$Windows NT $** | すべての Windows オペレーティング システム |
| **$Chicago $**    | すべての Windows オペレーティング システム |

 

外側のドル記号文字 ($) が必要ですが、大文字と小文字はこれらの文字列。 場合*signature 名*none は、これらの文字列値のファイルは有効な INF として受け入れられませんが。

一般に、Windows は、これらのシグネチャの値の間では区別されません。 これらのいずれかを指定する必要がありますが、どちらかは関係ありません。 だれかが、INF ファイルの読み取りの対象となるオペレーティング システムを確認できるように、適切な値を指定する必要があります。

一部のクラスのインストーラー署名値を指定する必要がある方法で追加の要件を配置します。 このような要件では、存在する場合は、デバイスの種類に固有のセクションでこの Windows Driver Kit (WDK) ので説明がします。

システム定義の拡張機能を追加することで OS 固有のインストール情報を指定する必要があります、INF、 *DDInstall*のセクションでは、かどうか、 *signature 名*は<strong>$Windows NT$</strong>または **$Chicago$** します。 (を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)これらの拡張機能の詳細についてはします)。

<a href="" id="class-class-name"></a>**クラス =**<em>クラス名</em>  
標準の種類のデバイスの名前を指定します、[デバイス セットアップ クラス](device-setup-classes.md)この INF ファイルを使用してインストールされているデバイスの種類。 この名前は通常のシステム定義のクラスの名前など**Net**または**表示、** にリストされています*Devguid.h*します。 詳細については、次を参照してください。 [System-Supplied デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff553419)します。

INF が指定されている場合、**クラス、** の対応するシステム定義の GUID 値を指定する必要がありますもその**ClassGUID**エントリ。 定義済みのデバイス セットアップ クラスが任意のデバイスの対応する GUID 値を指定することができますデバイスとドライバーのインストールの高速化、INF の検索を最適化するためにシステムのセットアップ コードは、このため。

一意で与える必要がありますが、INF では、システムにデバイスの新しいセットアップ クラスを追加する場合大文字*クラス名*システム提供のクラスのいずれかとは異なる値*Devguid.h*します。 長さ、*クラス名*文字列は 32 文字である必要がありますまたはそれ以下。 新しく生成された GUID 値を指定する必要があります、INF、 **ClassGUID**エントリ。 参照してください[ **INF ClassInstall32 セクション**](inf-classinstall32-section.md)します。

このエントリは、INF、定義済みのデバイス セットアップ クラスの下に新しいデバイス ドライバも、新しいデバイス セットアップ クラスをインストールするには関係ありません。

**注**  このエントリは、プラグ アンド プレイ (PnP) マネージャーを通じてインストールされているデバイス ドライバーに必要です。

 

<a href="" id="classguid--nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn-"></a>**ClassGuid={**<em>nnnnnnnn</em>**-***nnnn***-***nnnn***-***nnnn***-**<em>nnnnnnnnnnnn</em>**}**  
指定します、[デバイス セットアップ クラス](device-setup-classes.md)GUID。 GUID 値は、ここで、書式設定された各*n*は 16 進数。

この GUID 値は、レジストリのデバイス セットアップ クラスのサブキーを指定 **.\\クラス**この INF ファイルからインストールされているデバイスのドライバーのレジストリ情報の書き込み先の下のツリーです。 このクラスに固有の GUID 値は、存在する場合にもデバイスおよびクラスに固有のプロパティ ページのプロバイダーの種類のデバイス クラスのインストーラーを識別します。

新しい[デバイス セットアップ クラス](device-setup-classes.md)、INF を新しく生成されたに指定する必要があります**ClassGUID**値。 Guid を作成する方法の詳細については、次を参照してください。[ドライバーを使用して Guid](https://msdn.microsoft.com/library/windows/hardware/ff565392)します。 デバイス セットアップ クラスを参照してください。

**注**  このエントリは、デバイス ドライバー、PnP マネージャーでインストールされたために必要です。

**ExtensionId**拡張子 INF を作成するときに {xxxxxxxx xxxx-xxxx-。} を指定します、拡張機能 ID の GUID を = です。 GUID 値は、ここで、書式設定された各*x*は 16 進数。

INF 拡張子の最初のバージョンを作成するときに、INF を新しく生成された指定する必要があります**ExtensionId**値。 ただし、INF、既存の拡張機能を更新するときに、 **ExtensionId**拡張子 INF の関連する複数のバージョンは独立した拡張子 Inf として扱われるのではなくどうしバージョン管理されるように、同じままする必要があります同じデバイス インスタンスで同時にインストールすることがあります。 拡張子 Inf を作成する方法の詳細については、次を参照してください。[拡張子 INF ファイルを使用して](using-an-extension-inf-file.md)します。

**注**のみこのエントリは、INF、拡張機能を作成するときに指定することによって識別される必要な`Class = Extension`と`ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}`します。
 

<a href="" id="provider--inf-creator-"></a>**Provider=%**<em>INF-creator</em>**%**  
INF ファイルのプロバイダーを識別します。 通常、として指定されて、 **%** <em>OrganizationName</em> **%** INF ファイルの後で展開されるトークン[**文字列**](inf-strings-section.md)セクション。 プロバイダー名の文字の最大長は、LINE_LEN です。

たとえば、通常のシステムで提供される INF ファイルの指定、 *INF 作成者*として<strong>%</strong>Msft<strong>%</strong>定義と<strong>%</strong> Msft<strong>% ="</strong>Microsoft<strong>"</strong>でその[**文字列**](inf-strings-section.md)セクション。

**注**  このエントリは、デバイス ドライバー、PnP マネージャーでインストールされたために必要です。

 



<a href="" id="catalogfile-filename-cat"></a>**CatalogFile=**<em>filename</em>**.cat**  
カタログを指定します (.*cat*) デバイス/ドライバーの配布メディアに含まれるファイル。

ときに、[ドライバー パッケージ](driver-packages.md)が Microsoft に提出では、デジタル署名 WHQL を提供します、[カタログ ファイル](catalog-files.md)ドライバー パッケージをテストし、パッケージにデジタル署名を割り当て、WHQL 後。 テストおよび IHV および OEM のドライバー パッケージの署名の詳細については、次を参照してください。 [WHQL リリース署名](whql-release-signature.md)します。 カタログ ファイルは表示されていない、 [ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)セクションまたは[ **CopyFiles** ](inf-copyfiles-directive.md) INF のディレクティブ。 Windows では、INF ファイルと同じ場所に、カタログ ファイルが前提としています。

システム提供の INF ファイルがあることはありません**CatalogFile =** エントリ、オペレーティング システムに対して、このような INF の署名を検証するため、すべてシステム提供*xxx.cat*ファイル。

<a href="" id="catalogfile-nt-unique-filename-cat--"></a>**CatalogFile.nt=**<em>unique-filename</em>**.cat** |  

<a href="" id="catalogfile-ntx86-unique-filename-cat--"></a>**CatalogFile.ntx86=**<em>unique-filename</em>**.cat** |  

<a href="" id="catalogfile-ntia64-unique-filename-cat--"></a>**CatalogFile.ntia64=**<em>unique-filename</em>**.cat** |  

<a href="" id="catalogfile-ntamd64-unique-filename-cat"></a>**CatalogFile.ntamd64=**<em>unique-filename</em>**.cat**  

<a href="" id="catalogfile-ntarm-unique-filename-cat"></a>**CatalogFile.ntarm=**<em>unique-filename</em>**.cat**  

<a href="" id="catalogfile-ntarm64-unique-filename-cat"></a>**CatalogFile.ntarm64=**<em>unique-filename</em>**.cat**  


もう 1 つの INF ライター決定、一意のファイル名を指定します。*cat*カタログ ファイルの拡張子。 これらの省略可能なエントリを省略すると、指定された**CatalogFile =**<em>filename.cat</em> WDM デバイス/ドライバーのインストールの検証に使用されます。

修飾されて存在する場合**CatalogFile *。xxx* =** で INF のエントリが存在する**バージョン**と共に、装飾されていないセクション**CatalogFile =** エントリ、装飾されていないエントリと見なされます識別、 *filename.cat*デバイスのインストール、ドライバーのインストール、またはその装飾のエントリが指定されていないこれらのプラットフォームの両方を検証するためです。

クロス プラットフォームのデバイス ドライバーの INF ファイルを持つ**CatalogFile =** と**CatalogFile** 。<em>xxx</em> **=** エントリは、一意の各 .cat ファイル IHV と OEM により決定された名前を指定する必要があります。

詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

**注**  このエントリの使用がいない必須または推奨同じ .cat ファイルは、サポートされているすべてのプラットフォームで使用できる、ためです。 ただし、ドライバー パッケージのプラットフォームに固有の .cat ファイルを作成する場合は、このエントリを使用する必要があります。

 

<a href="" id="driverver-mm-dd-yyyy--w-x-y-z-"></a>**DriverVer =** **/mm/dd/yyyy**、**w.x.y.z**  
このエントリには、この INF ファイルによってインストールされているドライバーのバージョン情報を指定します。 Windows 2000 以降、このエントリが必要です。

このエントリを指定する方法については、次を参照してください。 [ **INF DriverVer ディレクティブ**](inf-driverver-directive.md)します。


<a href="" id="pnplockdown-0-1"></a>**PnpLockDown=0**|**1**  
プラグ アンド プレイ (PnP) がアプリケーションから直接、ファイルの変更を防止するかどうかを指定する、[ドライバー パッケージの](driver-packages.md)INF ファイルを指定します。 場合、 **PnpLockDown**ディレクティブが 1 に設定されている、PnP にアプリケーションが INF によってコピーされるファイルを直接変更するを防ぐ**CopyFiles**ディレクティブ。 それ以外の場合、INF ファイルでディレクティブが含まれていない、またはディレクティブの値が 0 に設定されて、管理者特権を持つアプリケーションを直接変更できますこれらのファイル。 この方法で保護されているドライバー ファイルと呼びます*サード パーティ製のドライバー ファイルを保護する*します。

PnP ドライバーのインストールの整合性を確保するには、アプリケーションが直接変更ドライバー パッケージの INF ファイルでは、コピーされるドライバー ファイル。 アプリケーションでは、PnP ドライバーを更新するのにのみ Windows によって提供されるデバイスのインストール メカニズムを使用する必要があります。

Windows Vista 以降、ドライバー パッケージを設定する必要があります**PnpLockDown**アプリケーション、ドライバー ファイルを直接変更しないようにするには 1 です。 ただし、ドライバー パッケージをアンインストールするいくつかの既存のアプリケーションは、ドライバー ファイルを直接削除しないでください。 これらのアプリケーションとの互換性を維持するために、 **PnpLockDown**このようなドライバー パッケージのディレクティブは 0 に設定する必要があります。

**注**  PnP Windows Vista および Windows の以降のバージョンでは必要ありませんが、INF ファイルが含まれている、 **PnpLockDown**ディレクティブのドライバーをインストールするためには、将来の PnP Windows 版の可能性がありますINF ファイルが必要な PnP[ドライバー パッケージ](driver-packages.md)含める、 **PnpLockDown**ディレクティブ。

 

<a href="" id="driverpackagedisplayname--driver-package-description-"></a><strong>DriverPackageDisplayName=%</strong>driver-package-description<strong>%</strong>  
使用しないでください。 Driver Install Frameworks (DIFx) によって使用されていた。 DIFx 廃止については、次を参照してください。 [DIFx ガイドライン](difx-guidelines.md)します。

<a href="" id="driverpackagetype-packagetype"></a>**DriverPackageType=** *PackageType*  
使用しないでください。 Driver Install Frameworks (DIFx) によって使用されていた。 DIFx 廃止については、次を参照してください。 [DIFx ガイドライン](difx-guidelines.md)します。

<a name="remarks"></a>コメント
-------

ときに、[ドライバー パッケージ](driver-packages.md)渡します Microsoft Windows Hardware Quality Lab (WHQL) テスト、WHQL 返します *.cat* IHV および OEM にファイルをカタログします。 各 *.cat*ファイルには、ドライバー パッケージの暗号化されたデジタル署名が含まれています。 IHV および OEM はこれらでリストする必要があります *.cat* 、INF ファイル**バージョン**セクションし、INF ファイルと同じ場所に、配布メディア上のファイルを指定する必要があります。 *.Cat*ファイルは圧縮である必要があります。

**注**  場合は、INF**バージョン**セクションは少なくとも 1 つは含まれません**CatalogFile**または **CatalogFile.nt***xxx*エントリ、ドライバーは、として扱われます、署名されていないと、日付、 [ **DriverVer** ](inf-driverver-directive.md)ディレクティブは、Windows では表示されません。

 

詳細については、次を参照してください。[ドライバーの署名](signing-drivers-for-public-release--windows-vista-and-later-.md)します。

<a name="examples"></a>使用例
--------

次の例は、**バージョン**単純なデバイス ドライバー、必要な続けて INF の一般的なセクション[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)と[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)セクションではこのサンプルで指定されたエントリが含まれる**バージョン**セクション。

```ini
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

 

 






