---
title: lse (ソース エディターの起動)
description: よくコマンドでは、現在のソース ファイルのエディターが開きます。
ms.assetid: 2f66b5c3-1cd6-4641-8dea-5e3a11c87db0
keywords:
- よく (ソース エディターの起動) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lse (Launch Source Editor)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de740909aff1b6575cbec845a74e75ff2a053f89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383316"
---
# <a name="lse-launch-source-editor"></a>lse (ソース エディターの起動)


**よく**コマンドは、現在のソース ファイルのエディターを開きます。

```dbgcmd
lse 
```

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

**よく**コマンドは、現在のソース ファイルのエディターを開きます。 このコマンドを実行 をクリックすると**このファイルを編集**のショートカット メニューで、[ソース ウィンドウ](source-window.md)WinDbg でします。

使用することはできませんので、ターゲットで実行されているコンピューターでエディターを開く、**よく**リモート クライアントからコマンド。

WinDiff エディターのレジストリ情報や、WINDBG の値\_INVOKE\_エディター環境変数がどのエディターを開くを確認します。 たとえば、次の値は WINDBG\_INVOKE\_エディター。

```reg
c:\my\path\myeditor.exe -file %f -line %l
```

この値は、現在のソース ファイルの 1 から始まる行番号を Myeditor.exe を開くことを示します。 **%L**オプションを指定する行に 1 から始まる数値を読み取る必要がありますと **%f**現在のソース ファイルを使用することを示します。 含めることもできます **%L**を示す行番号は 0 から始まるまたは **%p**を現在のソース ファイルを使用することを示します。

 

 





