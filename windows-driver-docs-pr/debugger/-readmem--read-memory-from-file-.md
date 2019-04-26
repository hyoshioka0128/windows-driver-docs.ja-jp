---
title: .readmem (ファイルからメモリを読み込む)
description: .Readmem コマンドでは、指定したファイルから生のバイナリ データを読み取るし、対象のコンピュータのメモリにデータをコピーします。
ms.assetid: 128cbea1-5fb5-4685-8587-f814f94cc658
keywords:
- .readmem (ファイルから読み取りメモリ) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .readmem (Read Memory from File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e2a23efb0889cccf1ab13cc167866222c4701306
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338931"
---
# <a name="readmem-read-memory-from-file"></a>.readmem (ファイルからメモリを読み込む)


**.Readmem**コマンドが指定したファイルから生のバイナリ データを読み取るし、ターゲット コンピューターのメモリにデータをコピーします。

```dbgcmd
.readmem FileName Range 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
読み取るファイルの名前を指定します。 完全なパスまたはファイル名のみを指定することができます。 ファイル名にスペースが含まれている場合は、囲む*FileName*引用符で囲んで指定します。 パスを指定しない場合、デバッガーには、現在のディレクトリが使用されます。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
メモリ内のデータを格納するためのアドレス範囲を指定します。 このパラメーターは、開始と終了アドレスまたは開始アドレスと、オブジェクトの数に含めることができます。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

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

メモリ データは、文字どおり対象のコンピュータにコピーされます。 デバッガーは、任意の方法でデータを解析できません。 たとえば、 **.readmem myfile 1000 10**コマンドは、Myfile ファイルから 10 バイトをコピーし、1000 のアドレスで始まる、ターゲット コンピューターのメモリに格納します。

**.Readmem**コマンドは、逆の[ **.writemem (ファイルに書き込むメモリ)** ](-writemem--write-memory-to-file-.md)コマンド。

 

 





