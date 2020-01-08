---
title: アイドル状態の電源管理のハードディスクドライブのアイドルタイムアウト
description: アイドル状態の電源管理のハードディスクドライブのアイドルタイムアウト
ms.assetid: 1dcc261a-803c-4c0e-a68e-29b00f46cd32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 966d4b16bc415f731f9f7d89bca0753e38b72cc3
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606544"
---
# <a name="idle-power-management-hard-disk-drive-idle-timeout"></a>アイドル状態の電源管理のハードディスクドライブのアイドルタイムアウト

通常のモバイル PC では、ハードディスクドライブ (HDD) は主要な電力消費者ではありませんが、HDD メディアをスピンダウンすることで電力の節約を実現できます。 HDD のアイドルタイムアウトにより、Windows では、ディスクの読み取りと書き込みが非アクティブになった後に、HDD メディアを自動的にスピンダウンさせることができます。

HDD メディアがスピンダウンした場合に実現される電力の節約は、HDD の製造元とモデルによって異なります。 システム製造元が HDD ベンダーと協力して、特定のデバイスに最適な HDD アイドルタイムアウト値を判断することをお勧めします。

Windows Vista では、既定で、適度に長い HDD アイドルタイムアウト値が指定されています。 システムの製造元は、モバイル Pc で電力を大幅に節約するために、より短い値を指定することを検討してください。 次の表は、HDD のアイドル状態の設定の詳細をまとめたものです。

| 項目 | 説明 |
| ------ | ----------- |
| フレンドリ名     | の後にハードディスクをオフにする |
| 説明       | ハードドライブが非アクティブになってからディスクがオフになるまでの時間を指定します。 |
| PowerCfg エイリアス    | DISKIDLE |
| グループポリシーのパス | 管理用システム \ システム \ 管理 \ ハードディスク Settings\Turn |
| GUID              | 6738e2c4-e8a5-4a42-b16a-e040e769756e |
| 定義されている場所        | Ntpoapi .h |
| バランスの取れた既定値 | 60分 (AC) 30 分 (DC) |

詳細について[は、モバイルプラットフォームの専門家向けのガイドである「モバイルバッテリ寿命ソリューション](https://go.microsoft.com/fwlink/p/?linkid=144534)」を参照してください。
