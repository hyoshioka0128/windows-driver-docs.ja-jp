---
title: E_INVALIDARG 戻り値の処理
description: E_INVALIDARG 戻り値の処理
ms.assetid: 312b2452-71b3-4fbe-93fb-f4b0e6099c0f
keywords:
- ユーザー モードのディスプレイ ドライバー WDK Windows Vista では、E_INVALIDARG 戻り値
- E_INVALIDARG は、WDK 表示の値を返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dff82dc5e2b1c1b44e8bc8807d9b2e9b1121e23b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582414"
---
# <a name="handling-the-einvalidarg-return-value"></a>E を処理\_INVALIDARG 戻り値


通常、ユーザー モードのディスプレイ ドライバーはフェールバックできませんのいずれかの[関数](https://msdn.microsoft.com/library/windows/hardware/ff570118)を返すことによって E\_INVALIDARG します。 ただし、ユーザー モード ドライバーを表示する場合は、受信、E\_INVALIDARG は呼び出しのいずれかの値を返す、[ランタイムが指定した関数のマイクロソフトの Direct3D](https://msdn.microsoft.com/library/windows/hardware/ff552862) (ドライバーまたは悪意のあるコードでプログラミング エラーのためオペレーティング システムで実行される)、ドライバーが返す必要があります E\_INVALIDARG ランタイム後 Direct3D ランタイムに戻さがドライバーの関数のいずれかを呼び出します。 それ以外の場合、ユーザー モードのディスプレイ ドライバーが返さない E\_INVALIDARG Direct3D ランタイムにします。

 

 





