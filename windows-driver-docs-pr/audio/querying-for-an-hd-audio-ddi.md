---
title: HD オーディオ DDI のクエリ
description: HD オーディオ DDI のクエリ
ms.assetid: 972bce92-0ecd-486a-a9a8-fcd434ad12a5
keywords:
- HD オーディオ、クエリを実行します。
- 高解像度オーディオ (HD オーディオ) クエリを実行します。
- クエリの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12e61ddceb239d25bdc7d59c1c5f8f82dc81bd66
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355282"
---
# <a name="querying-for-an-hd-audio-ddi"></a>HD オーディオ DDI のクエリ


関数のドライバー、オーディオまたはモデムのコーデックを送信します、HD オーディオ DDI を持つオブジェクトへの参照をカウントを取得する、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)HD オーディオ バス ドライバーに IOCTL します。

Windows Vista 以降では、HD オーディオ バス ドライバーのサポート、 [ **HDAUDIO\_BUS\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)と[ **HDAUDIO\_バス\_インターフェイス\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2) DDI のバージョン。 サポートされていません、 [ **HDAUDIO\_BUS\_インターフェイス\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)バージョン。

HD オーディオのバス ドライバーは、Windows Server 2003 および Windows XP でのアップグレードとしてインストールできます。 このバス ドライバーには、両方の DDI バージョンがサポートしています。

HDAUDIO への参照を取得するためのプロシージャ\_BUS\_インターフェイス、HDAUDIO\_BUS\_インターフェイス\_V2 および、HDAUDIO\_BUS\_インターフェイス\_DDI の BDL バージョンは次のセクションで説明します。

[取得、HDAUDIO\_BUS\_インターフェイス DDI オブジェクト](obtaining-an-hdaudio-bus-interface-ddi-object.md)

[取得、HDAUDIO\_BUS\_インターフェイス\_V2 DDI オブジェクト](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)

[取得、HDAUDIO\_BUS\_インターフェイス\_BDL DDI オブジェクト](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)

 

 




