---
title: INF ClassInstall32 セクション
description: ClassInstall32 セクションは、新しいクラスでのデバイス向けの新しいデバイス セットアップ クラス (と可能性があるクラスのインストーラー) をインストールします。
ms.assetid: c1da44ca-3b99-43de-99ef-56fbe67b46c2
keywords:
- INF ClassInstall32 セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF ClassInstall32 Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 925d0a6d34f0d073bfc04b4dba361fd9f24cfbcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325287"
---
# <a name="inf-classinstall32-section"></a>INF ClassInstall32 セクション


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このセクションが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **ClassInstall32**セクションは、新しいインストール[デバイス セットアップ クラス](device-setup-classes.md)(およびクラスのインストーラー可能性があります)、新しいクラスでのデバイス向けです。

```ini
[ClassInstall32] | 
[ClassInstall32.nt] | 
[ClassInstall32.ntx86] |
[ClassInstall32.ntarm] | (Windows 8 and later versions of Windows) 
[ClassInstall32.ntarm64] | (Windows 10 version 1709 and later versions of Windows) 
[ClassInstall32.ntia64] | (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64] (Windows XP and later versions of Windows)

AddReg=add-registry-section[,add-registry-section]...
[AddProperty=add-property-section[,add-property-section] ...]  (Windows Vista and later versions of Windows)
[Copyfiles=@filename | file-list-section[,file-list-section]...]
[DelReg=del-registry-section[,del-registry-section]...]
[DelProperty=del-property-section[,del-property-section] ...]  (Windows Vista and later versions of Windows)
[Delfiles=file-listsection[,file-list-section]...]
[Renfiles=file-list-section[,file-list-section]...]
[BitReg=bit-registry-section[,bit-registry-section]...]
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
```

## <a name="entries"></a>エントリ


<a href="" id="addreg-add-registry-section--add-registry-section-----"></a>**AddReg=**<em>add</em>-*registry*-*section*\[**,**<em>add</em>-*registry*-*section*\] ...  
レジストリに書き込まれるエントリをクラスに固有の値が含まれる 1 つまたは複数の名前付きセクションを参照します。 通常、これは新しいデバイス セットアップ クラスが、他のコンポーネントが後で、レジストリから取得し、使用して、任意のデバイス クラスの新しいインストーラーやプロパティ ページに「インストール」するこの新しいデバイス クラスのインストールされているデバイスを開く、には少なくとも、フレンドリ名を指定に使用されます。このデバイス セットアップ クラス、やなどのためのプロバイダー。

**HKR**いずれかで仕様*追加レジストリ セクション*指定、 **.クラス\\{**<em>SetupClassGUID</em>**}** レジストリ キー。 詳細については、次を参照してください。**解説**セクション。

詳細については、次を参照してください。 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)します。

<a href="" id="addproperty-add-property-section--add-property-section-----"></a>**AddProperty=**<em>add-property-section</em>\[**,**<em>add-property-section</em>\] ...  
(Windows Vista および Windows の以降のバージョン)変更を 1 つまたは複数の INF ファイルでセクションを参照して[デバイス プロパティ](device-properties.md)用に設定されている、[デバイス セットアップ クラス](device-setup-classes.md)します。 使用する必要があります、 [ **INF AddProperty ディレクティブ**](inf-addproperty-directive.md) Windows Vista またはそれ以降のバージョンの Windows オペレーティング システムを新たに導入されたデバイス セットアップ クラスのプロパティを設定するだけです。

デバイス クラス プロパティの以前 Windows Server 2003、Windows XP、または Windows 2000 で導入された、対応するレジストリ エントリの値がある場合を使用する続行する必要があります[ **INF AddReg ディレクティブ**](inf-addreg-directive.md)デバイス セットアップ クラスのプロパティを設定します。 システム定義プロパティとカスタム プロパティに次のガイドラインが適用されます。

使用する方法についての詳細、 **AddProperty**ディレクティブを参照してください[INF AddProperty ディレクティブと INF DelProperty ディレクティブを使用して](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)します。

