---
title: Hyper-v 拡張可能スイッチポートに関するトピック
description: Hyper-v 拡張可能スイッチポートに関するトピック
ms.assetid: A9A07C71-BA64-4223-8402-254D87810167
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88a18f493516778f719706eb80ed2aeea2c6cffb
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565672"
---
# <a name="hyper-v-extensible-switch-ports-topics"></a>Hyper-v 拡張可能スイッチポートに関するトピック


ここでは、Hyper-v 拡張可能スイッチポートの特性について説明する次のトピックについて説明します。

[Hyper-v 拡張可能スイッチポートの概要](overview-of-hyper-v-extensible-switch-ports.md)

[検証ポート](validation-ports.md)

[操作ポート](operational-ports.md)

**注 NDIS ポート**と拡張可能なスイッチポートは異なるオブジェクトです  。 拡張可能なスイッチのデータパスを通過するパケットは、常に ndis ポート番号 **(\_ndis\_の\_既定のポート**番号) に割り当てられます。 ただし、パケットの発信元と宛先の拡張可能スイッチのポート番号には **、\_NDIS\_スイッチ\_の\_既定のポート ID**以上の値を指定できます。 詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。

 

 

 





