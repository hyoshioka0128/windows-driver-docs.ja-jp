---
title: minipkd.help
description: Minipkd.help 拡張機能では、Minipkd.dll の拡張機能コマンドのヘルプ テキストが表示されます。
ms.assetid: 5629aec8-8c9d-4ed0-91fb-c8d020f78405
keywords:
- デバッグ minipkd.help Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.help
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 005fb48ab498aafad1f79b443d68bf37118ce51c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336077"
---
# <a name="minipkdhelp"></a>!minipkd.help


**! Minipkd.help**拡張子 Minipkd.dll 拡張機能コマンドのヘルプ テキストを表示します。

```dbgcmd
!minipkd.help 
```

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
<td align="left"><p>Minipkd.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。 [SCSI ミニポート デバッグ](scsi-miniport-debugging.md)します。

<a name="remarks"></a>注釈
-------

次のようなエラー メッセージが表示されたら、シンボル パスが正しくないし、Scsiport.sys シンボルの正しいバージョンをポイントしていないことを示します。

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

使用して、 [ **.sympath (シンボル パスの設定)** ](-sympath--set-symbol-path-.md)コマンドを現在のパスを表示し、パスを変更します。 使用して、 [ **.reload (モジュールの再読み込み)** ](-reload--reload-module-.md)コマンドを現在のパスからシンボルを再読み込みします。

 

 





