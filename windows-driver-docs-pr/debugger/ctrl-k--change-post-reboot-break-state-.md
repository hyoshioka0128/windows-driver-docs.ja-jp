---
title: CTRL + K (再起動後の中断状態の変更)
description: CTRL + K キーをデバッガーは自動的に対象のコンピュータに中断する条件を変更します。
ms.assetid: 74f57775-63ad-4a96-9ba5-bfedd4c8c826
keywords:
- CTRL + K (再起動後の中断状態の変更) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+K (Change Post-Reboot Break State)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 918a4ccd632f2d8534b5fca185c94fd19d6efd10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558547"
---
# <a name="ctrlk-change-post-reboot-break-state"></a>CTRL + K (再起動後の中断状態の変更)


CTRL + K キーをデバッガーは自動的に対象のコンピュータに中断する条件を変更します。

KD 構文

```dbgcmd
CTRL+K  ENTER 
```

WinDbg の構文

```dbgcmd
CTRL+ALT+K 
```

## <span id="ddk_meta_ctrl_k_dbg"></span><span id="DDK_META_CTRL_K_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>デバッガー</strong></p></td>
<td align="left"><p>KD と WinDbg のみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドの概要と、再起動プロセスがデバッガーに与える影響の詳細については、[クラッシュし、ターゲット コンピューターを再起動](crashing-and-rebooting-the-target-computer.md)を参照してください。

<a name="remarks"></a>注釈
-------

このコントロールのキーには、次の 3 つの状態を順番にカーネル デバッガーが発生します。

<span id="No_break"></span><span id="no_break"></span><span id="NO_BREAK"></span>**区切りはありません。**  
この状態で、デバッガーは中断されません、ターゲット コンピューターを押さない限り[ **CTRL + C**](ctrl-c--break-.md)します。

<span id="Break_on_reboot"></span><span id="break_on_reboot"></span><span id="BREAK_ON_REBOOT"></span>**再起動時に中断します。**  
この状態では、カーネルが初期化された後、デバッガーは、再起動された対象のコンピュータに中断します。 KD または WinDbg を開始するのと同じ、 **-b**[コマンド ライン オプション](command-line-options.md)します。

<span id="Break_on_first_module_load"></span><span id="break_on_first_module_load"></span><span id="BREAK_ON_FIRST_MODULE_LOAD"></span>**最初のモジュールの読み込み時に中断します。**  
この状態では、最初のカーネル モジュールが読み込まれた後、デバッガーは、再起動された対象のコンピュータに中断します。 (これによりよりも前に発生するブレーク、**の再起動時に中断**オプション)。KD または WinDbg を開始するのと同じ、 **-d**[コマンド ライン オプション](command-line-options.md)します。

キーの CTRL + K を使用すると、新しいブレーク状態が表示されます。

WinDbg では、このことができますもすることで実現選択[デバッグ |カーネルの接続 |初期の中断をサイクル](debug---kernel-connection---cycle-initial-break.md)します。

 

 





