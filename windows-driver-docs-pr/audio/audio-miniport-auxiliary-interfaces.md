---
title: オーディオ ミニポート補助のインターフェイス
description: オーディオ ミニポート補助のインターフェイス
ms.assetid: cda22e86-f3f7-430c-856d-a2c868caa975
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15180ea52e96ee0759501206825a5727817296ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355685"
---
# <a name="audio-miniport-auxiliary-interfaces"></a>オーディオ ミニポート補助のインターフェイス


## <span id="ddk_audio_miniport_auxiliary_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_AUXILIARY_INTERFACES_KS"></span>


ミニポート ドライバーによっては、省略可能な補助型のインターフェイスをサポートし、特殊なミニポート ドライバー機能へのアクセスを指定します。 このセクションでは、ミニポート ドライバーによって実装され、ポート ドライバーに公開される補助インターフェイスについて説明します。

このセクションでは、次のインターフェイスがについて説明します。

[IMusicTechnology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-imusictechnology)- Dmu ミニポート ドライバーのピンのデータ範囲で指定されている DirectMusic シンセサイザー テクノロジの変更に使用されます。

[IPinCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-ipincount) -ミニポート ドライバーを動的に監視し、その pin カウントの操作の手段を提供します。

[IPinName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-ipinname-getpinname) -ポートのエンドポイントの名前を動的に更新するドライバーを使用します。

[IAdapterPnpManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpnpmanagement) -管理メッセージ PnP 受け取りを登録するアダプターを使用します。

 

 





