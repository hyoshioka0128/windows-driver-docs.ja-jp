---
title: .crash (システム クラッシュの強制実行)
description: .Crash コマンドでは、バグ チェックを発行する対象のコンピュータを実行します。
ms.assetid: 625d174d-7011-4b15-aad7-1b39aa3742a4
keywords:
- .crash (force システム クラッシュ) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .crash (Force System Crash)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8ef8a05ce1fc60eb642588604c148763d4d77f85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574302"
---
# <a name="crash-force-system-crash"></a>.crash (システム クラッシュの強制実行)


**.Crash**コマンドのバグ チェックが発行する対象のコンピュータを実行します。

```dbgsyntax
.crash
```

## <span id="ddk_meta_force_system_crash_dbg"></span><span id="DDK_META_FORCE_SYSTEM_CRASH_DBG"></span>


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
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

システム障害の後で使用できるオプションの説明と関連するコマンドの概要については、[クラッシュし、ターゲット コンピューターを再起動](crashing-and-rebooting-the-target-computer.md)を参照してください。

<a name="remarks"></a>コメント
-------

このコマンドには、ターゲット コンピューターがクラッシュするとすぐにされます。

バグ チェック ハンドラーでしている場合は使用しないで **.crash**します。 使用[ **g (移動)** ](g--go-.md)代わりに、クラッシュ ダンプを生成すると、ハンドラーの実行を続行します。

クラッシュ ダンプを有効になっているかどうかに、カーネル モードのダンプ ファイルが書き込まれます。 参照してください[カーネル モードのダンプ ファイルを作成する](creating-a-kernel-mode-dump-file.md)詳細についてはします。

 

 





