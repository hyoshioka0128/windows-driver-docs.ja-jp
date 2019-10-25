---
title: HD オーディオ DDI のクエリ
description: HD オーディオ DDI のクエリ
ms.assetid: 972bce92-0ecd-486a-a9a8-fcd434ad12a5
keywords:
- HD audio, クエリ
- High Definition Audio (HD audio)、クエリ
- WDK オーディオを照会する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92f093863cd5b0478a8071acbfe5a16dcc1b35d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832443"
---
# <a name="querying-for-an-hd-audio-ddi"></a>HD オーディオ DDI のクエリ


HD audio DDI を使用してオブジェクトへのカウントされた参照を取得するために、オーディオまたはモデムコーデックの関数ドライバーは、 [**IRP\_\_のクエリを\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)して hd オーディオバスドライバーに送信します。

Windows Vista 以降では、HD オーディオバスドライバーは、 [**hdaudio\_bus\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)、および[**hdaudio\_bus\_インターフェイス\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)バージョンの DDI をサポートしています。 [**Hdaudio\_BUS\_INTERFACE\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)バージョンはサポートされていません。

HD オーディオバスドライバーは、Windows Server 2003 および Windows XP でアップグレードとしてインストールできます。 このバスドライバーでは、両方の DDI バージョンがサポートされています。

HDAUDIO\_BUS\_インターフェイスへの参照を取得する手順、HDAUDIO\_BUS\_INTERFACE\_V2、および HDAUDIO\_BUS\_INTERFACE\_BDL バージョンの DDI の詳細については、「」を参照してください。次のセクション:

[HDAUDIO\_BUS\_INTERFACE DDI オブジェクトの取得](obtaining-an-hdaudio-bus-interface-ddi-object.md)

[\_V2 DDI オブジェクトの HDAUDIO\_BUS\_INTERFACE の取得](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)

[HDAUDIO\_BUS\_インターフェイス\_BDL DDI オブジェクトの取得](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)

 

 




