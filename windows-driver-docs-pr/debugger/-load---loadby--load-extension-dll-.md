---
title: .load、.loadby (拡張機能 DLL の読み込み)
description: Load および loadby コマンドは、新しい拡張 DLL をデバッガーに読み込みます。
ms.assetid: bf54064a-6f30-4f31-a373-fbc643e2660c
keywords:
- . load (拡張 DLL の読み込み) コマンド
- loadby (拡張 DLL の読み込み) コマンド
- 拡張 DLL (. load-. loadby) コマンドの読み込み
- 拡張コマンド (コマンド)、拡張 DLL (. load-. loadby) コマンドの読み込み
- . load,. loadby (拡張 DLL の読み込み) Windows デバッグ
ms.date: 01/30/2020
topic_type:
- apiref
api_name:
- .load, .loadby (Load Extension DLL)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd4128d46781e0558ff58d9489a8652bd3c31ea4
ms.sourcegitcommit: 581fb777a2376854ca12e767d366e2cb79724b73
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84461829"
---
# <a name="load-loadby-load-extension-dll"></a>.load、.loadby (拡張機能 DLL の読み込み)

**Load**および**loadby**コマンドは、新しい拡張 DLL をデバッガーに読み込みます。

```dbgcmd
.load DLLName  
!DLLName.load 
.loadby DLLName ModuleName
```

## <a name="span-idddk_meta_load_extension_dll_dbgspanspan-idddk_meta_load_extension_dll_dbgspanparameters"></a><span id="ddk_meta_load_extension_dll_dbg"></span><span id="DDK_META_LOAD_EXTENSION_DLL_DBG"></span>パラメータ


<span id="_______DLLName______"></span><span id="_______dllname______"></span><span id="_______DLLNAME______"></span>*DLLName*   
読み込むデバッガー拡張 DLL を指定します。 **Load**コマンドを使用する場合、 *DLLName*には完全なパスを含める必要があります。 **. Loadby**コマンドを使用する場合、 *DLLName*にはファイル名のみを含める必要があります。

<span id="_______ModuleName______"></span><span id="_______modulename______"></span><span id="_______MODULENAME______"></span>*ModuleName*   
*DLLName*が指定する拡張 DLL と同じディレクトリにあるモジュールのモジュール名を指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

拡張機能の読み込み、アンロード、および制御の方法の詳細については、「[デバッガー拡張 dll の読み込み](loading-debugger-extension-dlls.md)」を参照してください。

<a name="remarks"></a>解説
-------

**Load**コマンドを使用する場合は、完全なパスを指定する必要があります。

**. Loadby**コマンドを使用する場合、パスは指定しません。 代わりに、デバッガーは、 *ModuleName*パラメーターが指定するモジュールを検出し、そのモジュールのパスを決定して、デバッガーが拡張 DLL を読み込むときにそのパスを使用します。 デバッガーがモジュールを見つけられない場合、または拡張 DLL が見つからない場合は、問題を示すエラーメッセージが表示されます。 指定されたモジュールと拡張 DLL の間にリレーションシップが存在している必要はありません。 したがって、 **loadby**コマンドを使用するのは、長いパスを入力しないようにするための方法にすぎません。

**Load**または**loadby**コマンドが完了したら、読み込まれた拡張機能に格納されているコマンドにアクセスできます。

拡張 DLL を読み込むには、次のいずれかの操作を行います。

- **Load**または**loadby**コマンドを使用します。

- 完全なを発行して拡張機能を実行し**ます。**<em>DLLName</em>**。**<em>Extensioncommand</em>構文。 デバッガーがまだ*DLLName*を読み込んでいない場合は、現在の dll 検索パスに dll がある場合は、この時点で dll が読み込まれます。

Chain コマンドを使用して、読み込まれた内容と現在の DLL 検索パスに関する情報を表示します[。](-chain--list-debugger-extensions-.md)

```dbgcmd
0:000> .chain
Extension DLL search Path:
    C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\WINXP;C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext;C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext\arcade;C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\pri;C:\Program Files (x86)\Windows Kits\10\Debuggers\x64;
Extension DLL chain:
    C:\Windows\Microsoft.NET\Framework64\v4.0.30319\SOS.dll: image 4.8.4084.0, API 1.0.0, built Sun Nov 24 00:38:52 2019
```

たとえば、マネージコードの SOS は、上に示した Dll の検索パスに含まれていません。そのため、その dll を読み込むには、load コマンドを完全なパスで使用します。  

```dbgcmd
0:000> .load C:\Windows\Microsoft.NET\Framework64\v4.0.30319\SOS.dll
```
