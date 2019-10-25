---
title: オーディオ ミニポート補助のインターフェイス
description: オーディオ ミニポート補助のインターフェイス
ms.assetid: cda22e86-f3f7-430c-856d-a2c868caa975
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3a0b3926661436a283853361fcb97a529e7f745
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831356"
---
# <a name="audio-miniport-auxiliary-interfaces"></a>オーディオ ミニポート補助のインターフェイス


## <span id="ddk_audio_miniport_auxiliary_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_AUXILIARY_INTERFACES_KS"></span>


一部のミニポートドライバーでは、省略可能な補助インターフェイスがサポートされており、特化されたミニポートドライバー機能にアクセスできます。 このセクションでは、ミニポートドライバーによって実装され、ポートドライバーに公開される補助インターフェイスについて説明します。

このセクションでは、次のインターフェイスについて説明します。

[Imusictechnology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-imusictechnology)-dmus ミニポートドライバーの pin のデータ範囲で指定されている DirectMusic シンセサイザーテクノロジを変更するために使用されます。

[Ipincount](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-ipincount) -ミニポートドライバーが pin カウントを動的に監視および操作するための手段を提供します。

[Ipinname](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-ipinname-getpinname) -ポートドライバーがエンドポイントの名前を動的に更新できるようにします。

[IAdapterPnpManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpnpmanagement) -アダプターが PnP 管理メッセージを受信するための登録を許可します。

 

 





