---
title: .settings (デバッグ設定の指定)
description: .Settings コマンド設定、変更が表示されます、読み込みますおよび Debugger.Settings 名前空間の設定を保存します。
ms.assetid: DAD68FA5-21EF-4A5C-8E5E-0C763CD28C44
keywords:
- .settings (デバッグの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .settings (Set Debug Settings)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed27d34f56ab44d8b9e2170a02cae120d218eb4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334247"
---
# <a name="settings-set-debug-settings"></a>.settings (デバッグ設定の指定)


**.Settings**コマンド設定、変更が表示されます、読み込みおよび Debugger.Settings 名前空間の設定を保存します。

```dbgcmd
.settings set  namespace.setting=value
.settings set namespace.setting+=value 
.settings save [file path] 
.settings load file path
.settings list [namespace][-v]
.settings help   
```

## <a name="span-idddkmetasetsymbolpathdbgspanspan-idddkmetasetsymbolpathdbgspanparameters"></a><span id="ddk_meta_set_symbol_path_dbg"></span><span id="DDK_META_SET_SYMBOL_PATH_DBG"></span>パラメーター


**.settings パラメーターを設定します。**

<span id="_______NAMESPACE.SETTING_VALUE______"></span> **namespace.setting=value**   
設定の変更または設定します。 C: たとえば、エスケープ スラッシュを使用して、ファイルのパスを指定するときに\\\\シンボル\\\\します。

例:

`.settings set Display.PreferDMLOutput=false`

`.settings set Sources.DisplaySourceLines=true`

`.settings set Symbols.Sympath="C:\\Symbols\\"`

<span id="_______NAMESPACE.SETTING__VALUE______"></span> **namespace.setting+=value**   
新しい値が、指定に追加されます (なく置き換える) 以前の値。

以下に例を示します。

`.settings set Extensions.ExtensionSearchPath+=";C:\\MyExtension\\"`

**パラメーターを保存 .setting**

<span id="_______file_path______"></span><span id="_______FILE_PATH______"></span> **ファイルのパス**   
指定した XML ファイルに Debugger.Settings 名前空間には、すべての値を保存します。

<span id="_______none______"></span><span id="_______NONE______"></span> **[なし]**   
ファイル パスが指定されていない場合、設定は、最後が読み込まれたまたは保存するファイルに保存します。 前のファイルが存在しない場合が config.xml という名前のファイルを作成して実行可能ファイルのデバッガーがから読み込まれたディレクトリにします。

**.setting パラメーターの読み込み**

<span id="_______file_path______"></span><span id="_______FILE_PATH______"></span> **ファイルのパス**   
XML 設定ファイルからすべての設定を読み込みます。 設定を読み込んで、そのファイルで定義されている設定のみが変更されます。 そのファイルに表示されない、以前に読み込まれたまたは変更された設定は変更されません。 このファイルは、次の保存または読み込み操作しないと、既定の保存パスとして扱われます。

**.setting リスト パラメーター**

<span id="_______namespace______"></span><span id="_______NAMESPACE______"></span> **namespace**   
指定した名前空間とその値のすべての設定を一覧表示します。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
– V フラグにより、表示される設定の説明。

**.setting ヘルプ パラメーター**

<span id="_______None______"></span><span id="_______none______"></span><span id="_______NONE______"></span> **[なし]**   
すべてのデバッガーの名前空間とその説明の設定の一覧を表示します。

<span id="_______Namespace______"></span><span id="_______namespace______"></span><span id="_______NAMESPACE______"></span> **Namespace**   
指定した名前空間とその説明のすべての設定を一覧表示します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

起動時、デバッガーは、デバッガーの実行可能ファイルがディレクトリに config.xml から、すべての設定を読み込みます。 デバッグ セッション全体では、以前の設定コマンドを使用して設定を変更できます (.sympath など .prefer\_dml) または新しい .settings コマンド。 '保存 .settings' を使用すると、設定の構成ファイルに設定を保存します。 次のコマンドを使用して、自動保存を有効にすることができます。

`.settings set AutoSaveSettings=true`

自動保存が有効にすると Debugger.Settings 名前空間の設定が自動的に保存、デバッガーを終了するときにします。

<a name="remarks"></a>注釈
-------

他のユーザーがそのデバッグ設定を複製すると、デバッグ xml 設定ファイルを交換することができます。

 

 





