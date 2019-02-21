---
title: リベース
description: リベース拡張機能は、指定したアドレスまたはシンボルの rebase.log ファイル内で検索します。
ms.assetid: 811e7ab8-301f-433a-bfc4-8a4e5f002b30
keywords:
- Windows のデバッグを再配置します。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rebase
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 66c00390ea06a189b8f6541cfac89cfcd65ec34b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558149"
---
# <a name="rebase"></a>! リベース


**! リベース**rebase.log ファイルで指定したアドレスまたはシンボルの拡張機能の検索。

```dbgcmd
!rebase [-r] Address [Path]
!rebase Symbol [Path]
!rebase -stack [Path]
!rebase -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-r______"></span><span id="_______-R______"></span> **-r**   
Rebase.log で見つかった任意のモジュールをロードしようとしています。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
標準の 16 進数形式でアドレスを指定します。 拡張機能は、このアドレスの近くに Dll が検索されます。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *パス*   
Rebase.log へのファイル パスを指定します。 場合*パス*が指定されていない拡張機能が、rebase.log またはされていない場合は、パスを推測しようとした場合、現在の作業ディレクトリから rebase.log ファイルを読み取ろうとします。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span> *シンボル*   
シンボルまたはイメージ名を指定します。 拡張機能は、この部分文字列が含まれている Dll が検索されます。

<span id="_______-stack______"></span><span id="_______-STACK______"></span> **-stack**   
現在のスタック内のすべてのモジュールを表示します。

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
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

 

 





