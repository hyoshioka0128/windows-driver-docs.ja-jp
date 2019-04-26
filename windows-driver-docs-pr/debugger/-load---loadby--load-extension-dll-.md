---
title: .load、.loadby (拡張機能 DLL の読み込み)
description: .Load と .loadby コマンドは、デバッガーに、新しい拡張 DLL を読み込みます。
ms.assetid: bf54064a-6f30-4f31-a373-fbc643e2660c
keywords:
- .load (拡張 DLL の読み込み) コマンド
- loadby (拡張 DLL の読み込み) コマンド
- 拡張 DLL を読み込む (.load - .loadby) コマンド
- 拡張機能のコマンド (コマンド)、拡張 DLL の読み込み (.load - .loadby) コマンド
- .load、.loadby (拡張 DLL の読み込み) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .load, .loadby (Load Extension DLL)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c559509c916563fe1f9fedc459503c407b55fd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336512"
---
# <a name="load-loadby-load-extension-dll"></a>.load、.loadby (拡張機能 DLL の読み込み)


**.Load**と **.loadby**コマンドでは、新しい拡張 DLL を読み込む、デバッガーを起動します。

```dbgcmd
.load DLLName  
!DLLName.load 
.loadby DLLName ModuleName
```

## <a name="span-idddkmetaloadextensiondlldbgspanspan-idddkmetaloadextensiondlldbgspanparameters"></a><span id="ddk_meta_load_extension_dll_dbg"></span><span id="DDK_META_LOAD_EXTENSION_DLL_DBG"></span>パラメーター


<span id="_______DLLName______"></span><span id="_______dllname______"></span><span id="_______DLLNAME______"></span> *DLLName*   
デバッガーの拡張 DLL の読み込みを指定します。 使用する場合、 **.load**コマンド、 *DLLName*の完全なパスを含める必要があります。 使用する場合、 **.loadby**コマンド、 *DLLName*ファイル名のみを含める必要があります。

<span id="_______ModuleName______"></span><span id="_______modulename______"></span><span id="_______MODULENAME______"></span> *ModuleName*   
拡張 DLL と同じディレクトリにあるモジュールのモジュール名を指定する*DLLName*を指定します。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

読み込み、アンロード、およびコントロール拡張機能する方法の詳細については、次を参照してください。[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)します。

<a name="remarks"></a>注釈
-------

使用すると、 **.load**コマンド、完全なパスを指定する必要があります。

使用すると、 **.loadby**コマンド、パスを指定しないでください。 代わりに、デバッガーのモジュールを検出、 *ModuleName*パラメーターを指定します、そのモジュールのパスを決定およびデバッガー拡張 DLL の読み込み時にそのパスを使用します。 モジュールが見つからないか、拡張 DLL が見つからない場合、エラー メッセージが表示される場合、問題を指定します。 存在する必要はありませんおよび拡張 DLL の指定したモジュール間の関係があります。 使用して、 **.loadby**コマンドは、そのため、長いパスを入力しなくて済むようにする方法だけです。

後に、 **.load**または **.loadby**コマンドが完了したら、読み込まれた拡張機能に格納されているコマンドにアクセスすることができます。

拡張 DLL を読み込むには、次のいずれかの操作を行います。

- 使用して、 **.load**または **.loadby**コマンド。

- 完全なを発行して、拡張機能を実行 **!**<em>DLLName</em>**.**<em>ExtensionCommand</em>構文。 デバッガーがまだ読み込まれていない場合*DLLName*.dll、この時点で、DLL を読み込みます。

 

 





