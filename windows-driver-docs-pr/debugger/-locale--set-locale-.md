---
title: .locale (ロケールの設定)
description: .Locale コマンドでは、ロケールを設定または現在のロケールを表示します。
ms.assetid: 66c2a522-886f-41ef-ab90-176a3e0b7d88
keywords:
- .locale (ロケールを設定する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .locale (Set Locale)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 39cc03ebcdc74b86e7d471cccc62583a55d20186
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578249"
---
# <a name="locale-set-locale"></a>.locale (ロケールの設定)


**.Locale**コマンドは、ロケールを設定または現在のロケールが表示されます。

```dbgcmd
.locale [Locale] 
```

## <a name="span-idddkmetasetlocaledbgspanspan-idddkmetasetlocaledbgspanparameters"></a><span id="ddk_meta_set_locale_dbg"></span><span id="DDK_META_SET_LOCALE_DBG"></span>パラメーター


<span id="_______Locale______"></span><span id="_______locale______"></span><span id="_______LOCALE______"></span> *ロケール*   
目的のロケールを指定します。 このパラメーターを省略した場合、デバッガーには、現在のロケールが表示されます。

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

ロケールの詳細については、次を参照してください。、 **setlocale**日常的なリファレンス ページです。

<a name="remarks"></a>コメント
-------

ロケールでは、Unicode 文字列の表示方法を制御します。

次の例に示す、 **.locale**コマンド。

```dbgcmd
kd> .locale
Locale: C

kd> .locale E
Locale: English_United States.1252

kd> .locale c
Locale: Catalan_Spain.1252

kd> .locale C
Locale: C
```

 

 





