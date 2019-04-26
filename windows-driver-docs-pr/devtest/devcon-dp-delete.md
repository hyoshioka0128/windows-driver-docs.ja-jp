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
ms.date: 04/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: 240d2eed9fe8f4fe56f6236d586768c12cf90b08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347693"
---
# <a name="devcon-dpdelete"></a>DevCon Dp\_削除

ローカル コンピューターのドライバー ストアからサード パーティ (OEM) のドライバー パッケージを削除します。 このコマンドは、INF ファイル、PNF ファイル、および関連するカタログ ファイル (.cat) を削除します。

```command
    devcon [-f] dp_delete inf
```

## <a name="parameters"></a>パラメーター

**-f**デバイスを使用すると、時に使用されている場合でも、このパラメーターは、ドライバー パッケージを削除します。

*inf* OEM\*INF ファイルの .inf ファイル名。 追加すると、ドライバー パッケージ、ドライバー ストアなどを使用して Windows に INF ファイルをこの形式のファイル名が割り当てられます[ **DevCon dp\_追加**](devcon-dp-add.md)します。

## <a name="comments"></a>コメント

### <a name="sample-usage"></a>使用例

```command
devcon dp_delete oem2.inf
devcon dp_delete oem0.inf -f
```
