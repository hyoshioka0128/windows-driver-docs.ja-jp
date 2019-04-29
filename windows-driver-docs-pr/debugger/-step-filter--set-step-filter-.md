---
title: .step_filter (ステップ フィルターの設定)
description: .Step_filter コマンドは、トレースする場合はスキップされます (ステップ オーバー) 関数の一覧を作成します。
ms.assetid: 9ce2bed4-fac0-4537-a129-7cb9f1e8725e
keywords:
- .step_filter (ステップ フィルターの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .step_filter (Set Step Filter)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a39a8bf4fe882844e31ee9f23d7756017f7e70ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334254"
---
# <a name="stepfilter-set-step-filter"></a>.step\_フィルター (ステップ フィルターの設定)


**.Step\_フィルター**をトレースする場合、コマンドがスキップされます (ステップ オーバー) 関数の一覧を作成します。 これにより、コードをトレースし、特定の関数のみをスキップすることができます。 コントロールの 1 つの行に複数の関数呼び出しがある場合にステップ インする元のモードでも使用できます。

```dbgcmd
.step_filter "FilterList" 
.step_filter /c 
.step_filter 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_FilterList_"></span><span id="_filterlist_"></span><span id="_FILTERLIST_"></span>**"**<em>Filterlist 内</em>**"**  
ステップ オーバーする関数に関連付けられているシンボルを指定します。 *Filterlist 内*セミコロンで区切られたテキスト パターンの任意の数を含めることができます。 これらの各パターンのさまざまなワイルドカードや; 指定子を含めることができます。参照してください[文字列のワイルドカード構文](string-wildcard-syntax.md)詳細についてはします。 記号では、これらのパターンの少なくとも 1 つと一致する関数は、トレース中にステップ オーバーされます。 毎回 **"**<em>filterlist 内</em>**"** が使用すると、以前のフィルター一覧のすべては破棄され、新しいリストに完全に置き換えられます。

<span id="________c______"></span><span id="________C______"></span> **/c**   
フィルターの一覧をクリアします。

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

 

<a name="remarks"></a>注釈
-------

任意のパラメーターを指定せず **.step\_フィルター**現在フィルター一覧を表示します。

Trace コマンドでは通常、(たとえば、 [ **t** ](t--trace-.md)や、windbg[デバッグ | にステップ イン](debug---step-into.md)ボタン![、ステップ イン ボタンのスクリーン ショット](images/tbinto.png)) トレース関数呼び出し。 ただし、シンボルに関連付けられている場合、呼び出される関数は一致で指定されたパターン*filterlist 内*、関数がステップ オーバー--ステップ コマンド場合と (たとえば、 [ **p**](p--step-.md)) 使用されていた。

命令ポインターがフィルターの一覧に記載されているコード内にある場合は、トレースまたはステップ コマンドが関数をステップ アウトこの、このような[ **gu** ](gu--go-up-.md)コマンドや、WinDbg**ステップ アウト**ボタンをクリックします。 もちろん、このフィルターできなくなりますこのようなコードに最初の段階で、トレースがされているため、フィルターを変更またはブレークポイントにヒットした場合にのみ発生これは。

たとえば、次のコマンドでは、CRT のすべての呼び出しをスキップするトレース コマンドが発生します。

```dbgcmd
.step_filter "msvcrt!*" 
```

**.Step\_フィルター**コマンドは、元のモードでデバッグするときに最も役に立つ、1 つのソース行に複数の関数を呼び出す可能性があるためです。 [ **P** ](p--step-.md)と[ **t** ](t--trace-.md)コマンドを使用してこれらの関数呼び出しを分離することはできません。

たとえば、次の行で、 [ **t** ](t--trace-.md)コマンドは、GetTickCount と、printf の両方にステップ イン中に、 [ **p** ](p--step-.md)コマンドでは、手順両方の関数呼び出し。

```dbgcmd
printf( "%x\n", GetTickCount() );
```

**.Step\_フィルター**コマンドでは、まだ他のトレース中にこれらの呼び出しのいずれかをフィルター処理することができます。

関数が記号で識別され、ため、1 つのフィルターは、モジュール全体を含めることができます。 フレームワークの機能 - たとえば、Microsoft Foundation Classes (MFC) や Active Template Library (ATL) の呼び出しをフィルター処理するこのことができます。

モードのアセンブリで、デバッグ時に各呼び出しは、別の行にステップ実行またはトレースするかどうかを選択できるように 1 行ずつ。 したがって **.step\_フィルター**はモードのアセンブリで非常に役に立ちません。

 

 





