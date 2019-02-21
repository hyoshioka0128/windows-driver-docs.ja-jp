---
title: SIM のツールキットを起動する予約済みの URI
description: SIM のツールキットを起動する予約済みの URI
ms.assetid: d194b37e-427b-4fe2-a49a-050d06a7d3b9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 322e0e454812b9c1a0c3dc4fd53188b0447110ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539282"
---
# <a name="reserved-uri-to-launch-sim-toolkit"></a>SIM のツールキットを起動する予約済みの URI


Windows には、[Start] 画面をさらに検出できるように SIM アプリケーション CPL 起動できる UWP アプリを配置するパートナーをできるようにする予約済みの URI スキームのサポートが含まれています。 現時点では、ユーザーのみを取得できます SIM アプリケーションに移動して、**設定** &gt; **ネットワークとワイヤレス** &gt; **移動体通信および SIM** &gt; **詳細オプション**画面とタップ、 **SIM アプリケーション**ボタンをクリックします。 詳細については、次を参照してください。 [SIM toolkit](sim-toolkit.md)します。

URI スキームを`"ms-settings-uicctoolkit"`、SIM toolkit ランチャーが定義されています。 これは、ユーザーが銀行業務やセキュリティ アプリの課金などの携帯電話会社のネットワークでより簡単にアクセス機能を有効になります。

## <a name="launching-a-uri"></a>URI の起動


UWP アプリへの呼び出しを使用して CPL SIM アプリケーションを読み込むことができます、 [Launcher.LaunchUriAsync(Uri)](https://msdn.microsoft.com/library/windows/apps/hh701480.aspx)からメソッド、**ランチャー**のオブジェクト、 **Windows.System**名前空間。

次の例では、パートナーが、アプリから SIM アプリケーション CPL を起動する方法を示します。

``` syntax
Windows.System.Launcher.LaunchUriAsync("ms-settings-uicctoolkit:");
```

## <a name="related-topics"></a>関連トピック


[SIM toolkit](sim-toolkit.md)

 

 






