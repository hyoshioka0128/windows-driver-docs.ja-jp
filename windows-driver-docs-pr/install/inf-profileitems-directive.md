---
title: INF ProfileItems ディレクティブ
description: に対するプロファイル-項目のセクションの詳細を含むアイテムや追加、または [スタート] メニューから削除するグループまたは ProfileItems ディレクティブは、いずれかの一覧に INF DDInstall セクションで使用されます。
ms.assetid: 8cdd6dcd-de5d-4652-8842-6b0be6f5fb59
keywords:
- INF ProfileItems ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF ProfileItems Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 604a781f1f8cf400d73783ae1af5132bb6b88e5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536724"
---
# <a name="inf-profileitems-directive"></a>INF ProfileItems ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **ProfileItems**にディレクティブを使用する[ **INF *DDInstall*セクション**](inf-ddinstall-section.md)を 1 つまたは複数のリストに*プロファイルのセクションの項目*アイテムや追加、または [スタート] メニューから削除するグループが含まれています。

```ini
[DDInstall] 
 
ProfileItems=profile-items-section[,profile-items-section]...
...
```

セクションによって参照される各名前付き、 **ProfileItems**ディレクティブは、次の形式。

```ini
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

このディレクティブは、Windows XP および Windows の以降のバージョンでサポートされます。

## <a name="entries"></a>エントリ


<a href="" id="name-link-name--name-attributes-"></a>**Name=**<em>link-name</em>\[**,**<em>name-attributes</em>\]  
*リンク名*メニュー項目またはグループのリンクの名前を指定せず、 *.lnk*拡張機能。 この値は文字列または %*strkey*% トークンで定義されている、 [**文字列**](inf-strings-section.md) INF ファイルのセクション。 場合、 **DisplayResource**エントリが指定されていない*リンク名*も表示文字列です。

省略可能な*名属性*値がメニュー項目の動作に影響する 1 つまたは複数のフラグを指定します。 この値は、システム定義のフラグの値の論理和のビットマスクとして表されます。 使用できるフラグを以下に示します。

<a href="" id="0x00000001--flg-profitem-currentuser-"></a>**0x00000001** (FLG_PROFITEM_CURRENTUSER)  
作成または現在のユーザーのプロファイルでスタート メニュー項目を削除する Windows に指示します。 このフラグが指定されていない場合、Windows は、すべてのユーザーの項目を処理します。

<a href="" id="0x00000002---flg-profitem-delete-"></a>**0x00000002** (FLG_PROFITEM_DELETE)  
メニュー項目を削除する Windows に指示します。 このフラグが指定されていない場合、項目が作成されます。

<a href="" id="0x00000004--flg-profitem-group-"></a>**0x00000004** (FLG_PROFITEM_GROUP)  
作成または開始 [スタート] メニューのグループを削除する Windows に指示\\プログラム。 このフラグが指定されていない場合、Windows は作成またはメニュー グループではなく、メニュー項目を削除します。

フラグが指定されていない場合、Windows は、すべてのユーザーのメニュー項目を作成します。

<a href="" id="cmdline-dirid--subdir--filename"></a>**CmdLine =**<em>dirid</em>**、**\[*subdir*\]**、**<em>ファイル名</em>  
*Dirid*コマンド プログラムが存在するディレクトリを識別する値を指定します。 たとえば、 *dirid* 11 のシステム ディレクトリを示します。 使用可能な*dirid*値の説明に表示されます、 *dirid*値、 [ **DestinationDirs** ](inf-destinationdirs-section.md)セクション。

場合、 *subdir*文字列が存在する、コマンドのプログラムによって参照されるディレクトリのサブディレクトリにある*dirid*します。 *Subdir*サブディレクトリを指定します。 ない場合は*subdir*を指定すると、プログラムがによって参照されるディレクトリでは*dirid*します。

*Filename*メニュー項目に関連付けられているプログラムの名前を指定します。

<a href="" id="subdir-path"></a>**SubDir =**<em>パス</em>  
この省略可能なエントリが 開始サブディレクトリ (サブメニューで開く) を指定します\\メニュー項目が存在するプログラムします。 このエントリを省略すると、パスの開始既定\\プログラム。

たとえば場合、*プロファイル-section 項目*エントリがあります"Subdir = [アクセサリ]\\ゲーム"、メニュー項目がされているし、作成または削除、[スタート] 内\\プログラム\\アクセサリ\\ゲーム サブメニューで開く。

**注**  場合 FLG_PROFITEM_GROUP が指定されて*名属性*、 **SubDir**エントリは無視されます。

 

<a href="" id="workingdir-wd-dirid--wd-subdir-"></a>**WorkingDir =**<em>wd dirid</em>\[**、**<em>wd subdir</em>\]  
この省略可能なエントリには、コマンド ライン プログラム用の作業ディレクトリを指定します。 このエントリを省略した場合、コマンド ライン プログラムが存在するディレクトリを作業ディレクトリが既定値です。

*Wd dirid*値は、作業ディレクトリを識別します。 候補のリストの*dirid*値を参照してください[を使用して Dirids](using-dirids.md)します。

*Wd subdir*文字列、存在する場合、指定のサブディレクトリ*wd dirid*を作業ディレクトリ。 このパラメーターを使用して、システム定義していないディレクトリを指定する*dirid*します。 このパラメーターを省略した場合、 *wd dirid*値だけでは、作業ディレクトリを指定します。

<a href="" id="iconpath-icon-dirid--icon-subdir--icon-filename"></a>**IconPath =**<em>アイコン dirid</em>**、**\[*アイコン subdir*\]**、** <em>アイコンのファイル名</em>  
この省略可能なエントリでは、メニュー項目のアイコンを含むファイルの場所を指定します。

*アイコン dirid*アイコンを含む DLL のディレクトリを識別する文字列。 候補のリストの*dirid*値を参照してください[を使用して Dirids](using-dirids.md)します。

*アイコン subdir*値、存在する場合、あることを示します、DLL のサブディレクトリに*アイコン dirid*します。 *アイコン subdir*値をサブディレクトリを指定します。

*アイコンのファイル名*アイコンを含む DLL を指定します。

このエントリを省略すると、Windows 検索で指定されたファイルのアイコン、 **CmdLine**エントリ。

<a href="" id="iconindex-index-value"></a>**IconIndex=**<em>index-value</em>  
この省略可能なエントリでは、メニュー項目に使用する DLL のアイコンを指定します。 DLL 内のアイコンのインデックスを作成する方法については、Microsoft Windows SDK のドキュメントを参照してください。

場合、 **IconPath**エントリが指定されて、*インデックス値*その DLL へのインデックス。 この値で指定されたファイルにインデックスを作成、それ以外の場合、 **CmdLine**エントリ。

<a href="" id="hotkey-hotkey-value"></a>**ホットキー =**<em>ホットキー値</em>  
この省略可能なエントリでは、メニュー項目のキーボード ショートカット キーを指定します。

ホット キーの詳細については、Windows SDK のドキュメントを参照してください。

<a href="" id="infotip-info-tip"></a>**ヒント =**<em>に関するヒント</em>  
この省略可能なエントリでは、メニュー項目の情報のヒントを指定します。

この値は文字列または %*strkey*% トークンで定義されている、 [**文字列**](inf-strings-section.md) INF ファイルのセクション。

*に関するヒント*として値を指定することも **"@**<em>ResDllPath</em>**\\**<em>ResDll</em> **、-**<em>ResID</em>**"** ここで、 *ResDllPath*と*ResDll*パスを指定リソース DLL のファイル名と、*resID*リソース ID を表す負の値は、

この形式を使用して、Windows Multilingual User Interface (MUI) をサポートします。 例は次のとおりです。

```ini
InfoTip = "@%11%\shell32.dll,-22531"
```

<a href="" id="displayresource--resdllpath-resdll--resid"></a>**DisplayResource="**<em>ResDllPath\\ResDll</em>**",**<em>ResID</em>  
この省略可能なエントリでは、[スタート] メニューのショートカットまたはグループの表示名として使用する、ローカライズ可能な文字列を識別する文字列リソースを指定します。

*ResDllPath*と*ResDll*リソース DLL のパスとファイル名を指定し、 *resID*リソース ID を表す正の値は、 例は次のとおりです。

```ini
DisplayResource="%11%\shell32.dll",22019
```

このエントリは、Windows Multilingual User Interface (MUI) をサポートするために使用します。 文字列が指定されたこのエントリを使用しない場合、**名前**エントリが表示されます。

<a name="remarks"></a>注釈
-------

指定された*プロファイル-section 項目*名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)を参照してください。

各*プロファイル-section 項目*作成または 1 つのスタート メニュー項目またはグループを削除する詳細な情報が含まれます。 1 つ以上のメニュー項目または、INF からグループを操作するには、1 つ以上を作成*プロファイル-section 項目*セクションでは、ボックスの一覧と、 **ProfileItems**ディレクティブ。

指定された文字列パラメーターのいずれか、*プロファイル-section 項目*% を使用してエントリを指定できます*strkey*% トークン、」の説明に従って[INF ファイルに関する一般的な構文規則](general-syntax-rules-for-inf-files.md).

<a name="examples"></a>例
--------

次の INF ファイルの抜粋は、使用する方法を示します、*プロファイル-section 項目*電卓を [スタート] メニューに追加します。

```ini
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

次の INF ファイルの抜粋を使用して、同じソフトウェアをインストールする方法を示しています、 **DisplayResource**ローカライズされたメニュー項目を作成するエントリ。

```ini
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

 

 






