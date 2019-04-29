---
title: .ecxr (例外コンテキスト レコードの表示)
description: .Ecxr コマンドには、現在の例外に関連付けられているコンテキスト レコードが表示されます。
ms.assetid: 020dfa99-ba25-4af3-929a-143d5c91ad87
keywords:
- 例外コンテキスト レコード (.cxr) コマンドが表示されます。
- 例外、例外コンテキスト レコード
- .ecxr (例外コンテキスト レコードの表示) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .ecxr (Display Exception Context Record)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5776f993fd21050a6e8c6ef44c78e568aec8d259
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336772"
---
# <a name="ecxr-display-exception-context-record"></a>.ecxr (例外コンテキスト レコードの表示)


**.Ecxr**コマンドは、現在の例外に関連付けられているコンテキスト レコードを表示します。

```dbgcmd
.ecxr
```

## <span id="ddk_meta_display_exception_context_record_dbg"></span><span id="DDK_META_DISPLAY_EXCEPTION_CONTEXT_RECORD_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>クラッシュ ダンプのみ (ミニダンプのみ)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

レジスタのコンテキストとその他のコンテキストの設定の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

<a name="remarks"></a>注釈
-------

**.Ecxr**コマンドは、現在の例外のコンテキスト情報を検索し、指定したコンテキスト レコードの重要なレジスタを表示します。

このコマンドでは、レジスタのコンテキストとして現在の例外に関連付けられているコンテキスト レコードを使用してデバッガーもように指示します。 実行した後 **.ecxr**、最も重要なレジスタとスタック トレースをこのスレッドをデバッガーにアクセスできます。 実行、現在のプロセスまたはスレッドを変更または別のレジスタ コンテキスト コマンドを使用してターゲットを有効にするまで、このレジスタのコンテキストが永続化 ([**.cxr** ](-cxr--display-context-record-.md)または **.ecxr**). レジスタのコンテキストの詳細については、次を参照してください。[登録コンテキスト](changing-contexts.md#register-context)します。

[ **.Excr** ](-excr--display-exception-context-record-.md)コマンドは同一の機能が、シノニム コマンド。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**.excr**](-excr--display-exception-context-record-.md)

 

 






