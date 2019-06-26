---
title: E_INVALIDARG 戻り値の処理
description: E_INVALIDARG 戻り値の処理
ms.assetid: 312b2452-71b3-4fbe-93fb-f4b0e6099c0f
keywords:
- ユーザー モードのディスプレイ ドライバー WDK Windows Vista では、E_INVALIDARG 戻り値
- E_INVALIDARG は、WDK 表示の値を返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54da26c839c6d003106f8fa97c1f0aa7ee3fe992
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369843"
---
# <a name="handling-the-einvalidarg-return-value"></a>E を処理\_INVALIDARG 戻り値


通常、ユーザー モードのディスプレイ ドライバーはフェールバックできませんのいずれかの[関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)を返すことによって E\_INVALIDARG します。 ただし、ユーザー モード ドライバーを表示する場合は、受信、E\_INVALIDARG は呼び出しのいずれかの値を返す、[ランタイムが指定した関数のマイクロソフトの Direct3D](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) (ドライバーまたは悪意のあるコードでプログラミング エラーのためオペレーティング システムで実行される)、ドライバーが返す必要があります E\_INVALIDARG ランタイム後 Direct3D ランタイムに戻さがドライバーの関数のいずれかを呼び出します。 それ以外の場合、ユーザー モードのディスプレイ ドライバーが返さない E\_INVALIDARG Direct3D ランタイムにします。

 

 





