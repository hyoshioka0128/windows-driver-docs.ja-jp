---
title: KSEVENTSETID\_LoopedStreaming
description: KSEVENTSETID\_LoopedStreaming
ms.assetid: 88baf1f0-d18f-4601-9ba3-fea957712cd6
keywords:
- KSEVENTSETID_LoopedStreaming
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 587158e7bee784222efa0bb8d0ae1e3d8ba14a2d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578744"
---
# <a name="kseventsetidloopedstreaming"></a>KSEVENTSETID\_LoopedStreaming


このイベントのセットは、システム内部使用のみのものです。

`KSEVENTSETID_LoopedStreaming`イベント セットを使用するオーディオ ストリーム内のイベント バッファーをループする位置を定義します。 ループのバッファーが型のオーディオ ストリームのデータ バッファー [ **KSINTERFACE\_標準\_るーぷさいせいぼたん\_ストリーミング**](https://msdn.microsoft.com/library/windows/hardware/ff563381)します。 位置イベントを介して、クライアントは、オーディオ ストリームがループのバッファー内の指定位置に達すると、ドライバーから通知を受信できます。

Microsoft Windows Server 2003、Windows XP、Windows 2000、Windows Me、Windows 98 で、このイベント セット用のドライバー サポートを実装する唯一のシステム コンポーネントは、KMixer および PortCls (Kmixer.sys および Portcls.sys)。 DirectSound (Dsound.dll) は、このイベントをクライアントとして設定を使用する唯一のシステム コンポーネントです。 通常、カスタムのオーディオ ドライバーでは、このイベントのセットのサポートは実装されません。

Windows Vista 以降では、システム コンポーネントがないが使用またはサポート、`KSEVENTSETID_LoopedStreaming`イベントのセット。

このセット内のイベント項目が KSEVENT として指定された\_LOOPEDSTREAMING 列挙値。

このセット内の唯一のイベントは[ **KSEVENT\_LOOPEDSTREAMING\_位置**](ksevent-loopedstreaming-position.md)します。

 

 





