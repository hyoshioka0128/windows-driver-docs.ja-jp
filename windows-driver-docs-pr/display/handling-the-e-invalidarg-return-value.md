---
title: E_INVALIDARG の戻り値の処理
description: E_INVALIDARG の戻り値の処理
ms.assetid: 312b2452-71b3-4fbe-93fb-f4b0e6099c0f
keywords:
- ユーザーモード表示ドライバー WDK Windows Vista、E_INVALIDARG 戻り値
- E_INVALIDARG 戻り値の WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 646c77a9eb633d7d7bdbaa05b04d19cdd39cebdc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839661"
---
# <a name="handling-the-e_invalidarg-return-value"></a>E\_INVALIDARG の戻り値の処理


通常、ユーザーモードの表示ドライバーは、E\_INVALIDARG を返すことによって、その[機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を失敗させることはできません。 ただし、ユーザーモードの表示ドライバーが、 [Microsoft Direct3D ランタイム](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)によって提供された関数の1つを呼び出すときに、E\_invalidarg の戻り値を受け取る場合は、ドライバーのプログラミングエラーまたは操作で実行される悪意のあるコードのために、システム) は、ランタイムがドライバーの関数のいずれかを呼び出した後に、ドライバーが E\_INVALIDARG を Direct3D ランタイムに返す必要があります。 それ以外の場合、ユーザーモードの表示ドライバーは、E\_INVALIDARG を Direct3D ランタイムに返すことはできません。

 

 





