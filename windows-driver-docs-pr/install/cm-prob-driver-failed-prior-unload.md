---
title: CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
description: CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
ms.assetid: c7639fd7-738f-4115-9abc-0bafca097b9e
keywords:
- CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4797c3c15795b203221bd0176652721ee1c91e16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582053"
---
# <a name="cmprobdriverfailedpriorunload"></a>CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD

この関数は、システムの使用に予約されています。

以前のインスタンスがまだ読み込まれているために、ドライバーを読み込むことができませんでした。

## <a name="error-code"></a>エラー コード

38

### <a name="display-message"></a>メッセージを表示します。

"Windows 読み込むことができませんこのハードウェアのデバイス ドライバーは、デバイス ドライバーの以前のインスタンスをメモリ内に残っています。 (コード 38)"

### <a name="recommended-resolution"></a>推奨される解決方法

以前のドライバーのインスタンスが正しくない参照カウントまたは負荷の間の競合が原因で読み込まれるまだとアンロード操作。 さらに、このメッセージは複数のドライバーが参照されている場合に表示される[ **INF AddService ディレクティブ**](inf-addservice-directive.md)で 1 つ以上の INF ファイル。

選択**コンピューターの再起動**、これには、コンピューターを再起動します。