<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**Copyfiles=@**<em>filename</em> | *file*-*list*-*section*\[**,**<em>file</em>-*list*-*section*\] ...  
先のソース メディアからコピーされる 1 つの名前付きファイルを指定します。 または、変換先に転送するため、元のメディアのクラスに関連するファイルを指定する 1 つまたは複数の名前付きセクションを参照します。 **DefaultDestDir**内のエントリ、 [ **DestinationDirs** ](inf-destinationdirs-section.md) INF のセクションがコピーされる 1 つのクラスに固有ファイルの保存先ディレクトリを指定します。

詳細については、次を参照してください。 [ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)します。

**注**  デバイス セットアップ クラス (およびクラスのインストーラー) 用のシステム提供の INF ファイルには、このセクションでこのディレクティブは使用しないでください。

 

<a href="" id="delreg-del-registry-section--del-registry-section-----"></a>**DelReg=**<em>del</em>-*registry*-*section*\[**,**<em>del</em>-*registry*-*section*\] ...  
どちらの値では、クラスのインストーラーのインストール中に、レジストリから削除するエントリまたはキーを指定します。 1 つまたは複数の名前付きセクションを参照します。

ただし、特定 **{**<em>SetupClassGUID</em>**}** レジストリのサブキーが存在する **.クラス**ブランチ、システムのセットアップ コードは、その後は無視されます、 **ClassInstall32**で同じ GUID 値を指定する任意の INF のセクションでその**バージョン**セクション。 その結果、INF を既存のクラスのインストーラーを置換またはからその動作を変更ことはできません、 **ClassInstall32**セクション。 既存のクラスのインストーラーの動作を変更するには、クラス固有の共同インストーラーを使用します。

詳細については、次を参照してください。 [ **INF してディレクティブ**](inf-delreg-directive.md)します。

<a href="" id="delproperty-del-property-section--del-property-section-----"></a>**DelProperty=**<em>del-property-section</em>\[**,**<em>del-property-section</em>\] ...  
(Windows Vista および Windows の以降のバージョン)削除する 1 つまたは複数の INF ファイルでセクションを参照して[デバイス プロパティ](device-properties.md)用に設定されている、[デバイス セットアップ クラス](device-setup-classes.md)します。 使用する必要があります、 [ **INF DelProperty ディレクティブ**](inf-delproperty-directive.md)のみを Windows Vista またはそれ以降のバージョンの Windows オペレーティング システムを新たに導入されたデバイス セットアップ クラスのプロパティを削除します。

デバイス クラス プロパティの以前 Windows Server 2003、Windows XP、または Windows 2000 で導入された、対応するレジストリ エントリの値がある場合を使用する続行する必要があります[ **INF してディレクティブ**](inf-delreg-directive.md)デバイス セットアップ クラスのプロパティを削除します。 システム定義プロパティとカスタム プロパティに次のガイドラインが適用されます。

使用する方法についての詳細、 **DelProperty**ディレクティブを参照してください[INF AddProperty ディレクティブと INF DelProperty ディレクティブを使用して](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)します。

<a href="" id="delfiles-file-listsection--file-list-section-----"></a>**Delfiles =**<em>ファイル listsection</em>\[**、**<em>ファイル</em>-*一覧*-*セクション*\] .  
削除対象を 1 つまたは複数の名前付きセクションがインストールされていた移行先のクラスに関連するファイルの参照が指定されます。

詳細については、次を参照してください。 [ **INF DelFiles ディレクティブ**](inf-delfiles-directive.md)します。

<a href="" id="renfiles-file-list-section--file-list-section-----"></a>**Renfiles =**<em>ファイルのセクション一覧</em>\[**、**<em>ファイル</em>-*一覧*-*セクション*\] .  
参照先の名前を変更するクラスに関連するファイルの 1 つまたは複数の名前付きセクションの一覧が表示されます。

詳細については、次を参照してください。 [ **INF RenFiles ディレクティブ**](inf-renfiles-directive.md)します。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg =**<em>ビットのレジストリ セクション</em>\[**、**<em>ビットのレジストリ セクション</em>\].  
このセクションでは有効ですが、ほとんどない使用されます。

詳細については、次を参照してください。 [ **INF BitReg ディレクティブ**](inf-bitreg-directive.md)します。

<a href="" id="updateinis-update-ini-section--update-ini-section------"></a>**UpdateInis**=*update-section ini\[、update-section ini\]*.   
このセクションでは有効ですが、ほとんどない使用されます。

