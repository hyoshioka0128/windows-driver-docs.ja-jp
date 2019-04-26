---
title: .allow_image_mapping (画像マッピングの許可)
description: .Allow_image_mapping コマンドでは、イメージ ファイルをマップするかどうかを制御します。
ms.assetid: 3d216d17-f2af-48f7-9d91-e12c3c305a67
keywords:
- .allow_image_mapping (イメージのマッピングを許可する) Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .allow_image_mapping (Allow Image Mapping)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7c1f0fe1fc270df9ee1212ce26848ecf37d139c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334777"
---
# <a name="allowimagemapping-allow-image-mapping"></a>.allow\_イメージ\_マッピング (イメージのマッピングを許可する)


**.Allow\_イメージ\_マッピング**コマンド コントロールかどうかイメージ ファイルにマップされます。

```dbgcmd
    .allow_image_mapping [/r] 0 
    .allow_image_mapping [/r] 1 
    .allow_image_mapping 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________r______"></span><span id="________R______"></span> **/r**   
デバッガーのモジュールの一覧のすべてのモジュールを再読み込みします。 これに相当[ **.reload/d**](-reload--reload-module-.md)します。

<span id="_______0______"></span> **0**   
イメージ ファイルがマップされるを防ぎます。

<span id="_______1______"></span> **1**   
マップをイメージ ファイルを使用します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードとカーネル モード</p></td>
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

パラメーターなしで **.allow\_イメージ\_マッピング**イメージ ファイルのマッピングは現在許可されているかどうかが表示されます。 既定では、このマッピングは許可されています。

ミニダンプをデバッグするときに、イメージのマッピングが一般的です。 イメージのマッピングは、DbgHelp が (たとえば、デバッグ中にカーネル メモリはページ アウトされたときに) デバッグ レコードにアクセスできない場合にも発生します。

 

 





