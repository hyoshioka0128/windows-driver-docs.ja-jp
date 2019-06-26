---
title: センサー ドライバーの記述に関する考慮事項
description: センサー ドライバーの記述に関する考慮事項
ms.assetid: fec3cfe8-43ad-481a-833a-6f38d04bfdef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30e4955a24aeecf96b96d8993fbbf2326f73d71f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364904"
---
# <a name="considerations-for-writing-a-sensor-driver"></a>センサー ドライバーの記述に関する考慮事項


センサー ドライバーを記述する前に、次の重要な質問を考慮する必要があります。 このプロセスにより、さまざまな設計と実装の決定を行う。

-   ドライバーが複数のセンサーまたは 1 つのセンサーをサポートしているかどうかを決定します。 たとえば、ハードウェア デバイスは、センサーの組み合わせを含めることができますが、1 つのデバイス ドライバーを使用することがあります。

-   デバイスで、必要な操作のレベルを決定し、プラットフォームにイベントを送信、かどうか。 (ほとんどのドライバー、およびセンサー ソリューションをサポートするイベントです。)センサー ドライバーのイベントの概要については、次を参照してください。[センサー ドライバー イベントについて](about-sensor-driver-events.md)します。

-   カテゴリ、センサーの種類、およびドライバーのデータ型を決定します。 プラットフォーム定義されている並べ替え方法のいずれかを使用して、または独自に定義することができます。 プラットフォームがセンサーの情報を整理する方法の概要については、次を参照してください[センサー定数について。](about-sensor-constants.md)

## <a name="related-topics"></a>関連トピック
[センサー地理位置情報ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)  



