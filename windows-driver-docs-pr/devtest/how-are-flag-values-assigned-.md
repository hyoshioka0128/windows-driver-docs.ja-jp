---
title: フラグの値を割り当てる方法
description: フラグの値を割り当てる方法
ms.assetid: de74e2d9-0ebf-4125-9dbb-42f7755010f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67eb4272f816cb41eb76980f9547e7d3e00b1a0f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358301"
---
# <a name="how-are-flag-values-assigned"></a>フラグの値を割り当てる方法


[トレース フラグ](trace-flags.md)それぞれで個別に定義されて[トレース プロバイダー](trace-provider.md)します。 その結果、プロバイダーを 1 つのフラグの値を意味フラグの値から、まったく異なるエンティティ別のプロバイダーのします。 値を解釈するには、プロバイダーを理解する必要があります。

通常、トレース フラグは、しだいに詳細レポートのレベルを表します。

フラグの値は、WPP で定義されている\_定義\_のビット要素、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロは、この例のようになど。

```
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
        WPP_DEFINE_BIT(Error)  \
        WPP_DEFINE_BIT(Unusual)  \
        WPP_DEFINE_BIT(Noise) )
```

Windows が各 WPP に割り当てます\_定義\_ビット要素 1 で始まるを連続するビット値。 たとえば、最初ビット (エラー) (異常な)、2 番目のビットを 2 と 3 番目のビット (ノイズ) を 4 に 1 を割り当てます。

開始すると、[トレース セッション](trace-session.md)フラグを表すビット値を使用します。 たとえば、次のコマンドを使用して[Tracelog](tracelog.md)でトレース セッションを開始する、[トレース プロバイダー](trace-provider.md)前に定義します。 4 (ノイズ) フラグの値に設定します。

```
tracelog -start MyTrace -guid MyDriver.guid -flags 4
```









