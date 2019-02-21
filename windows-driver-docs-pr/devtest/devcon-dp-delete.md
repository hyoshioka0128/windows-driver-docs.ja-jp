---
title: DevCon Dp_delete
description: ローカル コンピューターのドライバー ストアからサード パーティ (OEM) のドライバー パッケージを削除します。 このコマンドは、INF ファイル、PNF ファイル、および関連するカタログ ファイル (.cat) を削除します。
ms.assetid: bc9d8d66-4aa1-423b-b907-40a8c0194eb1
keywords:
- DevCon Dp_delete ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Dp_delete
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 582f8aac06c8de1f30f70575b49f9a4d55ebe368
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548579"
---
# <a name="devcon-dpdelete"></a>DevCon Dp\_削除


ローカル コンピューターのドライバー ストアからサード パーティ (OEM) のドライバー パッケージを削除します。 このコマンドは、INF ファイル、PNF ファイル、および関連するカタログ ファイル (.cat) を削除します。

```
    devcon dp_delete [-f] inf
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-f______"></span><span id="_______-F______"></span> **-f**   
このパラメーターは、デバイスを使用すると、時に使用されている場合でも、ドライバー パッケージを削除します。

<span id="_______inf______"></span><span id="_______INF______"></span> *inf*   
OEM\*INF ファイルの .inf ファイル名。 追加すると、ドライバー パッケージ、ドライバー ストアなどを使用して Windows に INF ファイルをこの形式のファイル名が割り当てられます[ **DevCon dp\_追加**](devcon-dp-add.md)します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon dp_delete oem2.inf
devcon dp_delete oem0.inf -f
```









