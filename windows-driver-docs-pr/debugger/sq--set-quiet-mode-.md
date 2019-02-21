---
title: sq (Quiet モードに設定)
description: '%Sq コマンドでは、オンまたはオフ、quiet モードがオンにします。'
ms.assetid: db8a266c-e2e5-4de7-8154-993a78585f04
keywords:
- sq (Quiet モードに設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sq (Set Quiet Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b4ff1ee435585c99cb0bb2f7df467d2a011b3b07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552333"
---
# <a name="sq-set-quiet-mode"></a>sq (Quiet モードに設定)


**Sq**コマンドが非表示モードを有効または無効です。

```dbgcmd
sq 
sq{e|d} 
```

## <span id="ddk_cmd_set_quiet_mode_dbg"></span><span id="DDK_CMD_SET_QUIET_MODE_DBG"></span>


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

 

<a name="remarks"></a>注釈
-------

**Sqe**コマンドは、非表示モードをオンにし、 **sqd**コマンドがオフにします。 **Sq**コマンドは、オンとオフは、非表示モードをオンにします。 これらの各コマンドには、新しい非表示モードのステータスも表示されます。

KD モードまたはカーネル モードで非表示モードを設定することができます、KDQUIET を使用して、WinDbg[環境変数](kernel-mode-environment-variables.md)します。 (ユーザー モードとカーネル モードのデバッグの両方で非表示モードが存在しますが、KDQUIET 環境変数がカーネル モードでのみ認識されることに注意してください)。

*Quiet モード*は 3 つの個別の効果があります。

-   デバッガー メッセージを表示しませんが、拡張 DLL のロードまたはアンロードされるたびにします。

-   [ **R (レジスタ)** ](r--registers-.md)コマンドには、不要になったその構文内で等号 (=) が必要です。

-   カーネル デバッグを時間の長い中にターゲット コンピューターに分割するときに警告メッセージは表示されません。

Quiet モードの影響とを混同しないでください、 **- myob** [コマンド ライン オプション](command-line-options.md)が CDB などの KD) で、または **-q** [**コマンド ライン オプション** ](windbg-command-line-options.md) (WinDbg) でします。

 

 





