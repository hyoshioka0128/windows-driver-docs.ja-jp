---
title: .bugcheck (バグ チェック データを表示する)
description: .Bugcheck コマンドでは、ターゲット コンピューター上のバグ チェックからデータを表示します。
ms.assetid: 4b453b5a-4a3c-4056-92e7-b6a17f987fa4
keywords:
- .bugcheck (バグ チェック データを表示する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .bugcheck (Display Bug Check Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a24198184af88054b599c230d8e308bdd3d882fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551404"
---
# <a name="bugcheck-display-bug-check-data"></a>.bugcheck (バグ チェック データを表示する)


**.Bugcheck**バグからデータを確認して、ターゲット コンピューターで、コマンドが表示されます。

```dbgsyntax
    .bugcheck 
```

## <span id="ddk_meta_display_bug_check_data_dbg"></span><span id="DDK_META_DISPLAY_BUG_CHECK_DATA_DBG"></span>


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

バグ チェックの詳細については、次を参照してください。[バグ チェック (ブルー スクリーン)](bug-checks--blue-screens-.md)します。 個々 のバグ チェックの説明は、次を参照してください。、[バグ チェック コード参照](bug-check-code-reference2.md)セクション。

<a name="remarks"></a>注釈
-------

このコマンドは、現在のバグ チェックのデータを表示します。 (このバグ チェックのデータがアクセスできる、クラッシュしたマシンが再起動されるまで。)

使用して、32 ビット システムのバグ チェックのデータを表示することも**dd NT!KiBugCheckData L5**、またはを使用して 64 ビット システムで**dq NT!KiBugCheckData L5**します。 ただし、.bugcheck のコマンドは、信頼性が高く、いくつかのシナリオで動作するためを[ **d\* (表示メモリ)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドではありません (ユーザー モードのミニダンプ) など。

[ **! 分析**](-analyze.md)拡張機能コマンドでは、バグ チェックが行われた後にも役立ちます。

 

 





