---
title: IEEE 802.1p の優先度レベル
description: IEEE 802.1p の優先度レベル
ms.assetid: C7EB3D85-544E-4898-A456-843621F6488D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92c91917211c16566728241d5999597a03d2e129
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551462"
---
# <a name="ieee-8021p-priority-levels"></a>IEEE 802.1p の優先度レベル


IEEE 802.1p は、IEEE 802.1 タスクで指定されたサービスの品質 (QoS) のトラフィックの優先順位付けに対処するグループ。 802.1p は、個別の IEEE 802.1 標準ではありませんが、IEEE 802.1 q の Annex G で定義されている-2005 standard。

IEEE 802.1 q 内で優先度コード ポイント (PCP) と呼ばれる 3 ビット フィールドを定義する IEEE 802.1p タグ。 NDIS パケットの場合、802.1 p PCP の値がで指定された、 **UserPriority**のメンバー、 [ **NDIS\_NET\_バッファー\_一覧\_8021Q\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566565)構造に関連付けられたパケットの[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

最高の優先順位と 1、PCP 値は 7 と 8 の優先度レベルを定義します。 最も低い優先順位。 0 の優先度レベルでは、既定値です。 各優先度レベルを定義、*サービス クラス*転送されたパケットの別のトラフィック クラスを識別します。

 

 





