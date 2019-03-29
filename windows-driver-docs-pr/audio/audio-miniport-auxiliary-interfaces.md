---
title: オーディオ ミニポート補助のインターフェイス
description: オーディオ ミニポート補助のインターフェイス
ms.assetid: cda22e86-f3f7-430c-856d-a2c868caa975
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a13664b1c4fb2c557773b8ddd9ee21781ad5fb53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571687"
---
# <a name="audio-miniport-auxiliary-interfaces"></a>オーディオ ミニポート補助のインターフェイス


## <span id="ddk_audio_miniport_auxiliary_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_AUXILIARY_INTERFACES_KS"></span>


ミニポート ドライバーによっては、省略可能な補助型のインターフェイスをサポートし、特殊なミニポート ドライバー機能へのアクセスを指定します。 このセクションでは、ミニポート ドライバーによって実装され、ポート ドライバーに公開される補助インターフェイスについて説明します。

このセクションでは、次のインターフェイスがについて説明します。

[IMusicTechnology](https://msdn.microsoft.com/library/windows/hardware/ff536778)- Dmu ミニポート ドライバーのピンのデータ範囲で指定されている DirectMusic シンセサイザー テクノロジの変更に使用されます。

[IPinCount](https://msdn.microsoft.com/library/windows/hardware/ff536832) -ミニポート ドライバーを動的に監視し、その pin カウントの操作の手段を提供します。

[IPinName](https://msdn.microsoft.com/library/windows/hardware/ff536840) -ポートのエンドポイントの名前を動的に更新するドライバーを使用します。

[IAdapterPnpManagement](https://msdn.microsoft.com/library/windows/hardware/mt604850) -管理メッセージ PnP 受け取りを登録するアダプターを使用します。

 

 





