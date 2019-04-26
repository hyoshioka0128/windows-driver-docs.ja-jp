---
title: .closehandle (ハンドルを閉じる)
description: .Closehandle コマンドでは、ターゲット アプリケーションによって所有されているハンドルを閉じます。
ms.assetid: 1513cbdd-327f-447a-8267-633cb123d17d
keywords:
- .closehandle (ハンドルを閉じる) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .closehandle (Close Handle)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20ad6c9c453ad5ea1d28b090e3052fc7b1a7b63d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336890"
---
# <a name="closehandle-close-handle"></a>.closehandle (ハンドルを閉じる)


**.Closehandle**コマンドは、ターゲット アプリケーションによって所有されているハンドルを閉じます。

```dbgsyntax
.closehandle Handle 
.closehandle -a 
```

## <a name="span-idddkmetaclosehandledbgspanspan-idddkmetaclosehandledbgspanparameters"></a><span id="ddk_meta_close_handle_dbg"></span><span id="DDK_META_CLOSE_HANDLE_DBG"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
終了するハンドルを指定します。

<span id="_______-a______"></span><span id="_______-A______"></span> **-**   
終了する対象のアプリケーションによって所有されているすべてのハンドルをによりします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

使用することができます、 [ **! 処理**](-handle.md)拡張機能を既存のハンドルを表示します。

 

 





