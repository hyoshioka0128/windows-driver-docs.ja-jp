---
title: dg (セレクターの表示)
description: Dg コマンドは、セグメントの記述子を指定されたセレクターを示しています。
ms.assetid: bf680931-f4f9-4b72-bb25-42d095514d2a
keywords:
- 配布グループ (表示セレクター) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dg (Display Selector)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e4e0bc8c6e5795c8762a371b63732361aa5cf354
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582004"
---
# <a name="dg-display-selector"></a>dg (セレクターの表示)


**Dg**コマンドは、指定されたセレクターのセグメントの記述子を表示します。

```dbgcmd
dg FirstSelector [LastSelector]
```

## <a name="span-idddkcmddisplayselectordbgspanspan-idddkcmddisplayselectordbgspanparameters"></a><span id="ddk_cmd_display_selector_dbg"></span><span id="DDK_CMD_DISPLAY_SELECTOR_DBG"></span>パラメーター


<span id="_______FirstSelector______"></span><span id="_______firstselector______"></span><span id="_______FIRSTSELECTOR______"></span> *FirstSelector*   
表示される最初のセレクターの 16 進数のセレクターの値を指定します。

<span id="_______LastSelector______"></span><span id="_______lastselector______"></span><span id="_______LASTSELECTOR______"></span> *LastSelector*   
表示される最後のセレクターの 16 進数のセレクターの値を指定します。 これを省略すると、1 つだけのセレクターが表示されます。

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
<td align="left"><p>x86、Itanium</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

このコマンドでは、256 個のセレクターを表示できます。

一般的なセレクターの値は次のとおりです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ID</th>
<th align="left">decimal</th>
<th align="left">16 進数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KGDT_NULL</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_R0_CODE</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p>0x08</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KGDT_R0_DATA</p></td>
<td align="left"><p>16</p></td>
<td align="left"><p>0x10</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_R3_CODE</p></td>
<td align="left"><p>24</p></td>
<td align="left"><p>0x18</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KGDT_R3_DATA</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>0x20</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_TSS</p></td>
<td align="left"><p>40</p></td>
<td align="left"><p>0x28</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KGDT_R0_PCR</p></td>
<td align="left"><p>48</p></td>
<td align="left"><p>0x30</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_R3_TEB</p></td>
<td align="left"><p>56</p></td>
<td align="left"><p>0x38</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KGDT_VDM_TILE</p></td>
<td align="left"><p>64</p></td>
<td align="left"><p>0x40</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_LDT</p></td>
<td align="left"><p>72</p></td>
<td align="left"><p>0x48</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KGDT_DF_TSS</p></td>
<td align="left"><p>80</p></td>
<td align="left"><p>0x50 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_NMI_TSS</p></td>
<td align="left"><p>88</p></td>
<td align="left"><p>0x58</p></td>
</tr>
</tbody>
</table>

 

 

 





