---
title: WDI 全般データパス インターフェイス
description: このセクションには、一般的な WDI データパス インターフェイスがについて説明します
ms.assetid: 5B40171C-4E5F-4C35-A6E7-1EA5181C02E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d12c26e570cd869624a354e4e1247d68c8f193d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528717"
---
# <a name="wdi-general-datapath-interfaces"></a>WDI 全般データパス インターフェイス


## <a name="80211-frame-handling-and-frame-metadata"></a>802.11 フレームの処理とフレームのメタデータ


WDI との形式で話して間 802.11 フレームで渡される[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388) (NBL) チェーン。 各 NBL では、1 つ MSDU を表します。 マクロ、を通じては、NBL 構造体は、データ バッファーとオペレーティング システムの設定、Wi-fi TX メタデータを含むメタデータへのアクセスでの操作を提供します。 構造体は、そのコンテキストを使用して拡張および**MiniportReserved**メンバー。 **MiniportReserved\[0\]** 型のバッファーを指す[ **WDI\_フレーム\_メタデータ**](https://msdn.microsoft.com/library/windows/hardware/dn897827)します。 コールバックを使用して RX パスで話してと TX パスが、WDI によって、このバッファーが割り当てられている[ *NdisWdiAllocateWiFiFrameMetaData*](https://msdn.microsoft.com/library/windows/hardware/mt297597)します。 話して MiniportReserved を使用して\[1\]を追加するフレームのメタデータを格納します。

## <a name="datapath-management-requests-and-indications"></a>データパス管理要求と表示


データパス管理要求とを示す値関数のリファレンスを参照してください。 [WDI データパス管理機能](https://msdn.microsoft.com/library/windows/hardware/mt297634)します。

## <a name="related-topics"></a>関連トピック


[**NDIS\_WDI\_データ\_API**](https://msdn.microsoft.com/library/windows/hardware/mt297620)

[**NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

[*NdisWdiAllocateWiFiFrameMetaData*](https://msdn.microsoft.com/library/windows/hardware/mt297597)

[**WDI\_フレーム\_メタデータ**](https://msdn.microsoft.com/library/windows/hardware/dn897827)

 

 






