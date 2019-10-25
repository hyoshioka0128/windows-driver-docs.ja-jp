---
title: KS プロパティ、イベント、およびメソッド
description: KS プロパティ、イベント、およびメソッド
ms.assetid: 933bbe81-92d8-4bcc-b935-9ae929464ca1
keywords:
- カーネルストリーミング WDK、プロパティ
- KS プロパティ WDK カーネルストリーミング
- カーネルストリーミング WDK、イベント
- KS WDK、イベント
- カーネルストリーミング WDK、メソッド
- KS WDK、メソッド
- プロパティ WDK カーネルストリーミング
- イベント WDK カーネルストリーミング
- 方法 WDK カーネルストリーミング
- エイリアス構造 WDK カーネルストリーミング
- set 操作 WDK カーネルストリーミング
- get 操作 WDK カーネル streaming
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ca8c41beb16133204e70251b1fe0d46479736f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842508"
---
# <a name="ks-properties-events-and-methods"></a>KS プロパティ、イベント、およびメソッド





カーネルストリーミングアーキテクチャは、[プロパティ](ks-properties.md)、[イベント](ks-events.md)、および[メソッド](ks-methods.md)を使用して、ミニドライバークライアントとユーザーモードクライアントの間の対話をサポートします。 これらの構成体を使用して、KS オブジェクトのクライアントは、オブジェクトの状態の取得と設定、イベントの通知コールバックの登録、およびオブジェクトメソッドの実行を行うことができます。

クライアントは、3つのすべての操作クラスを標準化された方法で要求します。 クライアントは、 **DeviceIoControl** (Microsoft Windows SDK のドキュメントで説明されています) または[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)の呼び出しで、 [**KSIDENTIFIER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)の別名構造を提供します。

エイリアス構造は、 [**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)、 [**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))、および[**ksproperty**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))です。 3つすべてに次のパラメーターが含まれます。

-   **一連**

    機能的に類似した操作は、セットにまとめてグループ化されます。 各プロパティ、イベント、またはメソッドセットは、GUID によって識別されます。 Microsoft では、標準的なテクノロジ固有の操作の Guid を定義しています。 ミニドライバーでは、独自の Guid を定義してカスタム操作を行うことができます。

-   **識別子**

    各操作は、セット内の ID 番号によって指定されます。

-   **操作固有の識別データ**

    特定のプロパティ要求には追加データが必要です。 たとえば、オーディオデバイスのピンは、 [Kspropsetid\_audio](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audio)プロパティセットをサポートしています。 オーディオ pin では、複数の異なるオーディオチャンネルがサポートされる場合があります。 特定の KSPROPSETID\_を取得または設定するクライアントは、要求が適用されるオーディオチャネルを指定する必要があります。 イベント要求とメソッド要求では、追加のデータは必要ありません。

汎用操作の Microsoft 定義セット Guid および識別子は、ヘッダー *ks*にあります。 マルチメディアテクノロジの特定のクラスの標準 Guid と識別子は、 *ksmedia. h*にあります。

AVStream ミニドライバーサポートのプロパティ、イベント、およびメソッド。関連する[**Ksk フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)または[**KSPIN\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)の[**ksautomation\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksautomation_table_)構造へのポインターを提供します。 KSAUTOMATION\_テーブルには、オブジェクト\_設定された[**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)の配列へのポインターが含まれています。 詳細については、「[オートメーションテーブルの定義](defining-automation-tables.md)」を参照してください。

これらのセクションには、ミニドライバーが3つの操作クラスをサポートする方法に関する情報が含まれています。

[KS プロパティ](ks-properties.md)

[KS イベント](ks-events.md)

[KS メソッド](ks-methods.md)

 

 




