---
title: finddata
description: Finddata 拡張機能では、指定されたファイル オブジェクト内で指定されたオフセット位置に、キャッシュされたデータを表示します。
ms.assetid: 1d6f920b-5716-4ccc-8c2d-08b422f57124
keywords:
- キャッシュ マネージャー
- Windows デバッグ finddata
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- finddata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e001a16ddf155d32d0e8923572b34a4af7b87729
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336741"
---
# <a name="finddata"></a>!finddata


**! Finddata**拡張機能は、指定されたファイル オブジェクト内で指定されたオフセット、キャッシュされたデータを表示します。

```dbgcmd
!finddata FileObject Offset
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span> *FileObject*   
ファイル オブジェクトのアドレスを指定します。

<span id="_______Offset______"></span><span id="_______offset______"></span><span id="_______OFFSET______"></span> *オフセット*   
オフセットを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

キャッシュの管理については、Microsoft Windows SDK のマニュアルを参照し、 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

その他のキャッシュ管理拡張機能については、次を参照してください。、 [ **! cchelp** ](-cchelp.md)拡張機能。

 

 





