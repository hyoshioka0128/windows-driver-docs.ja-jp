---
title: INF ProfileItems ディレクティブ
description: '[INF DDInstall] セクションでは、[スタート] メニューに追加または削除する項目またはグループを含む1つまたは複数のプロファイル項目セクションを一覧表示するために、ProfileItems ディレクティブが使用されます。'
ms.assetid: 8cdd6dcd-de5d-4652-8842-6b0be6f5fb59
keywords:
- INF ProfileItems ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF ProfileItems Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e74eeb050677a3e8f7267f2288dff0e17e7df5d
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223130"
---
# <a name="inf-profileitems-directive"></a>INF ProfileItems ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

[ [**INF *ddinstall* ] セクション**](inf-ddinstall-section.md)では、[スタート] メニューに追加または削除する項目またはグループを含む1つまたは複数の*プロファイル項目セクション*を一覧表示するために、 **profileitems**ディレクティブが使用されます。

```inf
[DDInstall] 
 
ProfileItems=profile-items-section[,profile-items-section]...
...
```

**Profileitems**ディレクティブによって参照される名前付きセクションには、次の形式があります。

```inf
[profile-items-section]
 
Name=link-name[,name-attributes]
CmdLine=dirid,[subdir],filename
[SubDir=path]
[WorkingDir=wd-dirid,wd-subdir]
[IconPath=icon-dirid,[icon-subdir],icon-filename]
[IconIndex=index-value]
[HotKey=hotkey-value]
[Infotip=info-tip]
[DisplayResource="ResDllPath\ResDll",ResID]
```

このディレクティブは、windows XP 以降のバージョンの Windows でサポートされています。

## <a name="entries"></a>エントリ


<a href="" id="name-link-name--name-attributes-"></a>**名前 =**<em>リンク-名前</em>\[**、**<em>名前属性</em>\]  
*リンク名*には、メニュー項目またはグループのリンクの名前を指定し*ます。 .lnk*拡張子はありません。 この値には、文字列または INF ファイルの[**文字列**](inf-strings-section.md)セクションで定義されている%*strkey*% トークンを指定できます。 **Displayresource**エントリが指定されていない場合は、*リンク名*も表示文字列になります。

省略可能*な名前-属性*の値は、メニュー項目の操作に影響を与える1つ以上のフラグを指定します。 この値は、システム定義のフラグ値のビットマスクとして表されます。 使用できるフラグは次のとおりです。

<a href="" id="0x00000001--flg-profitem-currentuser-"></a>**0x00000001** (FLG_PROFITEM_CURRENTUSER)  
現在のユーザーのプロファイルの [スタート] メニュー項目を作成または削除するように Windows に指示します。 このフラグが指定されていない場合、Windows はすべてのユーザーの項目を処理します。

<a href="" id="0x00000002---flg-profitem-delete-"></a>**0x00000002** (FLG_PROFITEM_DELETE)  
メニュー項目を削除するように Windows に指示します。 このフラグが指定されていない場合は、項目が作成されます。

<a href="" id="0x00000004--flg-profitem-group-"></a>**0x00000004** (FLG_PROFITEM_GROUP)  
[スタート\\プログラム] の [スタート] メニューグループを作成または削除するように Windows に指示します。 このフラグが指定されていない場合、Windows はメニューグループではなく、メニュー項目を作成または削除します。

フラグが指定されていない場合、Windows はすべてのユーザーのメニュー項目を作成します。

<a href="" id="cmdline-dirid--subdir--filename"></a>**CmdLine =**<em>dirid</em>**、**\[*subdir*\]**、**<em>filename</em>  
*Dirid*は、コマンドプログラムが存在するディレクトリを識別する値を指定します。 たとえば、値が11の*dirid*は、システムディレクトリを示します。 使用可能な*dirid*値は、 [**destinationdirs**](inf-destinationdirs-section.md)セクションの*dirid*値の説明に記載されています。

*Subdir*文字列が存在する場合、コマンドプログラムは*dirid*によって参照されるディレクトリのサブディレクトリにあります。 *Subdir*は、サブディレクトリを指定します。 *Subdir*が指定されていない場合、プログラムは*dirid*によって参照されるディレクトリにあります。

*Filename*は、メニュー項目に関連付けられているプログラムの名前を指定します。

<a href="" id="subdir-path"></a>**SubDir =**<em>パス</em>  
この省略可能なエントリは、メニュー項目が存在\\する [スタートプログラム] の下にサブディレクトリ (サブメニュー) を指定します。 このエントリが省略されている場合、パス\\は既定で [プログラムの開始] になります。

たとえば、"Subdir = アクセサリー\\ゲーム" というエントリ*が含まれている*場合、メニュー項目は [スタート\\プログラム\\] [アクセサリ\\ゲーム] サブメニューで作成または削除されます。

**注**  *名前属性*に FLG_PROFITEM_GROUP が指定されている場合、 **SubDir**エントリは無視されます。

 

<a href="" id="workingdir-wd-dirid--wd-subdir-"></a>**WorkingDir =**<em>wd-dirid</em>\[**,**<em>wd-subdir</em>\]  
この省略可能なエントリは、コマンドプログラムの作業ディレクトリを指定します。 このエントリを省略した場合、作業ディレクトリは、コマンドプログラムが存在するディレクトリに既定で設定されます。

