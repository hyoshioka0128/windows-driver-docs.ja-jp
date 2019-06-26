---
title: SIM ツールキットを起動するための予約済み URI
description: SIM ツールキットを起動するための予約済み URI
ms.assetid: d194b37e-427b-4fe2-a49a-050d06a7d3b9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d73bc5dc34995eec6854464553fab1d7e53f0edb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384712"
---
# <a name="reserved-uri-to-launch-sim-toolkit"></a>SIM ツールキットを起動するための予約済み URI


Windows には、[Start] 画面をさらに検出できるように SIM アプリケーション CPL 起動できる UWP アプリを配置するパートナーをできるようにする予約済みの URI スキームのサポートが含まれています。 現時点では、ユーザーのみを取得できます SIM アプリケーションに移動して、**設定** &gt; **ネットワークとワイヤレス** &gt; **移動体通信および SIM** &gt; **詳細オプション**画面とタップ、 **SIM アプリケーション**ボタンをクリックします。 詳細については、次を参照してください。 [SIM toolkit](sim-toolkit.md)します。

URI スキームを`"ms-settings-uicctoolkit"`、SIM toolkit ランチャーが定義されています。 これは、ユーザーが銀行業務やセキュリティ アプリの課金などの携帯電話会社のネットワークでより簡単にアクセス機能を有効になります。

## <a name="launching-a-uri"></a>URI の起動


UWP アプリへの呼び出しを使用して CPL SIM アプリケーションを読み込むことができます、 [Launcher.LaunchUriAsync(Uri)](https://docs.microsoft.com/uwp/api/Windows.System.Launcher#Windows_System_Launcher_LaunchUriAsync_Windows_Foundation_Uri_)からメソッド、**ランチャー**のオブジェクト、 **Windows.System**名前空間。

次の例では、パートナーが、アプリから SIM アプリケーション CPL を起動する方法を示します。

``` syntax
Windows.System.Launcher.LaunchUriAsync("ms-settings-uicctoolkit:");
```

## <a name="related-topics"></a>関連トピック


[SIM toolkit](sim-toolkit.md)

 

 