詳細については、次を参照してください。 [ **INF UpdateInis ディレクティブ**](inf-updateinis-directive.md)します。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>update-section inifields</em>\[**、**<em>update-section inifields</em>\].  
このセクションでは有効ですが、ほとんどない使用されます。

詳細については、次を参照してください。 [ **INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)します。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>セクション レジストリ ini</em>\[**、**<em>セクション レジストリ ini</em>\].  
このセクションでは有効ですが、ほとんどない使用されます。

詳細については、次を参照してください。 [ **INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)します。

<a name="remarks"></a>注釈
-------

含める必要があります、 **ClassInstall32**新しいカスタム デバイス セットアップ クラスをインストールにのみデバイス INF ファイルのセクション。 インストールされているクラスで、デバイスの INF ファイルかどうかを[システム提供のデバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff553419)またはカスタムのクラスを含めないでください、 **ClassInstall32**セクション。 システムが処理されるため、 **ClassInstall32**セクションだけで、クラスが既にインストールされていない場合は使用できません、 **ClassInstall32**セクションを再インストールするか、既にあるクラスの設定を変更するにはインストールされています。 具体的には、使用することはできません、 **ClassInstall32**クラス共同インストーラーまたは既にインストールされているクラスのクラスのフィルター ドライバーを追加するセクション。 共同インストーラーをインストールして、ドライバーをフィルター処理する方法については、次を参照してください。[共同インストーラーの作成](writing-a-co-installer.md)と[フィルター ドライバーをインストールする](installing-a-filter-driver.md)します。

通常、 **ClassInstall32**セクションには 1 つまたは複数**AddReg**システム提供の下にエントリを追加するディレクティブ*SetupClassGUID*レジストリのサブキー。 これらのエントリは、クラス固有の「表示名、」を含めることができますクラスのインストーラーのパス、クラスのアイコン、プロパティ ページのプロバイダー、およびなど。

除く**AddReg**と**CopyFiles**、表示されるその他のディレクティブは、ここではほとんど使われません、 **ClassInstall32**セクション。

ドライバー ファイルのマルチプラット フォーム対応の配布をサポートするプラットフォームに固有の構築**ClassInstall32**セクション。 たとえば、そのプロセスの機能すべてのシステム SetupAPI、 **ClassInstall32**最初のセクションでは検索、 **ClassInstall32.ntx86** x86 セクション プラットフォームのみ非装飾のを調べると**ClassInstall32**セクションが見つけられない場合、 **ClassInstall32.ntx86**セクション。 詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

**注**  、 **ClassInstall32**セクション名は 64 ビット プラットフォーム上のインストールでも使用されます。

 

Windows 2000 以降、インストールされているすべてのデバイスに関連付けられている、[デバイス セットアップ クラス](device-setup-classes.md)レジストリにします。 デバイスの INF をインストールするのには、新しいデバイスのクラスのインストーラーに関連付けられていない場合、または場合その**ClassGUID =** 内の指定、**バージョン**セクションは、システム定義のセットアップ クラス GUID と一致しませんそのデバイスのレジストリ サブキーの下に作成 **.クラス\\{**<em>UnknownClassGUID</em>**}** します。

通常、任意のデバイス クラスのインストーラーの INF には、 **AddReg**ディレクティブでその**ClassInstall32**セクションで、その種類のデバイスのフレンドリ名を作成するには少なくとも 1 つの名前付きセクションを定義します。 セットアップ コードが自動的に作成、 *SetupClassGUID*に指定された値からレジストリ サブキー、 **ClassGUID =** INF の内のエントリ**バージョン**セクションときに、(新規) そのセットアップ クラスの最初のデバイスがインストールされています。

この*SetupClassGUID*サブキー、そのような INF レジストリの情報も提供*モデル*の追加を使用して特定のサブキー **AddReg**そのディレクティブ*DDInstall*セクション。 INF がで参照されている追加レジストリ セクションを使用してさらに、その**ClassInstall32**セクション プロパティ ページのプロバイダーを指定して、そのクラスのデバイスのユーザー インターフェイスでの処理方法を制御します。

このようなクラスに固有の追加レジストリ セクションでは、次の一般的な形式があります。

