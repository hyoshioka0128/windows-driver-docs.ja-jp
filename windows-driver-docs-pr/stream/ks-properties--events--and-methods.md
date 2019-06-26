---
title: KS のプロパティ、イベント、メソッド
description: KS のプロパティ、イベント、メソッド
ms.assetid: 933bbe81-92d8-4bcc-b935-9ae929464ca1
keywords:
- カーネルの WDK、プロパティをストリーミングします。
- ストリーミング KS プロパティ WDK カーネル
- カーネルの WDK、イベントのストリーミング
- KS WDK、イベント
- カーネルの WDK、メソッドのストリーミング
- KS WDK、メソッド
- ストリーミング プロパティ WDK カーネル
- ストリーミング イベント WDK カーネル
- ストリーミング メソッド WDK カーネル
- エイリアスの構造体の WDK カーネルがストリーミング
- WDK のカーネル ストリーミングの操作を設定します。
- WDK のカーネル ストリーミングの操作を取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb64892140522d443fa4d845c63ddaffbc21187
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382491"
---
# <a name="ks-properties-events-and-methods"></a>KS のプロパティ、イベント、メソッド





ストリーミング アーキテクチャ カーネルを通じてミニドライバーとユーザー モードのクライアント間の相互作用をサポートしている[プロパティ](ks-properties.md)、[イベント](ks-events.md)、および[メソッド](ks-methods.md)します。 これらのコンストラクトを使用して、クライアント KS オブジェクトのことができます取得しオブジェクトの状態を設定、イベントの通知コールバックを登録およびオブジェクトのメソッドを実行します。

クライアントは、標準化された方法で 3 つの操作のすべてのクラスを要求します。 クライアントのエイリアス構造体を提供する[ **KSIDENTIFIER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)への呼び出しで**DeviceIoControl** (Microsoft Windows SDK のドキュメントで説明) または[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)します。

エイリアスの構造体が[ **KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)、 [ **KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))、および[ **KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85)). 3 つすべては、次のパラメーターです。

-   **設定**

    機能的によく似た操作は、一連のグループ化されます。 各プロパティ、イベント、またはメソッドのセットは、GUID によって識別されます。 Microsoft では、標準的なテクノロジに特化した操作の Guid を定義します。 ミニドライバーは、カスタム操作の独自の Guid を定義できます。

-   **[Identifier]**

    各操作は、セット内の ID 番号を指定します。

-   **操作に固有の id データ**

    特定のプロパティの要求では、追加のデータが必要です。 など、オーディオ デバイス サポートのピン留め、 [KSPROPSETID\_オーディオ](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audio)プロパティ セット。 オーディオの pin には、いくつかの異なるオーディオ チャンネルをサポートできます。 クライアントを取得または設定の特定 KSPROPSETID\_オーディオのプロパティは、要求を適用するオーディオ チャネルを指定する必要があります。 イベントとメソッドの要求では、追加のデータは必要ありません。

Microsoft 定義セット Guid および汎用的な操作の識別子がヘッダーにある*ks.h*します。 標準の Guid とマルチ メディア テクノロジの特定のクラスの識別子は、「 *ksmedia.h*します。

AVStream ミニドライバーへのポインターを提供することで、プロパティ、イベント、およびメソッドをサポートする、 [ **KSAUTOMATION\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksautomation_table_)構造、関連する[ **KSFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)または[ **KSPIN\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)します。 KSAUTOMATION\_テーブルの配列へのポインターを格納する[ **KSPROPERTY\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_set)オブジェクト。 詳細についてを参照してください。 [Automation テーブルを定義する](defining-automation-tables.md)します。

これらのセクションには、ミニドライバーが 3 つの操作のクラスをサポートする方法に関する情報が含まれます。

[KS プロパティ](ks-properties.md)

[KS イベント](ks-events.md)

[KS メソッド](ks-methods.md)

 

 




