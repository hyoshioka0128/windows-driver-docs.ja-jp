---
title: .fiber (ファイバー コンテキストの設定)
description: .Fiber コマンドでは、どのファイバーがファイバー コンテキストの使用を指定します。
ms.assetid: 37473c90-018c-417f-a2b2-3723b9d03ca7
keywords:
- Set ファイバー コンテキスト (.fiber) コマンド
- コンテキスト、ファイバー コンテキストの設定 (.fiber) コマンド
- ファイバー
- .fiber (ファイバー コンテキストの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fiber (Set Fiber Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6a637c508e4fb708514cedc6758bc3f8e14904a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334477"
---
# <a name="fiber-set-fiber-context"></a>.fiber (ファイバー コンテキストの設定)


**.Fiber**コマンドでは、どのファイバーがファイバー コンテキストの使用を指定します。

```dbgcmd
.fiber [Address]
```

## <a name="span-idddkmetasetfibercontextdbgspanspan-idddkmetasetfibercontextdbgspanparameters"></a><span id="ddk_meta_set_fiber_context_dbg"></span><span id="DDK_META_SET_FIBER_CONTEXT_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ファイバーのアドレスを指定します。 このパラメーターを省略または 0 を指定する場合は、ファイバー コンテキストが現在ファイバーにリセットされます。

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

プロセスのコンテキスト、レジスタのコンテキストとローカル コンテキストの詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

 

 





