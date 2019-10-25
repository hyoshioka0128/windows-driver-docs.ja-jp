---
title: NFC 電源管理
description: NFC 電源管理
ms.assetid: 7B45730F-A49D-45E0-B314-0464141E3C8B
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdfac29b49b9c670bfa77128c79196382c48cbf4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842268"
---
# <a name="nfc-power-management"></a>NFC 電源管理


NFC ドライバーは、デバイスの電源状態をインテリジェントに管理する必要があります。 NFC ドライバーを提供する Ihv 向けの一般的なガイドラインを次に示します。

**近接電源管理。** アクティブな近接するパブリケーション、サブスクリプション、またはスマートカードの存在/存在しない操作が保留されていない場合、または近接無線の状態が無効になっている場合、NFC ドライバーは、検出/ポーリングループの P2P およびタグ検出部分を非アクティブ化する可能性があります。

**セキュリティで保護された要素の電源管理。** セキュリティで保護された要素がエミュレーションを通じてリーダーに公開されない場合、または secure element 無線状態が無効になっている場合、NFC ドライバーは検出/ポーリングループのカードエミュレーション部分を非アクティブ化する可能性があります。

**全体的な電源管理。** 近接とカードの両方のエミュレーション操作が非アクティブ化されている場合、NFC ドライバーはアイドル状態 (システムが S0 の場合) を使用して低電力状態 (D3 状態) に移行することで、デバイスの電源を完全に切ることができます。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  


