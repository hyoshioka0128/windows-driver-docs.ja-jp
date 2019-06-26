---
title: IEEE 802.1p 優先順位のレベル
description: IEEE 802.1p 優先順位のレベル
ms.assetid: C7EB3D85-544E-4898-A456-843621F6488D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52ae6167aaa42d9ef14f82344a22fb09d3f9a3c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384548"
---
# <a name="ieee-8021p-priority-levels"></a>IEEE 802.1p 優先順位のレベル


IEEE 802.1p は、IEEE 802.1 タスクで指定されたサービスの品質 (QoS) のトラフィックの優先順位付けに対処するグループ。 802.1p は、個別の IEEE 802.1 標準ではありませんが、IEEE 802.1 q の Annex G で定義されている-2005 standard。

IEEE 802.1 q 内で優先度コード ポイント (PCP) と呼ばれる 3 ビット フィールドを定義する IEEE 802.1p タグ。 NDIS パケットの場合、802.1 p PCP の値がで指定された、 **UserPriority**のメンバー、 [ **NDIS\_NET\_バッファー\_一覧\_8021Q\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)構造に関連付けられたパケットの[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。

最高の優先順位と 1、PCP 値は 7 と 8 の優先度レベルを定義します。 最も低い優先順位。 0 の優先度レベルでは、既定値です。 各優先度レベルを定義、*サービス クラス*転送されたパケットの別のトラフィック クラスを識別します。

 

 





