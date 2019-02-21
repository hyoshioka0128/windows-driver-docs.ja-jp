---
title: Microsoft STI の概要
description: Microsoft STI の概要
ms.assetid: b329dbbc-28c5-47df-9ced-33180415b7c6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 768ad786bdadeb33ad7640ad629254134c88a54f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528262"
---
# <a name="introduction-to-microsoft-sti"></a>Microsoft STI の概要





Microsoft STI は、次の主要なコンポーネントの構成をされます。

-   A[イメージ イベント モニターではまだ](overview-of-sti-components.md#ddk-still-image-event-monitor-si)、イメージ デバイスをまだインストールされているすべてを監視し、通知を受信とき[イメージ デバイス イベントではまだ](still-image-device-events.md)発生します。 通常、イベントは、デバイスがイメージ データを送信する準備を示します。 イベント モニターは、登録されているすべてのアプリケーションの追跡もとイベントが検出されたときに、アプリケーションを開始できます。

-   一連のベンダーから提供された[ユーザー モードのままイメージ ミニドライバー](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)デバイスのアクティビティを検出し、イメージ デバイス イベントではまだを介してアクティビティの静止画像イベント モニターに通知することができます。 これらミニドライバーも、上位レベルのソフトウェアをカーネル モード ドライバーからイメージ データを渡します。

-   A[スキャナーとカメラのコントロール パネル](overview-of-sti-components.md#ddk-scanners-and-cameras-control-panel-si)ユーザーは特定のアプリケーションに特定の静止画像デバイス イベントを割り当てできます。 この方法でイベント モニタは、イベントが検出されたときに開始するには、どのアプリケーションを認識します。 コントロール パネルでは、ユーザーがテスト デバイスのイメージではまだこともできます。

[イメージング アプリケーション](overview-of-sti-components.md#ddk-imaging-application-si)として自身を登録できる*プッシュ モデルの対応*、つまりによってアクティブになるイベント モニター静止画像デバイスがイメージを送信できます。

呼び出して、高度なイメージのデータ ストリームの読み取りイメージング アプリケーションを通常[Image Acquisition API](overview-of-sti-components.md#ddk-image-acquisition-api-si)、TWAIN など。 TWAIN データ ソースでは、イメージの取得 API のサブコンポーネントをデバイスに固有では、ユーザー モードの静止画像ミニドライバーにインターフェイスを使用して、I/O 操作を実行します。

Microsoft STI では、いくつかを定義します[COM インターフェイスのイメージも](still-image-com-interfaces.md)STI コンポーネントが互いに通信できるようにします。

次のセクションは、これらおよびその他の詳細情報を提供[Microsoft STI コンポーネント](microsoft-sti-components.md)します。

 

 




