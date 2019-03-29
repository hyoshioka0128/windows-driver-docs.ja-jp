---
title: .symfix (シンボル ストア パスの設定)
description: .Symfix コマンドでは、Microsoft のシンボル ストアをポイントするシンボル パスが自動的に設定します。
ms.assetid: 9ad80217-e2d1-4776-a620-f2735b2c8f84
keywords:
- シンボル ストア パス (.symfix) コマンドを設定します。
- SymSrv、シンボル ストア パスの設定 (.symfix) コマンド
- .symfix (セット シンボル ストア パス) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .symfix (Set Symbol Store Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 422fa5e208c6d4714f74cdd6470b993404965e78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570685"
---
# <a name="symfix-set-symbol-store-path"></a>.symfix (シンボル ストア パスの設定)


**.Symfix**コマンドは、Microsoft のシンボル ストアをポイントするシンボル パスを自動的に設定します。

```dbgcmd
.symfix[+] [LocalSymbolCache]
```

## <a name="span-idddkmetasetsymbolstorepathdbgspanspan-idddkmetasetsymbolstorepathdbgspanparameters"></a><span id="ddk_meta_set_symbol_store_path_dbg"></span><span id="DDK_META_SET_SYMBOL_STORE_PATH_DBG"></span>パラメーター


<span id="______________"></span> **+**   
既存のシンボル パスに追加するには、Microsoft シンボル ストア パスをによりします。 これが含まれていない場合は、既存のシンボル パスが置き換えられます。

<span id="_______LocalSymbolCache______"></span><span id="_______localsymbolcache______"></span><span id="_______LOCALSYMBOLCACHE______"></span> *LocalSymbolCache*   
ローカル シンボル キャッシュとして使用するディレクトリを指定します。 このディレクトリが存在しない場合は、シンボル サーバーは、ファイルのコピーを開始時に作成されます。 場合*LocalSymbolCache*は省略すると、デバッガーのインストール ディレクトリの sym サブディレクトリが使用されます。

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

詳細については、次を参照してください。[シンボル サーバーを使用して、シンボル ストア](symbol-stores-and-symbol-servers.md)します。

<a name="remarks"></a>コメント
-------

次の例は、使用する方法を示します **.symfix** Microsoft シンボル ストアを指す新しいシンボル パスを設定します。

```dbgcmd
3: kd> .symfix c:\myCache
3: kd> .sympath
Symbol search path is: srv*
Expanded Symbol search path is: cache*c:\myCache;SRV*https://msdl.microsoft.com/download/symbols
```

次の例は、使用する方法を示します **.symfix +** Microsoft シンボル ストアを指定するパスでは、既存のシンボル パスを追加します。

```dbgcmd
3: kd> .sympath
Symbol search path is: c:\someSymbols
Expanded Symbol search path is: c:\somesymbols
3: kd> .symfix+ c:\myCache
3: kd> .sympath
Symbol search path is: c:\someSymbols;srv*
Expanded Symbol search path is: c:\somesymbols;cache*c:\myCache;SRV*https://msdl.microsoft.com/download/symbols
```

 

 





