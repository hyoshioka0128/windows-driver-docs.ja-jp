---
title: Fusion センサーの実装の詳細
description: このセクションでは、Windows fusion センサー ドライバー スタックに関する実装の詳細を提供します。
ms.assetid: B53D76AC-127C-4B5A-B908-A647D2B3F164
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: bfff1b8c8357b5b6e706fdf5eea4f6b8b193974a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386191"
---
# <a name="fusion-sensor-implementation-details"></a>Fusion センサーの実装の詳細


このセクションでは、Windows fusion センサー ドライバー スタックに関する実装の詳細を提供します。

>[!NOTE]
>Fusion のドライバー バイナリ一部のプラットフォームで提供し、これらのパートナーによっては置き換えることができません。

 

次の図は、センサー フュージョン ソフトウェア スタックを示します。

![fusion のセンサーのスタックを示す図](images/fusion-sensor-stack.png)

Fusion のソフトウェア スタックは、次のコンポーネントで構成されます。

-   **センサー ネイティブ Api**融接およびコンパスの機能や機能にアクセスするアプリケーションによって呼び出されます。 Api は、ReadFile や DeviceIoControl のラッパーです。 これらの Api はセンサー クラスの拡張を処理し、要求を完了に送信されます。

-   **センサー クラス拡張**任意の必要なセンサーに固有の機能拡張のサポートを提供します。

-   **Fusion ドライバー**は、ドライバーの関数に固有のソフトウェアの一部です。 物理センサーの読み取りし、データを処理します。 コンパスと融接センサーのアルゴリズムは、このコンポーネントに実装されます。

## <a name="coordinate-systems"></a>座標系


次の図に示すように座標系は、すべての物理センサーと fusion データに使用されます。

![ジャイロスコープ デバイスの向きを示す図](images/gyroscope-orientation.png)

次の図に示すように、座標システム/アースの基準枠ですべてのベクトルの fusion アルゴリズムおよび Api によって使用される規則があります。

![fusion アルゴリズムで使用される地球座標系を示す図](images/earth-coordinatesystem.png)

<!--
//commenting out for now, all these links are bad.
## Data structures


The following structures and enumerations are used by the fusion data part of the logical sensor driver:

-   [**VEC3D**](https://docs.microsoft.com/windows-hardware/drivers/sensors/)

-   [**COORDINATE\_AXIS**](https://docs.microsoft.com/windows-hardware/drivers/sensors/)

-   [**QUATERNION**](https://docs.microsoft.com/windows-hardware/drivers/sensors/)

-   [**MATRIX3X3**](https://docs.microsoft.com/windows-hardware/drivers/sensors/)

-   [Fusion sensor enumerations](https://go.microsoft.com/fwlink/p/?linkid=839352) and [Fusion sensor structures](https://go.microsoft.com/fwlink/p/?linkid=839355) provide information about the entire sensor fusion data structure, which include the attitude (in multiple formats) and the linear acceleration, and the compass data.
-->
 

 




