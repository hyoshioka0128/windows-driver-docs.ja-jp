---
title: INF ClassInstall32 セクション
description: ClassInstall32 セクションでは、新しいクラスにデバイス用の新しいデバイスセットアップクラス (および場合によってはクラスインストーラー) をインストールします。
ms.assetid: c1da44ca-3b99-43de-99ef-56fbe67b46c2
keywords:
- INF ClassInstall32 セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF ClassInstall32 Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 672538c83dfcc0af374d6eaebe23467070e89a28
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223272"
---
# <a name="inf-classinstall32-section"></a>INF ClassInstall32 セクション


**注**  ユニバーサルまたはモバイルのドライバーパッケージを作成する場合、このセクションは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**ClassInstall32**セクションでは、新しいクラスにデバイス用の新しい[デバイスセットアップクラス](device-setup-classes.md)(および場合によってはクラスインストーラー) をインストールします。

```inf
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


<a href="" id="addreg-add-registry-section--add-registry-section-----"></a>**AddReg =**<em>add</em>-*レジストリ*\[**,**<em>add</em>-*registry**section*-*section*セクションの追加、レジストリセクション\]の追加...-  
レジストリに書き込まれるクラス固有の値エントリを含む、1つまたは複数の名前付きセクションを参照します。 通常、これは、新しいデバイスセットアップクラスに、その他のコンポーネントが後でレジストリから取得し、この新しいデバイスクラスのインストールされているデバイスを開くために使用し、このデバイスセットアップクラスの新しいデバイスクラスインストーラーやプロパティページプロバイダーを "インストール" するために使用するフレンドリ名を指定するために使用されます。

すべての*レジストリセクション*で**hkr**仕様を指定すると、 **..クラス\\{**<em>setupclassguid</em>**}** レジストリキー。 詳細については、次の「**解説**」を参照してください。

詳細については、「 [**INF AddReg ディレクティブ**](inf-addreg-directive.md)」を参照してください。

<a href="" id="addproperty-add-property-section--add-property-section-----"></a>**Addproperty =**<em>add</em>\[-property **-section-**<em>section</em> \] ...  
(Windows Vista 以降のバージョンの Windows)[デバイスセットアップクラス](device-setup-classes.md)に設定されている[デバイスプロパティ](device-properties.md)を変更する1つ以上の INF ファイルセクションを参照します。 Windows Vista 以降のバージョンの Windows オペレーティングシステムで新しく追加されたデバイスセットアップクラスのプロパティを設定する場合にのみ、 [**INF AddProperty ディレクティブ**](inf-addproperty-directive.md)を使用する必要があります。

Windows Server 2003、Windows XP、または Windows 2000 で以前に導入され、対応するレジストリエントリ値を持つデバイスクラスのプロパティについては、引き続き[**INF AddReg ディレクティブ**](inf-addreg-directive.md)を使用して、デバイスセットアップクラスのプロパティを設定する必要があります。 これらのガイドラインは、システム定義のプロパティとカスタムプロパティに適用されます。

**Addproperty**ディレクティブの使用方法の詳細については、「 [Inf addproperty ディレクティブと Inf Delproperty ディレクティブの使用](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)」を参照してください。

<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**Copyfiles = @**<em>filename</em> | *ファイル*-*リスト*-*セクション*-*list***,**<em>file</em>\] 、ファイルリスト-*セクション*...\[  
は、ソースメディアから転送先にコピーする名前付きのファイルを指定するか、ソースメディア上のクラス関連ファイルが転送先に転送するように指定する1つ以上の名前付きセクションを参照します。 INF の[**Destinationdirs**](inf-destinationdirs-section.md)セクションの**DefaultDestDir**エントリは、コピーするクラス固有の1つのファイルのコピー先ディレクトリを指定します。

詳細については、「 [**INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)」を参照してください。

**メモ**  デバイスセットアップクラス (およびクラスインストーラー) 用のシステム提供の INF ファイルでは、このセクションではこのディレクティブを使用しないことに注意してください。

 

<a href="" id="delreg-del-registry-section--del-registry-section-----"></a>**Delreg =**<em>del</em>-*レジストリ*-*セクション*\[**、**<em>del</em>-*section* *registry*レジストリセクション\] ...-  
クラスインストーラーのインストール中に値エントリまたはキーがレジストリから削除されるように指定されている、1つまたは複数の名前付きセクションを参照します。

ただし、特定の **{**<em>setupclassguid</em>**}** サブキーがレジストリに存在する場合は**です。クラス**の分岐では、システムセットアップコードは、その**バージョン**セクションで同じ GUID 値を指定するすべての INF の**ClassInstall32**セクションを無視します。 そのため、INF は、既存のクラスインストーラーを置き換えることや、 **ClassInstall32**セクションから動作を変更することはできません。 既存のクラスインストーラーの動作を変更するには、クラス固有の共同インストーラーを使用します。

詳細については、「 [**INF DelReg ディレクティブ**](inf-delreg-directive.md)」を参照してください。

<a href="" id="delproperty-del-property-section--del-property-section-----"></a>**Delproperty =**<em>del-property</em>\[-section **,**<em>delete-section</em> \] ...  
(Windows Vista 以降のバージョンの Windows)[デバイスセットアップクラス](device-setup-classes.md)に設定されている[デバイスプロパティ](device-properties.md)を削除する1つ以上の INF ファイルセクションを参照します。 [**INF delproperty ディレクティブ**](inf-delproperty-directive.md)は、windows Vista 以降のバージョンの windows オペレーティングシステムで新しく追加されたデバイスセットアップクラスのプロパティを削除する場合にのみ使用してください。

Windows Server 2003、Windows XP、または Windows 2000 で以前に導入され、対応するレジストリエントリ値を持つデバイスクラスのプロパティについては、引き続き[**INF DelReg ディレクティブ**](inf-delreg-directive.md)を使用して、デバイスセットアップクラスのプロパティを削除する必要があります。 これらのガイドラインは、システム定義のプロパティとカスタムプロパティに適用されます。

**Delproperty**ディレクティブの使用方法の詳細については、「 [Inf addproperty ディレクティブと Inf Delproperty ディレクティブの使用](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)」を参照してください。

<a href="" id="delfiles-file-listsection--file-list-section-----"></a>**Delfiles =**<em>ファイル-listsection</em>\[**、**<em>ファイル</em>-*リスト*-*セクション*\] ...  
ターゲットに既にインストールされているクラス関連ファイルが削除対象として指定されている、1つまたは複数の名前付きセクションを参照します。

詳細については、「 [**INF DelFiles ディレクティブ**](inf-delfiles-directive.md)」を参照してください。

<a href="" id="renfiles-file-list-section--file-list-section-----"></a>**Renfiles =**<em>file-list-section</em>\[**,**<em>file</em>\] *list*ファイルリストの*セクション*...--  
転送先で名前を変更するクラス関連ファイルが一覧表示される1つ以上の名前付きセクションを参照します。

詳細については、「 [**INF RenFiles ディレクティブ**](inf-renfiles-directive.md)」を参照してください。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**Bitreg =**<em>ビットレジストリ-セクション</em>\[**、**<em>ビットレジストリ-セクション</em>\]...  
はこのセクションでは有効ですが、ほとんど使用されていません。

詳細については、「 [**INF BitReg ディレクティブ**](inf-bitreg-directive.md)」を参照してください。

<a href="" id="updateinis-update-ini-section--update-ini-section------"></a>**Updateinis**=*.ini-\[セクション、更新プログラム-ini-セクション\]*...   
はこのセクションでは有効ですが、ほとんど使用されていません。

詳細については、「 [**INF UpdateInis ディレクティブ**](inf-updateinis-directive.md)」を参照してください。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>inifields-section</em>\[**,**<em>inifields-section</em>\]...  
はこのセクションでは有効ですが、ほとんど使用されていません。

詳細については、「 [**INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)」を参照してください。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>ini</em>\[-セクション **、**<em>ini からレジストリへ</em>\]のセクション...  
はこのセクションでは有効ですが、ほとんど使用されていません。

詳細については、「 [**INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)」を参照してください。

<a name="remarks"></a>解説
-------

新しいカスタムデバイスセットアップクラスをインストールする場合にのみ、デバイスの INF ファイルに**ClassInstall32**セクションを含める必要があります。 インストールされているクラスのデバイスの INF ファイル。[システムが提供するデバイスセットアップクラス](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))またはカスタムクラスに**ClassInstall32**セクションを含めることはできません。 **ClassInstall32**セクションは、クラスがまだインストールされていない場合にのみ、システムによって処理されるため、 **ClassInstall32**セクションを使用して、既にインストールされているクラスの設定を再インストールまたは変更することはできません。 特に、 **ClassInstall32**セクションを使用して、既にインストールされているクラスのクラスの共同インストーラーまたはクラスフィルタードライバーを追加することはできません。 共同インストーラーとフィルタードライバーをインストールする方法の詳細については、「[共同インストーラーを作成](writing-a-co-installer.md)する」および「[フィルタードライバーをインストール](installing-a-filter-driver.md)する」を参照してください。

通常、 **ClassInstall32**セクションには、レジストリのシステム指定の*setupclassguid*サブキーの下にエントリを追加するための**AddReg**ディレクティブが1つ以上含まれています。 これらのエントリには、クラス固有の "表示名"、"クラスインストーラーパス"、"クラスアイコン"、"プロパティページプロバイダー" などを含めることができます。

**AddReg**と**CopyFiles**を除き、ここで示す他のディレクティブは、 **ClassInstall32**セクションではほとんど使用されません。

ドライバーファイルのマルチプラットフォーム配布をサポートするには、プラットフォーム固有の**ClassInstall32**セクションを構築します。 たとえば、 **ClassInstall32**セクションを処理するすべてのシステムの機能は、最初に x86 プラットフォームの ClassInstall32 セクションを検索し、 **ntx86**セクションが見つからない場合にのみ、装飾されていない**ClassInstall32**セクションを**調べます。** システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

**注**   **ClassInstall32**セクション名は、64ビットプラットフォームでのインストールにも使用されます。

 

Windows 2000 以降では、インストールされているすべてのデバイスが、レジストリ内の[デバイスセットアップクラス](device-setup-classes.md)に関連付けられています。 インストールするデバイスの INF が新しいデバイスクラスインストーラーに関連付けられていない場合、または**Version**セクションの**classguid =** specification がシステム定義のセットアップクラス GUID と一致しない場合は、そのデバイスのレジストリサブキーが. の下に作成され**ます。クラス\\{**<em>UnknownClassGUID</em>**}**。

デバイスクラスインストーラーの INF には、通常、 **ClassInstall32**セクションに**AddReg**ディレクティブがあり、デバイスの種類のフレンドリ名を作成する名前付きセクションを少なくとも1つ定義します。 セットアップコードは、(新しい) セットアップクラスの最初のデバイスがインストールされるときに、INF の**Version**セクションの**classguid =** エントリに指定された値からレジストリに*setupclassguid*サブキーを自動的に作成します。

この*Setupclassguid*サブキーの下では、このような INF は、 *ddinstall*セクションで追加の**AddReg**ディレクティブを使用して、*モデル*固有のサブキーのレジストリ情報も提供します。 さらに、INF は、 **ClassInstall32**セクションで参照されているレジストリの追加セクションを使用して、プロパティページプロバイダーを指定したり、ユーザーインターフェイスでのデバイスのクラスの処理方法を制御したりすることができます。

このようなクラス固有の追加レジストリのセクションには、次の一般的な形式があります。

```inf
[SetupClassAddReg]
 
