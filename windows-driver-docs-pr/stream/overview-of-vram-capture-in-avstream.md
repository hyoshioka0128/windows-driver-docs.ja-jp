---
title: AVStream での VRAM キャプチャの概要
description: AVStream での VRAM キャプチャの概要
ms.assetid: b5fd026f-75e3-49e0-a39e-4883dd6cacf2
keywords:
- VRAM キャプチャ WDK AVStream、VRAM キャプチャについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad7d9f7aa5cc9a24fb7fdd11d4a264f93cd783c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570166"
---
# <a name="overview-of-vram-capture-in-avstream"></a>AVStream での VRAM キャプチャの概要


VRAM にキャプチャをサポートするためには、仕入先は、Windows Vista のディスプレイ ドライバー スタック内の機能を追加します。 具体的には、仕入先には、特定の KS プロパティをサポートする、暗証番号 (pin) を中心とした AVStream ミニドライバーが用意されています。 ディスプレイのミニポート ドライバー内で AVStream 機能を含めることはできますが、ミニドライバーがディスプレイのミニポート ドライバーに従属する代わりにすることをお勧めします。 ディスプレイのミニポート ドライバーが Windows Vista display driver スタックに収める方法を説明するダイアグラムを表示するには、Windows Vista ドライバー モデル アーキテクチャの表示」を参照します。

このドキュメントでは、このような個別のスタンドアロン キャプチャ ミニドライバーを実装する方法について説明します。

キャプチャ ドライバーは、すべて DXVA2 対応ダウン ストリームへのデータまたはフィルター処理、たとえば、レンダラーをエンコーダーに送信できます。

次の図は、VRAM のキャプチャが有効な AVStream ミニドライバーで、ディスプレイのミニポート ドライバーと他のモジュールがどのように対話する方法を示します。

![vram のキャプチャが有効な avstream ミニドライバーがディスプレイのミニポート ドライバーおよびその他のモジュールと対話する方法を示す図](images/lddmcapturearchitectureoverview.gif)

 

 




