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
ms.openlocfilehash: 8d74d0b559c939a3a23ee3ce097c6841fdfbc59c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359871"
---
# <a name="installing-in-windows"></a>Windows でのインストール


INF のデバイス ドライバーのインストール」セクションの次の例では、2 つのディレクティブは、Windows でオーディオのアダプターのコアのシステム コンポーネントをインストールするシステム ドライバー情報を追加します。

```inf
  [XYZ-Audio-Device.Registration.NTX86]
  Include=ks.inf, wdmaudio.inf
  Needs=KS.Registration, WDMAUDIO.Registration
```

については、 **Include**と**必要がある**ディレクティブを参照してください[ **INF DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)します。

 

 




