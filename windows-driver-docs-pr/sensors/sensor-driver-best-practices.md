---
title: センサードライバーのベストプラクティス
description: センサードライバーのベストプラクティス
ms.assetid: adb20558-aa94-41a9-9d26-9d757bdb0999
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 63794fd8792f6220e4ff04a54a34c29e10821faf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845500"
---
# <a name="sensor-driver-best-practices"></a>センサードライバーのベストプラクティス


このセクションでは、センサードライバーのベストプラクティスについて説明します。

## <a name="windows-hardware-certification-program-requirements"></a>Windows ハードウェア認定プログラムの要件

Windows ハードウェア認定プログラムを使用すると、ハードウェアの製造元は、デバイスが Windows を操作するために必要な標準を満たしていることを証明する認定を受けることができます。 このプログラムは、すべてのセンサーの要件と、位置センサーとアンビエント光センサーの特定の要件を提供します。 センサードライバーをすべての Windows ハードウェア認定プログラムの要件に準拠させる必要があります。

一般に、この WDK ドキュメントに記載されている推奨事項は、プログラムの要件と一致します。 ただし、認定のために送信するセンサードライバーを作成する場合は、Windows ハードウェア認定プログラムの公式プログラムに関するドキュメントを参照する必要があります。 Windows ハードウェア認定プログラムの詳細については、 [Windows Hardware Developer Central](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))の web サイトを参照してください。

## <a name="performance"></a>パフォーマンス

Location API とセンサー API を使用する場合は、次の推奨事項に従ってセンサーのパフォーマンスを最適化します。

-   [**ISensorDriver:: OnClientSubscribeToEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents)と[**ISensorDriver:: OnClientUnsubscribeFromEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientunsubscribefromevents)の呼び出しを使用して、どのプログラムがイベントを監視しているかを追跡します。 クライアントがサブスクライブされていない場合にイベントの発生を停止します。

-   イベントを発生させる頻度のヒントとして、センサーの\_プロパティ\_現在の\_レポート\_間隔の値を使用します。 推奨される間隔の間だけイベントを発生させて、ドライバーが提供するデータのフィルター処理を防止します。

-   現在のレポート間隔の設定の詳細については、「[データのフィルター選択](filtering-data.md)」を参照してください。

-   この操作を実行できる場合は、要求された最短のレポート間隔よりも頻繁にイベントを発生させないようにします。

-   要求されたときにデータを提供します。 プログラムでデータのポーリングを実行しないことをお勧めしますが、Api ではこれらの同期要求が制限されません。 適切な場合は、キャッシュされたデータを提供できます。

## <a name="properties-and-data-fields"></a>プロパティとデータフィールド

プロパティとデータフィールドには、次の要件が適用されます。

-   [プロパティ](sensor-properties.md)を設定または返す場合、ドライバーは正しい型を使用する必要があります。

-   [データフィールド](sensor-categories--types--and-data-fields.md)を返すには、ドライバーで正しい種類を使用する必要があります。

## <a name="events"></a>イベント

センサーイベントには、次の推奨事項が適用されます。

-   現在のレポートの間隔が経過し、変更の感度が超過した場合にのみ、データ更新イベントを発生させます。 これは、デバイスのファームウェアの機能の大部分です。 ただし、ドライバーは複数のクライアントを判別する必要があります。 詳細については、「[センサードライバーイベントについて](about-sensor-driver-events.md)」を参照してください。

## <a name="related-topics"></a>関連トピック
センサーの[場所センサー](https://docs.microsoft.com/windows-hardware/drivers/gnss/writing-a-location-sensor-driver)ドライバーの書き込み[
センサー](supporting-ambient-light-sensors.md) [の地理位置情報ドライバーのサンプル
します](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)。



