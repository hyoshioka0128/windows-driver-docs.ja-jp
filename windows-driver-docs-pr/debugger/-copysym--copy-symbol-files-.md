---
title: .copysym (シンボル ファイルのコピー)
description: .Copysym コマンドは、現在のシンボル ファイルを指定したディレクトリにコピーします。
ms.assetid: f90d1402-4bf3-4cd0-993e-a42c220beb7a
keywords:
- .copysym (シンボル ファイルのコピー) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .copysym (Copy Symbol Files)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4882da268e2f74ad4d9f832241bb14a1142814c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336894"
---
# <a name="copysym-copy-symbol-files"></a>.copysym (シンボル ファイルのコピー)


**.Copysym**コマンドは、指定したディレクトリに、現在のシンボル ファイルをコピーします。

```dbgsyntax
    .copysym [/l] Path
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________l______"></span><span id="________L______"></span> **/l**   
コピーするときに読み込まれる各シンボル ファイルをによりします。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *パス*   
シンボル ファイルのコピー先ディレクトリを指定します。 コピーでは、既存のファイルは上書きされません。

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

多くの場合、ネットワーク上のシンボルが格納されます。 シンボルへのアクセスを低速にすることがよくあります。 または別のコンピューターがネットワーク アクセスが不要になったあるデバッグ セッションを転送する必要があります。 このようなシナリオで、 **.copysym**ローカル ディレクトリに、セッションに必要なシンボルをコピーするコマンドを使用できます。

 

 





