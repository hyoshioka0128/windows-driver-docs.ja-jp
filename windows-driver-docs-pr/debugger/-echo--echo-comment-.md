---
title: .echo (コメントのエコー)
description: .Echo コマンドでは、コメント文字列が表示されます。
ms.assetid: 4a291952-695c-4292-8aa5-82d497f0141c
keywords:
- .echo (エコー コメント) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .echo (Echo Comment)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bf1befcd5327060bf1e2c924ee4171ac7f3a4e56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334547"
---
# <a name="echo-echo-comment"></a>.echo (コメントのエコー)


**.Echo**コマンドは、コメント文字列を表示します。

```dbgcmd
.echo String 
.echo "String" 
```

## <a name="span-idddkmetaechocommentdbgspanspan-idddkmetaechocommentdbgspanparameters"></a><span id="ddk_meta_echo_comment_dbg"></span><span id="DDK_META_ECHO_COMMENT_DBG"></span>パラメーター


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *文字列*   
表示するテキストを指定します。 囲むこともできます*文字列*引用符 (")。 引用符を使用するかどうかにかかわらず*文字列*任意の数のスペース、コンマ、および単一引用符 (') を含めることができます。 囲んだ場合*文字列*引用符で含めることができますが、セミコロン、引用符を追加できません。 囲まなかった場合*文字列*引用符で最初の文字を除く任意の場所での引用符を含めるできますが、セミコロンを含めることはできません。

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

 

<a name="remarks"></a>コメント
-------

**.Echo**コマンドにより、デバッガーを表示する*文字列*直後のコマンドを入力します。

**.Echo** (ない場合、セミコロンは、引用符で囲まれた文字列内に発生します)、デバッガーは、セミコロンが発生した場合、コマンドが終了しました。 この制限では、使用することができます **.echo**などの複雑な構造で[条件付きブレークポイント](setting-a-conditional-breakpoint.md)、次の例を示しています。

```dbgcmd
0:000> bp `:143` "j (poi(MyVar)>5) '.echo MyVar Too Big'; '.echo MyVar Acceptable; gc' " 
```

**.Echo**コマンド サーバーをデバッグ出力およびデバッグで互いと通信するクライアントのユーザーの簡単な方法も提供します。 このような状況の詳細については、次を参照してください。[リモート デバッグ セッションを制御する](controlling-a-remote-debugging-session.md)します。

**.Echo**コマンドとは異なります、 [ **$$ (コメント指定子)** ](-----comment-specifier-.md)トークンと[  **\* (コメント行指定子)**](----comment-line-specifier-.md)トークン、これらのトークンが、デバッガーを表示せずに、入力テキストを無視するためです。

 

 





