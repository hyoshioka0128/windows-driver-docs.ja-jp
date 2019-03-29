---
title: .enable_unicode (Unicode の表示を有効にする)
description: .Enable_unicode コマンドでは、デバッガーが Unicode 文字列として、USHORT ポインターと配列を表示するかどうかを指定します。
ms.assetid: bb029ff4-1802-4d91-ba4b-9db10fa7c055
keywords:
- Unicode の表示 (.enable_unicode) コマンドを有効にします。
- UNICODE_STRING 構造体
- .enable_unicode (Unicode 表示を有効にする) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .enable_unicode (Enable Unicode Display)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bbab1c0d18f3d1adeba498da7f58ed2f9ec2d790
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580192"
---
# <a name="enableunicode-enable-unicode-display"></a>リストア\_unicode (Unicode 表示を有効にする)


**リストア\_unicode**コマンドでは、デバッガーが Unicode 文字列として、USHORT ポインターと配列を表示するかどうかを指定します。

```dbgcmd
.enable_unicode 0 
.enable_unicode 1
```

## <a name="span-idddkmetaenableunicodedisplaydbgspanspan-idddkmetaenableunicodedisplaydbgspanparameters"></a><span id="ddk_meta_enable_unicode_display_dbg"></span><span id="DDK_META_ENABLE_UNICODE_DISPLAY_DBG"></span>パラメーター


<span id="_______0______"></span> **0**   
短整数としてすべての 16 ビット (USHORT) 配列とポインターが表示されます。 これは、デバッガーの既定の動作です。

<span id="_______1______"></span> **1**   
すべての 16 ビット (USHORT) 配列とポインターを Unicode 文字列として表示されます。

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

**リストア\_unicode**コマンドの出力に影響する、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンド。

、WinDbg で、**リストア\_unicode**コマンドの表示にも影響、 [[ローカル] ウィンドウ](locals-window.md)とウォッチ ウィンドウ。 これらのウィンドウが自動的に更新を発行した後**リストア\_unicode**します。

選択することもクリアまたは**表示の 16 ビット値**ローカルまたはウォッチのショートカット メニューでは Unicode として USHORT 配列とポインターの表示形式を指定するにはウィンドウ。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**ds、dS (表示文字列)**](ds--ds--display-string-.md)

 

 






