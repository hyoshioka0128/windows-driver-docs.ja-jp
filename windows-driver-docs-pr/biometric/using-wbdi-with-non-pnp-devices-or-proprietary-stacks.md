---
title: 非 PnP デバイスまたは専用スタックでの WBDI の使用
description: 非 PnP デバイスまたは専用スタックでの WBDI の使用
ms.assetid: 0143eae4-4ca8-4b25-9a97-2cace74f8de9
keywords:
- 生体認証ドライバー WDK、レガシ
- 生体認証ドライバー WDK、非 PnP デバイス
- 生体認証ドライバー WDK、独自の履歴
- レガシ ドライバー スタック WDK 生体認証
- 非 PnP デバイス WDK 生体認証
- 独自のスタック WDK 生体認証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3103760af97d510a505a5119e5bc2b0fc3439ec6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580340"
---
# <a name="using-wbdi-with-non-pnp-devices-or-proprietary-stacks"></a>非 PnP デバイスまたは専用スタックでの WBDI の使用


WBDI は、非 PnP デバイスをサポートしていません。 ただし、生体認証デバイスの非 PnP や WBDI 以外のドライバー スタックを使用するデバイスも連動できる WBDI。

WBDI でレガシ ドライバー スタックを使用する 2 つの主な方法はあります。

1.  新しいセンサーの生体認証リーダー出会いと別れを管理するプラグインを作成します。

2.  既存のデバイス スタックの生体認証機能またはイベントを検出するには、bus フィルターをインストールします。 バスのフィルターは、WBDI ドライバーの PDO を作成します。

WBDI Pdo を管理するフィルターを作成することが 2 つのソリューションの簡単ですし、これは Microsoft によって推奨される方法です。

 

 