HKR,,,,%DevClassName% ; device-class friendly name 
[HKR,,Installer32,,"class-installer.dll,class-entry-point"] 
[HKR,,EnumPropPages32,,"prop-provider.dll,provider-entry-point"]
HKR,,Icon,,"icon-number" 
[HKR,,SilentInstall,,1]
[HKR,,NoInstallClass,,1]
[HKR,,NoDisplayClass,,1]
```

システムは、指定されたアイコンを使用して、ユーザーに対するインストーラーを表します。

-   アイコンの値が正の値の場合は、リソースのリソース識別子を表します。 Installer32 キーが指定されている場合、またはプロパティページ DLL から、EnumPropPages32 キーが指定されている場合、リソースはクラスインストーラー DLL から抽出されます。 値 "0" は、DLL 内の最初のアイコンを表します。 値 "1" は予約されています。
-   アイコンの値が負の場合、absolute の値は、Setupapi.log のアイコンのリソース識別子になります。

クラス固有のレジストリキー**に定義済み**の NoInstallClass、 **nodisplayclass**、および**NoInstallClass**ブール値のエントリを設定すると、次のような影響があります。

-   このクラスのデバイスをインストールするときに、クラスインストーラーの INF ファイルの DDInstall セクションで指定されているかどうか、また、このクラスを宣言する後にインストールされるデバイス用に、それぞれのバージョンセクションで同じ ClassGuid = {ClassGUID} 仕様を設定することによって、このクラスのデバイスのインストール中に、応答を必要と たとえば、CD-ROM およびディスクデバイスのシステムクラスインストーラーと、システムパラレルポートクラスインストーラーによって、それぞれのレジストリキーに "ドライブのインストール" が設定されています。

    クラス固有のインストーラーで、インストールするデバイスに対してコンピューターを再起動する必要がある場合、その INF のクラス固有の追加レジストリセクションにこの値のエントリを含めることはできません。

-   NoDisplayClass を設定すると、デバイスマネージャーによって、このクラスのすべてのデバイスのユーザーに表示される表示が抑制されます。 たとえば、プリンターおよびネットワークドライバー (クライアント、サービス、プロトコルを含む) のシステムクラスインストーラーは、それぞれのレジストリキーで NoDisplayClass を設定します。
-   NoInstallClass を設定すると、この種類のデバイスがエンドユーザーによる手動インストールを必要としないことを示します。 たとえば、プラグアンドプレイ (PnP) デバイスのシステムクラスインストーラーでは、それぞれのレジストリキーに NoInstallClass が設定されています。

**ClassInstall32**セクションには、セットアップクラスのデバイスに **(devicetype**、 **DeviceCharacteristics**、および**セキュリティ**を設定する**AddReg**ディレクティブを含めることができます。 詳細については、 [**INF AddReg ディレクティブ**](inf-addreg-directive.md)を参照してください。

<a name="examples"></a>例
--------

この例では、 **ClassInstall32**セクションと、 [**AddReg ディレクティブ**](inf-addreg-directive.md)を使用して参照する名前付きセクションを、システム表示クラスインストーラーの INF に示します。

```inf
[ClassInstall32] 
AddReg=display_class_addreg

[display_class_addreg]
HKR,,,,%DisplayClassName%
HKR,,Installer32,,"Desk.Cpl,DisplayClassInstaller"
HKR,,Icon,,"-1"
```

これに対して、この例では、システムの CD-ROM INF の**ClassInstall32**セクションで参照されている [レジストリの追加] セクションを示しています。 インストールする CD-ROM デバイス/ドライバー用のクラス固有のプロパティページプロバイダーを設定します。 また、この INF は **、cd-rom**クラスキーの**NoInstallClass**値エントリを**TRUE** (**1**) に設定します。

```inf
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

[**Setupdibuildclassinの Istex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolistexa)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**バージョン**](inf-version-section.md)

 

 