*Wd-dirid*値は、作業ディレクトリを識別します。 使用可能な*dirid*値の一覧については、「 [Dirid の使用](using-dirids.md)」を参照してください。

*Subdir*文字列 (存在する場合) は、 *wd-dirid*のサブディレクトリを作業ディレクトリに指定します。 システム定義の*dirid*がないディレクトリを指定するには、このパラメーターを使用します。 このパラメーターを省略した場合、 *wd-dirid*値だけが作業ディレクトリを指定します。

<a href="" id="iconpath-icon-dirid--icon-subdir--icon-filename"></a>**Iconpath =**<em>icon-dirid</em>**、**\[*icon-subdir*\]**、**<em>icon-filename</em>  
この省略可能なエントリは、メニュー項目のアイコンを含むファイルの場所を指定します。

*Icon-dirid*文字列は、アイコンが含まれている DLL のディレクトリを識別します。 使用可能な*dirid*値の一覧については、「 [Dirid の使用](using-dirids.md)」を参照してください。

*Subdir*値 (存在する場合) は、DLL が*icon-dirid*のサブディレクトリにあることを示します。 *Subdir*値は、サブディレクトリを指定します。

*アイコン-filename*値は、アイコンを含む DLL を指定します。

このエントリを省略した場合、Windows は、 **CmdLine**エントリで指定されたファイル内のアイコンを検索します。

<a href="" id="iconindex-index-value"></a>**IconIndex =**<em>インデックス-値</em>  
この省略可能なエントリは、メニュー項目に使用する DLL 内のアイコンを指定します。 DLL 内のアイコンのインデックスを作成する方法の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

**Iconpath**エントリが指定されている場合、*インデックス値*はその DLL にインデックスを付けます。 それ以外の場合、この値は、 **CmdLine**エントリで指定されたファイルにインデックスを付けます。

<a href="" id="hotkey-hotkey-value"></a>**ホットキー =**<em>ホットキー-値</em>  
この省略可能なエントリは、メニュー項目のキーボードアクセスキーを指定します。

ホットキーの詳細については、Windows SDK のドキュメントを参照してください。

<a href="" id="infotip-info-tip"></a>ヒント **=**<em>ヒント</em>  
この省略可能なエントリは、メニュー項目の情報ヒントを指定します。

この値には、文字列または INF ファイルの[**文字列**](inf-strings-section.md)セクションで定義されている%*strkey*% トークンを指定できます。

*Info-tip*値は、 **"@**<em>resdllpath</em>**\\**<em>resdllpath</em>**,-**<em>ResID</em>**"** として指定することもできます。ここで、 *resdllpath*と*resdllpath*はリソース DLL のパスとファイル名を指定し、-*ResID*はリソース ID を表す負の値です。

Windows の多言語ユーザーインターフェイス (MUI) をサポートするには、この形式を使用します。 例を次に示します。

```inf
InfoTip = "@%11%\shell32.dll,-22531"
```

<a href="" id="displayresource--resdllpath-resdll--resid"></a>**Displayresource = "**<em>resdllpath\\resdllpath</em>**",**<em>ResID</em>  
この省略可能なエントリは、ショートカットまたはグループの表示名として [スタート] メニューで使用する、ローカライズ可能な文字列を識別する文字列リソースを指定します。

*Resdllpath*と*RESDLLPATH*はリソース DLL のパスとファイル名を指定し、 *resID*はリソース ID を表す正の値です。 例を次に示します。

```inf
DisplayResource="%11%\shell32.dll",22019
```

Windows の多言語ユーザーインターフェイス (MUI) をサポートするには、このエントリを使用します。 このエントリが使用されていない場合は、 **Name**エントリによって指定された文字列が表示されます。

<a name="remarks"></a>解説
-------

特定の*プロファイル項目セクション*名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

各*プロファイル項目-セクション*には、1つのスタートメニュー項目またはグループを作成または削除するための詳細情報が含まれています。 1つの INF から複数のメニュー項目またはグループを操作するには、複数の*プロファイル項目セクション*を作成し、 **profileitems**ディレクティブのセクションを一覧表示します。

*「* [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」で説明されているように、%*strkey*% トークンを使用して指定された文字列パラメーターのいずれかを指定できます。

<a name="examples"></a>例
--------

次の INF ファイルの抜粋では、[*プロファイル-項目] セクション*を使用して、電卓を [スタート] メニューに追加する方法を示しています。

```inf
[CalcInstallItems]
Name = %Calc_DESC%
CmdLine = 11,, calc.exe
SubDir = %Access_GROUP%
WorkingDir = 11
InfoTip = %Calc_TIP%
:
:
[Strings]
AccessGroup = "Accessories"
Calc_DESC = "Calculator"
Calc_TIP = "Performs basic arithmetic tasks with an on-screen calculator"
```

次の INF ファイルの抜粋は、 **Displayresource**エントリを使用して、ローカライズされたメニュー項目を作成することによって、同じソフトウェアをインストールする方法を示しています。

```inf
[CalcInstallItems]
Name = %Calc_DESC%
CmdLine = 11,, calc.exe
SubDir = %Access_GROUP%
WorkingDir = 11
InfoTip = "@%11%\shell32.dll,-22531"
DisplayResource="%11%\shell32.dll",22019
:
:
[Strings]
Access_GROUP = "Accessories"
Calc_DESC = "Calculator"
```

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

 

 






