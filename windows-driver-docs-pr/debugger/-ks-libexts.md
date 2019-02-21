---
title: ks.libexts
description: Ks.libexts 拡張機能は、拡張機能モジュールに静的にリンクされているライブラリの Microsoft 提供の拡張機能へのアクセスを提供します。
ms.assetid: 03328041-9922-4367-b6e9-d822a9c03f32
keywords:
- デバッグ ks.libexts Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.libexts
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 05c2e88f471b2aafa8b82a7d451103a5dcb130fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528085"
---
# <a name="kslibexts"></a>!ks.libexts


**! Ks.libexts**拡張機能が拡張機能モジュールに静的にリンクされているライブラリの Microsoft 提供の拡張機能へのアクセスを提供します。

```dbgcmd
!ks.libexts [Command] [Libext] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*コマンド*  
(省略可能)。 次の値のいずれかを指定します。 この引数を省略すると、 **! ks.libexts**ヘルプ情報を返します。

<span id="disableall________"></span><span id="DISABLEALL________"></span>**disableall**   
すべてのライブラリの拡張機能を無効にします。 これを使用する場合は、省略、 *Libext*パラメーター。

<span id="_________disable"></span><span id="_________DISABLE"></span> **無効にします。**  
名前で特定のライブラリの拡張機能を無効にします。 これを使用する場合に名前を指定、 *Libext*パラメーター。

<span id="_________enableall"></span><span id="_________ENABLEALL"></span> **enableall**  
すべてのライブラリの拡張機能を有効にします。 正しいシンボルに読み込まれたコンポーネントのみが有効です。 これを使用する場合は、省略、 *Libext*パラメーター。

<span id="enable"></span><span id="ENABLE"></span>**有効にします。**  
名前で特定のライブラリの拡張機能を有効にします。 これを使用する場合に名前を指定、 *Libext*パラメーター。 のみ正しいシンボルに読み込まれたコンポーネントを有効にすることができます。

<span id="_________details"></span><span id="_________DETAILS"></span> **詳細情報**  
現在リンクされているライブラリのすべての拡張機能の詳細を表示します。 これを使用する場合は、省略、 *Libext*パラメーター。

<span id="_______Libext______"></span><span id="_______libext______"></span><span id="_______LIBEXT______"></span> *Libext*   
ライブラリの拡張機能の名前を指定します。 のみ必須*コマンド*の値**を有効にする**または**を無効にする**します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)します。

<a name="remarks"></a>注釈
-------

拡張機能モジュールには、個別のコンポーネントを構築して Ks.dll にリンクを可能にする機能拡張フレームワークが含まれています。 これらのコンポーネントは、ライブラリの拡張機能と呼ばれます。

**! Ks.libexts**コマンドには、そのライブラリの拡張機能だけでなく制御に関する統計情報の表示ことができます。 詳細については、発行 **! ks.libexts**引数なしでします。

 

 





