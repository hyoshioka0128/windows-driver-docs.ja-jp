---
title: Windows でのインストール
description: Windows でのインストール
ms.assetid: 790caffd-ebb0-4ba1-b31c-b03d3c83bc59
keywords:
- オーディオ アダプター WDK、システム コンポーネント
- アダプターのドライバー WDK オーディオ、システム コンポーネント
- ポート クラス オーディオ アダプター WDK、システム コンポーネント
ms.date: 10/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86f81e2b9a783d30193dc83b271bfaf74eec515f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539356"
---
# <a name="installing-in-windows"></a>Windows でのインストール


INF のデバイス ドライバーのインストール」セクションの次の例では、2 つのディレクティブは、Windows でオーディオのアダプターのコアのシステム コンポーネントをインストールするシステム ドライバー情報を追加します。

```inf
  [XYZ-Audio-Device.Registration.NTX86]
  Include=ks.inf, wdmaudio.inf
  Needs=KS.Registration, WDMAUDIO.Registration
```

については、 **Include**と**必要がある**ディレクティブを参照してください[ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)します。

 

 




