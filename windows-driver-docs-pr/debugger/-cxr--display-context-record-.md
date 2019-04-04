---
title: .cxr (コンテキスト レコードの表示)
description: .Cxr コマンドには、指定したアドレスに保存されたコンテキスト レコードが表示されます。 また、レジスタのコンテキストを設定します。
ms.assetid: 0e882639-6029-4512-8d46-050228e95cb6
keywords:
- コンテキスト レコード (.cxr) コマンドが表示されます。
- コンテキスト レコード
- .cxr (コンテキスト レコードの表示) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .cxr (Display Context Record)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6fcedc429b537dea85194ce04ef331fa576d7d62
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580012"
---
# <a name="cxr-display-context-record"></a>.cxr (コンテキスト レコードの表示)


**.Cxr**コマンドには、指定したアドレスに保存されたコンテキスト レコードが表示されます。 また、レジスタのコンテキストを設定します。

```dbgsyntax
.cxr [Options] [Address]  
```

## <a name="span-idddkmetadisplaycontextrecorddbgspanspan-idddkmetadisplaycontextrecorddbgspanparameters"></a><span id="ddk_meta_display_context_record_dbg"></span><span id="DDK_META_DISPLAY_CONTEXT_RECORD_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の組み合わせを指定できます。

<span id="_f_Size"></span><span id="_f_size"></span><span id="_F_SIZE"></span>**/f** **** *サイズ*  
強制的にコンテキストのサイズの値と等しい*サイズ*、(バイト単位)。 これは、便利な場合、コンテキストと一致しません - 実際のターゲットなど、x86 を使用する場合の中に 64 ビット ターゲット コンテキスト*WOW64*デバッグします。 無効または非整合なサイズが指定されている場合は、「コンテキストを正規の形式に変換できません」エラーが表示されます。

<span id="_w"></span><span id="_W"></span>**/w**  
メモリに現在のコンテキストに書き込み、それが書き込まれる場所のアドレスを表示します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
システム コンテキスト レコードのアドレス。

アドレスを省略すると、コンテキスト レコードの情報は表示されませんが、レジスタのコンテキストをリセットには。

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

レジスタのコンテキストとその他のコンテキストの設定の詳細については、[変更コンテキスト](changing-contexts.md)を参照してください。

<a name="remarks"></a>コメント
-------

コンテキスト レコードからの情報は、ハンドルされない例外が発生しました、正確なスタック トレースをご利用いただけませんシステム停止のデバッグを支援するために使用できます。 **.Cxr**コマンドには、指定したコンテキスト レコードの重要なレジスタが表示されます。

このコマンドでは、レジスタのコンテキストとして指定したコンテキスト レコードを使用するデバッガーもように指示します。 このコマンドを実行すると、デバッガーは、このスレッドの最も重要なレジスタとスタック トレースへのアクセスがあります。 別のレジスタ コンテキスト コマンドを使用して、またはを実行するターゲットを許可するまで保持されるこのレジスタのコンテキスト ([**.thread**](-thread--set-register-context-.md)、 [ **.ecxr** ](-ecxr--display-exception-context-record-.md)、 [ **.trap** ](-trap--display-trap-frame-.md) 、または **.cxr**もう一度)。 ユーザー モードでもリセットされます、現在のプロセスまたはスレッドを変更する場合。 参照してください[登録コンテキスト](changing-contexts.md#register-context)詳細についてはします。

**.Cxr** 0x1E のバグ チェックをデバッグする多くの場合、コマンドを使用します。 詳細と例では、次を参照してください。 [**バグ チェック 0x1E** ](bug-check-0x1e--kmode-exception-not-handled.md) (KMODE\_例外\_いない\_処理済み)。

**.Cxr/w**コマンドは、コンテキストをメモリに書き込むし、格納されているアドレスが表示されます。 このアドレスに渡すことが[ **.apply\_dbp (適用データ ブレークポイントのコンテキストに)** ](-apply-dbp--apply-data-breakpoint-to-context-.md)データ ブレークポイントをこのコンテキストに適用する必要がある場合。

 

 





