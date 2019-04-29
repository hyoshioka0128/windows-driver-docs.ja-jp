---
title: Iasphelp get\_IsCluster メソッド
description: IsCluster プロパティは、クラスター サービスがクラスター ノードで実行されているかどうかを判断する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_96d39d88-6d6f-49af-93d7-0f6668af9564.xml
- print.iasphelp\_iscluster
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 78573fe7-d264-4d3c-8654-a85c2abfb93a
keywords:
- 印刷デバイスの get_IsCluster メソッド
- get_IsCluster メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_IsCluster メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_IsCluster
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12413c461bc41762f30f7fb91edc9e568946ef1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392891"
---
# <a name="iasphelpgetiscluster-method"></a>Iasphelp::get\_IsCluster メソッド

**IsCluster**プロパティは、クラスター サービスがクラスター ノードで実行されているかどうかを判断する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_IsCluster(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
受信するメモリ位置への呼び出し元が指定したポインター **TRUE**クラスター サービスがインストールされている、構成、および、ノードで実行されている場合と**FALSE**それ以外の場合。

<a name="return-value"></a>戻り値
------------

このプロパティ常に返します S\_ok をクリックします。

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、 **GetNodeClusterState**クラスター サービスの状態を判断する関数。 この関数の詳細については、Windows SDK のドキュメントを参照してください。

```vb
Dim objPrinter, ClusterRunning
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
ClusterRunning = objPrinter.IsCluster
```

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td>Desktop</td>
</tr>
</tbody>
</table>
