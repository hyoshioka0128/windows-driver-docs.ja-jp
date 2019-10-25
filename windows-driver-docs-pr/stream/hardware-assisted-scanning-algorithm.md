---
title: ハードウェア補助スキャン アルゴリズム
description: ハードウェア補助スキャン アルゴリズム
ms.assetid: 9a24b985-9667-4424-84e5-b1c728b3c558
keywords:
- ハードウェア支援型のスキャン (WDK ビデオキャプチャ)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85ce3b4466638ce7d71f8b4f214a1bb7f59026b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843353"
---
# <a name="hardware-assisted-scanning-algorithm"></a>ハードウェア補助スキャン アルゴリズム


**このセクションは、Microsoft Windows Vista 以降のオペレーティングシステムにのみ適用されます。**

ドライバーは、Ksk プロパティの**fSupportsHardwareAssistedScanning**メンバー [ **\_チューナー\_スキャン\_caps\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)構造体を設定します。これは、 [**ksk プロパティ\_チューナー**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-caps)への呼び出しで、スキャン\_キャップを\_プロパティは、それがイベントベースのスキャン操作をサポートしていることを示します。 チューナーフィルター (*KsTvTune.ax*) は、ドライバーの ksk プロパティ\_チューナー\_スキャン\_CAPS プロパティを呼び出して、ドライバーがハードウェア支援型のスキャンをサポートしているかどうかを判断します。 また、チューナーフィルターでは、KSK プロパティ\_チューナー\_スキャン\_CAPS を呼び出して、ドライバーがスキャンをサポートしているブロードキャストネットワークの種類を特定します。 ドライバーがハードウェア支援型のスキャンをサポートしている場合、サポートされている各ブロードキャストネットワークの種類について、その[**Ksk プロパティ\_チューナー\_NETWORKTYPE\_SCAN\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-networktype-scan-caps)プロパティを通じて、スキャン機能を返すことができます。 スキャン機能には、たとえば、周波数設定を安定した状態にするためにチューニングデバイスが必要とする時間 (時間がかかる) を提供し、チューニングフィルターが調整可能なの存在を特定するために使用できる頻度の範囲を指定します。signal (検出範囲)。 アナログブロードキャストネットワークのスキャン機能の詳細については、「[**チューナー\_アナログ\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tuner_analog_caps_s)構造体」を参照してください。

*KsTvTune.ax*は、値を近似値として使用します。 *KsTvTune.ax*は、スキャンの頻度と範囲に基づいて、スキャンプロセスにかかる時間の見積もりをアプリケーションに提供できます。 ドライバーの[**KSEVENT\_チューナー\_開始\_スキャン**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan)イベントが呼び出され、スキャンプロセスが開始されると、アプリケーションは、規定された時間のイベント通知を待機できます。

ハードウェア支援型のスキャンでは、チューニングデバイスがシグナルにロックされているかどうかによって、ドライバーは、\_LockType\_None またはチューナー\_LockType プロパティの呼び出しからロック状態\_ロック状態を返し[ **\_チューナー\_SCAN\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status)プロパティ。 ドライバーがシグナルにロックされている場合、ドライバーはロックされたシグナルの頻度も返します。

 

 




