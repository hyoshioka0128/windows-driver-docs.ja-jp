---
title: NFC の電源管理
description: NFC の電源管理
ms.assetid: 7B45730F-A49D-45E0-B314-0464141E3C8B
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83989b3d8ce74f3110da0453c69e635c9776173e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537831"
---
# <a name="nfc-power-management"></a>NFC の電源管理


NFC ドライバーでは、デバイスの電源の状態をインテリジェントに管理ものとします。 NFC のドライバーを提供する ihv 向けの一般的なガイドラインを次に示します。

**近接の電源管理します。** Active 近接パブリケーション、サブスクリプション、または、保留中のスマート カードの存在/ない操作がない場合、または近接ラジオの状態が無効になっている場合は、NFC ドライバーには、探索/ポーリング ループの P2P とタグの検出部分が非アクティブ化可能性があります。

**要素の電源管理をセキュリティで保護します。** エミュレーションでは、リーダーをセキュリティで保護された要素がない公開されている場合、またはセキュリティで保護された要素のオプションの状態が無効になっている場合は、NFC ドライバーには、探索/ポーリング ループのカード エミュレーション部分が非アクティブ化可能性があります。

**全体的な電源管理をします。** 近接とカードの両方のエミュレーション操作が非アクティブな場合、NFC ドライバー可能性がありますの電源を切るデバイス完全に (システム S0 状態にある) 場合は、アイドル状態の電源管理を使用して低電力状態 (D3 状態) に遷移するとします。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  


