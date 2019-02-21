---
title: mui
description: Mui 拡張機能には、多言語ユーザー インターフェイス (MUI) のキャッシュ情報が表示されます。 MUI の実装が、Windows Vista で強化されました。
ms.assetid: f485450f-0dd2-4f1c-85fe-dbf272c2dbae
keywords:
- 多言語ユーザー インターフェイス
- mui は Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- mui
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ea2ef45f04ede7e83ae51252ca7cffb655da1f88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539288"
---
# <a name="mui"></a>! mui


**! Mui**拡張機能には、Multilingual User Interface (MUI) のキャッシュ情報が表示されます。 

```dbgcmd
!mui -c
!mui -s
!mui -r ModuleAddress
!mui -i
!mui -f
!mui -t
!mui -u
!mui -d ModuleAddress
!mui -e ModuleAddress
!mui -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
により、言語識別子 (ID)、モジュールへのポインター、リソースの構成データへのポインター、および各モジュールに関連付けられている MUI DLL へのポインターを含める出力します。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
(カーネル モードのみ)モジュールの完全ファイル パス、モジュールごとに関連付けられている MUI DLL など、表示をによりします。

<span id="_______-r________ModuleAddress______"></span><span id="_______-r________moduleaddress______"></span><span id="_______-R________MODULEADDRESS______"></span> **-r** **** *ModuleAddress*   
あるモジュールの構成データがリソース*ModuleAddress*に表示されます。 これには、ファイルの種類、チェックサム値、およびリソースの種類が含まれます。

<span id="_______-i______"></span><span id="_______-I______"></span> **-i**   
により、インストールされている、ライセンス購入 MUI 言語とその関連情報を含める出力します。

<span id="_______-f______"></span><span id="_______-F______"></span> **-f**   
により、ローダーのマージされた言語フォールバック リストを含めるに出力します。

<span id="_______-t______"></span><span id="_______-T______"></span> **-t**   
により、スレッドの優先言語を含める出力します。

<span id="_______-u______"></span><span id="_______-U______"></span> **-u**   
により、現在のスレッド ユーザー UI の言語設定を含める出力します。

<span id="_______-d_ModuleAddress______"></span><span id="_______-d_moduleaddress______"></span><span id="_______-D_MODULEADDRESS______"></span> **-d** **** *ModuleAddress*   
により、モジュールに含まれているリソースを含める出力*ModuleAddress*します。

<span id="_______-e_ModuleAddress______"></span><span id="_______-e_moduleaddress______"></span><span id="_______-E_MODULEADDRESS______"></span> **-e** **** *ModuleAddress*   
により、含まれているリソースの型にあるモジュールを含む出力*ModuleAddress*します。

<span id="_______-_______"></span> **-?**   
デバッガー コマンド ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows Vista 以降</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

MUI およびリソースの構成データの形式については、Microsoft Windows SDK のドキュメントを参照してください。

 

 





