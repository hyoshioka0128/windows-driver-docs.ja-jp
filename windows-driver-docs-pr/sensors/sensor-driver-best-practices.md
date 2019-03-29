---
title: センサー ドライバーのベスト プラクティス
description: センサー ドライバーのベスト プラクティス
ms.assetid: adb20558-aa94-41a9-9d26-9d757bdb0999
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 08bbeaf79f0cb6e91fc0ee847df4b1211c8644bc
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136111"
---
# <a name="sensor-driver-best-practices"></a>センサー ドライバーのベスト プラクティス


このセクションでは、センサー ドライバーのベスト プラクティスについて説明します。

## <a name="windows-hardware-certification-program-requirements"></a>Windows ハードウェア認定プログラム要件

Windows ハードウェア認定プログラムには、ハードウェアの製造元を自分のデバイスが Windows を操作するための必要な基準を満たす証明書を受信するができます。 プログラムでは、すべてのセンサーの要件と場所のセンサーと周辺光センサーの特定の要件を提供します。 すべての Windows ハードウェア認定プログラム要件を満たすには、センサー ドライバーをする必要があります。

一般に、この WDK ドキュメントの推奨事項では、プログラムの要件と一致します。 ただし、証明書を送信するセンサー ドライバーを作成するときに、Windows ハードウェア認定プログラムの公式ドキュメントを確認する必要があります。 Windows ハードウェア認定プログラムに関する詳細については、次を参照してください。、 [Windows Hardware Developer Central](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) web サイト。

## <a name="performance"></a>パフォーマンス

Location API とセンサーの API を使用する場合は、センサーのパフォーマンスを最適化するためにこれらの推奨事項に従います。

-   呼び出しを使用して、 [ **ISensorDriver::OnClientSubscribeToEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents)と[ **ISensorDriver::OnClientUnsubscribeFromEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientunsubscribefromevents)にすべてのプログラムはイベントを監視するかどうかを追跡。 クライアントがサブスクライブしていないときのイベントの発生を停止します。

-   センサーの指定された値を使用して、\_プロパティ\_現在\_レポート\_多くの場合、イベントを発生させる方法のヒントとしての間隔。 中にのみ、またはお使いのドライバーのデータのフィルター処理を防ぐために推奨される間隔の後にイベントを発生させます。

-   現在のレポート間隔を設定する方法の詳細については、次を参照してください。、[データのフィルター処理](filtering-data.md)トピック。

-   これを行うことができる場合、要求された最短のレポート間隔よりもしないより頻繁にイベントを発生させます。

-   要求されたときにデータを提供します。 プログラムは、データのポーリングによって控えることをお勧め、Api はこれらの同期要求が制限されません。 適切なタイミングは、キャッシュされたデータを行うことができます。

## <a name="properties-and-data-fields"></a>プロパティとデータ フィールド

プロパティとデータ フィールドに、次の要件が適用されます。

-   ドライバーは、設定、または、返す場合は、正しい型を使用する必要があります、[プロパティ](sensor-properties.md)します。

-   返すときに、ドライバーが適切な型を使用する必要があります、[データ フィールド](sensor-categories--types--and-data-fields.md)します。

## <a name="events"></a>イベント

センサーのイベントに次の推奨事項が適用されます。

-   データ更新イベント、現在のレポート間隔が経過し、感度の変更を超えた場合にのみ発生します。 これは、デバイスのファームウェアの関数ではほとんどです。 ただし、ドライバーは、複数のクライアント間で判別する必要があります。 詳細については、次を参照してください。[センサー ドライバー イベントについて](about-sensor-driver-events.md)します。

## <a name="related-topics"></a>関連トピック
[場所のセンサー ドライバーの記述](https://docs.microsoft.com/windows-hardware/drivers/gnss/writing-a-location-sensor-driver)
[環境光センサーをサポートしている](supporting-ambient-light-sensors.md)
[センサー地理位置情報ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