```ini
[SetupClassAddReg]
 
HKR,,,,%DevClassName% ; device-class friendly name 
[HKR,,Installer32,,"class-installer.dll,class-entry-point"] 
[HKR,,EnumPropPages32,,"prop-provider.dll,provider-entry-point"]
HKR,,Icon,,"icon-number" 
[HKR,,SilentInstall,,1]
[HKR,,NoInstallClass,,1]
[HKR,,NoDisplayClass,,1]
```

システムでは、指定されたアイコンを使用して、ユーザーに、インストーラーを表します。

-   アイコンの値が正の場合は、リソースのリソース識別子を表します。 リソースは、EnumPropPages32 キーが指定されている場合、クラスのインストーラー Installer32 キーが指定されている場合、DLL からまたはプロパティ ページの DLL から抽出されます。 値「0」は、DLL の最初のアイコンを表します。 値「1」は予約されています。
-   アイコンの値が負の場合、絶対値、SetupApi.DLL にあるアイコンのリソース識別子です。

定義済み設定**SilentInstall**、 **NoDisplayClass**、および**NoInstallClass**クラス固有のレジストリ キー内のエントリをブール値が次の影響。

-   その後 DDInstall セクションでは、クラスのインストーラーの INF ファイルのまたはに個別の INF ファイルを指定するかどうか、このクラスのデバイスのインストール中に応答を要求するユーザーにポップアップ メッセージを送信しないインストーラーに指示 SilentInstall の設定インストールされている同じ ClassGuid を設定してこのクラスの宣言デバイス = {ClassGUID} 仕様の対応するバージョン セクションでします。 たとえば、CD-ROM とディスクのデバイスのシステム クラスのインストーラーとシステム パラレル ポートのクラスのインストーラーは、これらそれぞれのレジストリ キーで SilentInstall を設定します。

    クラスに固有のインストーラーには、コンピューターにインストールされる任意のデバイスの再起動が必要とする場合、INF でクラスに固有の追加レジストリ セクションこのエントリことはできません。

-   デバイス マネージャーでこのクラスのすべてのデバイスのユーザーに表示される表示を抑制 NoDisplayClass を設定します。 たとえば、プリンターとネットワーク ドライバーが (クライアント、サービス、およびプロトコルを含む) のシステム クラスのインストーラーは、それぞれのレジストリ キーで NoDisplayClass を設定します。
-   NoInstallClass の設定は、この種類のデバイスはこれまでは必要ありません手動インストール エンドユーザーによることを示します。 たとえば、プラグ アンド プレイ (PnP) デバイス専用のシステム クラスのインストーラーは、それぞれのレジストリ キーで NoInstallClass を設定します。

A **ClassInstall32**セクションに含めることができます**AddReg**を設定するディレクティブ、 **DeviceType**、 **DeviceCharacteristics**、および**セキュリティ**そのセットアップ クラスのデバイス用です。 参照してください、 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)詳細についてはします。

<a name="examples"></a>例
--------

この例では、 **ClassInstall32**セクションで、と共に、名前付きセクションの参照と、 [ **AddReg ディレクティブ**](inf-addreg-directive.md)システムの INF のクラスを表示インストーラー。

```ini
[ClassInstall32] 
AddReg=display_class_addreg

[display_class_addreg]
HKR,,,,%DisplayClassName%
HKR,,Installer32,,"Desk.Cpl,DisplayClassInstaller"
HKR,,Icon,,"-1"
```

これに対し、この例はシステム CD-ROM INF の参照の追加レジストリ セクション**ClassInstall32**セクション。 これは、インストール CD-ROM デバイス/ドライバーのクラスに固有のプロパティ ページのプロバイダーを設定します。 またこの INF を設定、 **SilentInstall**と**NoInstallClass**に CD-ROM クラス キーのエントリの値**TRUE** (**1**)。

```ini
[cdrom_class_addreg]
HKR,,,,%CDClassName%
HKR,,EnumPropPages32,,"SysSetup.Dll,CdromPropPageProvider"
HKR,,SilentInstall,,1
HKR,,NoInstallClass,,1
HKR,,Icon,,"101"
```

## <a name="see-also"></a>関連項目


[**AddProperty**](inf-addproperty-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelProperty**](inf-delproperty-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[***モデル***](inf-models-section.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SetupDiBuildClassInfoListEx**](https://msdn.microsoft.com/library/windows/hardware/ff550911)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**バージョン**](inf-version-section.md)

 

 






