---
title: DevCon Dp_delete
description: ローカルコンピューターのドライバーストアからサードパーティ (OEM) ドライバーパッケージを削除します。 このコマンドを実行すると、INF ファイル、PNF ファイル、および関連付けられているカタログファイル (.cat) が削除されます。
ms.assetid: bc9d8d66-4aa1-423b-b907-40a8c0194eb1
keywords:
- DevCon Dp_delete ドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon Dp_delete
api_type:
- NA
ms.date: 04/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3536a1a96fc305cfb7000dfda020d7beaab21255
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209484"
---
# <a name="devcon-dp_delete"></a>DevCon Dp\_削除

ローカルコンピューターのドライバーストアからサードパーティ (OEM) ドライバーパッケージを削除します。 このコマンドを実行すると、INF ファイル、PNF ファイル、および関連付けられているカタログファイル (.cat) が削除されます。

```command
    devcon [-f] dp_delete inf
```

## <a name="parameters"></a>パラメーター

**-f**このパラメーターは、デバイスがその時点で使用している場合でも、ドライバーパッケージを削除します。

*inf*INF ファイルの OEM\*.inf ファイル名。 [**DevCon dp\_add**](devcon-dp-add.md)などを使用してドライバーパッケージをドライバーストアに追加すると、Windows によって、この形式のファイル名が INF ファイルに割り当てられます。

## <a name="comments"></a>コメント

### <a name="sample-usage"></a>使用例

```command
devcon dp_delete oem2.inf
devcon -f dp_delete oem0.inf
```
