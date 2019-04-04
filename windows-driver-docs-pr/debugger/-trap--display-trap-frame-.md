---
title: .trap (表示トラップ フレーム)
description: .Trap コマンドでは、トラップ フレームの登録状態を表示しもレジスタのコンテキストを設定します。
ms.assetid: c53177ad-243c-4276-8602-2edc14b44251
keywords:
- トラップ フレーム (.trap) コマンドが表示されます。
- トラップ フレーム
- .trap (表示トラップ フレーム) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .trap (Display Trap Frame)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4d8e6a82cdbcd316ec278da383ec8a5777645f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539244"
---
# <a name="trap-display-trap-frame"></a>.trap (表示トラップ フレーム)


**.Trap**コマンドは、トラップ フレームの登録状態を表示しもレジスタのコンテキストを設定します。

```dbgcmd
.trap [Address]
```

## <a name="span-idddkmetadisplaytrapframedbgspanspan-idddkmetadisplaytrapframedbgspanparameters"></a><span id="ddk_meta_display_trap_frame_dbg"></span><span id="DDK_META_DISPLAY_TRAP_FRAME_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ターゲット システムでトラップ フレームの 16 進数のアドレス。 アドレスを省略すること、トラップ フレーム情報は表示されませんが、レジスタのコンテキストをリセットには。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
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

<a name="remarks"></a>注釈
-------

**.Trap**コマンドには、指定されたトラップのフレームの重要なレジスタが表示されます。

このコマンドでは、レジスタのコンテキストとして指定したコンテキスト レコードを使用してカーネル デバッガーもように指示します。 このコマンドを実行すると、デバッガーは、このスレッドの最も重要なレジスタとスタック トレースへのアクセスがあります。 別のレジスタ コンテキスト コマンドを使用して、またはを実行するターゲットを許可するまで保持されるこのレジスタのコンテキスト ([**.thread**](-thread--set-register-context-.md)、 [ **.cxr** ](-cxr--display-context-record-.md)、または **.trap**)。 参照してください[登録コンテキスト](changing-contexts.md#register-context)の完全な詳細情報。

この拡張機能には、0 xa、0x7F のバグ チェックをデバッグするときに通常使用されます。 詳細と例では、次を参照してください。 [ **0 xa のバグ チェック**](bug-check-0xa--irql-not-less-or-equal.md) (IRQL\_いない\_少ない\_または\_等しくない)。

 

 





