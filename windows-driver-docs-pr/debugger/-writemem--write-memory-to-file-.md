---
title: .writemem (ファイルへのメモリの書き込み)
description: .Writemem コマンドは、メモリのセクションをファイルに書き込みます。
ms.assetid: 928e9452-d9b4-49fa-a5fa-cdc3832d7349
keywords:
- .writemem (ファイルに書き込みメモリ) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .writemem (Write Memory to File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed5a669a39292388e96294742b9f7749516f03f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348034"
---
# <a name="writemem-write-memory-to-file"></a>.writemem (ファイルへのメモリの書き込み)


**.Writemem**コマンドでは、メモリのセクションをファイルに書き込みます。

```dbgcmd
.writemem FileName Range 
```

## <a name="span-idddkmetawritememorytofiledbgspanspan-idddkmetawritememorytofiledbgspanparameters"></a><span id="ddk_meta_write_memory_to_file_dbg"></span><span id="DDK_META_WRITE_MEMORY_TO_FILE_DBG"></span>パラメーター


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
作成するファイルの名前を指定します。 完全なパスとファイル名、またはファイル名だけを指定することができます。 ファイル名にスペースが含まれている場合*FileName*引用符で囲む必要があります。 パスを指定しない場合、現在のディレクトリが使われます。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
ファイルに書き込まれるメモリの範囲を指定します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

メモリは、文字どおりファイルにコピーされます。 任意の方法では解析されません。

**.Writemem**コマンドは、逆の[ **.readmem (ファイルから読み取りメモリ)** ](-readmem--read-memory-from-file-.md)コマンド。

 

 





