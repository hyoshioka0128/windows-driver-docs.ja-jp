---
title: NDIS の既定のポート
description: NDIS の既定のポート
ms.assetid: a9edf83f-9226-4c75-a04e-1879a05df24c
keywords:
- WDK NDIS、既定のポート
- NDIS WDK、NDIS の既定のポートをポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcee3e9181e21c4d35bf18ae457016cfc4a5e0ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536690"
---
# <a name="default-ndis-port"></a>NDIS の既定のポート





ポート 0 は、ミニポート アダプタの既定のポートとして予約されています。 場合、 *PortNumber*任意の関数のパラメーターまたは**PortNumber**ミニポート ドライバーが任意のポートを割り当てられなかったゼロ、いずれかまたは現在のアクティビティは特定のポートではありません、任意の構造体のメンバーに設定されています。

NDIS の既定のポートの良い例では、負荷分散とフェールオーバー (LBFO) のマルチプレクサー中間ドライバーを検討してください。 このようなドライバーの仮想ミニポート ポート 0 を指定できます (既定のポート)。 中間のドライバーは、基になるミニポート アダプターにポートをポートの数 1 からまでのポート番号で割り当てることができます (*N*)。 上にある、ドライバーはポート LBFO ドライバーは、基になるポートのいずれかを選択する 0 にデータを送信する可能性がありますまたは上にあるドライバーは 1 ~ からのポート番号を指定できます*N*送信操作の特定のポートを選択します。

ミニポート ドライバーは、任意のポートの割り当てまたは既定のポート以外の任意のポート番号をサポートする必要はありません。 NDIS が既定のポートを割り当てるし、ミニポート ドライバーの呼び出し後にアクティブ化して場合でも、ミニポート ドライバーがポートを割り当てられません、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)登録を設定する関数属性、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)構造体。 ミニポート ドライバーが既定の操作を開始できますポート**NdisMSetMiniportAttributes**が正常に終了します。 NDIS が既定のポートを解放するミニポート ドライバーがから戻るときにここで、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)関数。

 

 





