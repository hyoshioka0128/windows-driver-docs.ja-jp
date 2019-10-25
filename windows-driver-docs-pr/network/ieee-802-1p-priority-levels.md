---
title: IEEE 802.1p 優先順位のレベル
description: IEEE 802.1p 優先順位のレベル
ms.assetid: C7EB3D85-544E-4898-A456-843621F6488D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa371d0aa3c86aebf8416254adbb34a248ff273e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823823"
---
# <a name="ieee-8021p-priority-levels"></a>IEEE 802.1p 優先順位のレベル


Ieee 802.1 タスクグループによって、サービスの品質 (QoS) のトラフィックの優先順位付けに対応するように ieee 802.1 p が指定されました。 802.1 p は別個の IEEE 802.1 標準ではありませんが、IEEE 802.1 Q-2005 標準の付属の G で定義されています。

IEEE 802.1 p は、IEEE 802.1 Q タグ内の優先度コードポイント (PCP) と呼ばれる3ビットフィールドを定義します。 NDIS パケットの場合、802.1 p PCP 値は、パケットの Net\_バッファーに関連付けられている[**ndis\_net\_BUFFER\_LIST\_8021Q\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)構造体の**userpriority**メンバーによって指定され[ **\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体。

PCP 値は8つの優先度レベルを定義し、最も高い優先度と1つの優先度を定義します。 既定では、優先度のレベルは0です。 各優先度レベルは、送信パケットの個別のトラフィッククラスを識別する*サービスのクラス*を定義します。

 

 





