---
title: homedir
description: Homedir 拡張機能は、シンボル サーバーと移行元サーバーで使用される既定のディレクトリを設定します。
ms.assetid: 6bebd7df-03d8-4413-8a0c-a0d5ad913173
keywords:
- Windows デバッグ homedir
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- homedir
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74e85ade59232c03a23146028e52eb060288e296
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336521"
---
# <a name="homedir"></a>!homedir


**! Homedir**拡張機能は、シンボル サーバーと移行元サーバーで使用される既定のディレクトリを設定します。

```dbgcmd
!homedir Directory
!homedir
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span> *ディレクトリ*   
ホーム ディレクトリとして使用する新しいディレクトリを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

場合、 **! homedir**引数なしで拡張機能が使用される、現在のホーム ディレクトリが表示されます。

移行元サーバーのキャッシュは、ホーム ディレクトリの src サブディレクトリに格納されます。 シンボル サーバーのダウン ストリームのストアは、別の場所を指定しない限り、ホーム ディレクトリの sym サブディレクトリに既定値です。

WinDbg が開始されると、ホーム ディレクトリは、Windows のツールのデバッグがインストールされているディレクトリです。 **! Homedir**拡張機能を使用して、この値を変更します。

 

 





