---
title: 既定の NDIS ポート
description: 既定の NDIS ポート
ms.assetid: a9edf83f-9226-4c75-a04e-1879a05df24c
keywords:
- WDK NDIS、既定のポート
- NDIS WDK、NDIS の既定のポートをポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17608f7871b4878163ddeb5653d625015ce77d30
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354609"
---
# <a name="default-ndis-port"></a>既定の NDIS ポート





ポート 0 は、ミニポート アダプタの既定のポートとして予約されています。 場合、 *PortNumber*任意の関数のパラメーターまたは**PortNumber**ミニポート ドライバーが任意のポートを割り当てられなかったゼロ、いずれかまたは現在のアクティビティは特定のポートではありません、任意の構造体のメンバーに設定されています。

NDIS の既定のポートの良い例では、負荷分散とフェールオーバー (LBFO) のマルチプレクサー中間ドライバーを検討してください。 このようなドライバーの仮想ミニポート ポート 0 を指定できます (既定のポート)。 中間のドライバーは、基になるミニポート アダプターにポートをポートの数 1 からまでのポート番号で割り当てることができます (*N*)。 上にある、ドライバーはポート LBFO ドライバーは、基になるポートのいずれかを選択する 0 にデータを送信する可能性がありますまたは上にあるドライバーは 1 ~ からのポート番号を指定できます*N*送信操作の特定のポートを選択します。

ミニポート ドライバーは、任意のポートの割り当てまたは既定のポート以外の任意のポート番号をサポートする必要はありません。 NDIS が既定のポートを割り当てるし、ミニポート ドライバーの呼び出し後にアクティブ化して場合でも、ミニポート ドライバーがポートを割り当てられません、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)登録を設定する関数属性、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造体。 ミニポート ドライバーが既定の操作を開始できますポート**NdisMSetMiniportAttributes**が正常に終了します。 NDIS が既定のポートを解放するミニポート ドライバーがから戻るときにここで、 [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数。

 

 





