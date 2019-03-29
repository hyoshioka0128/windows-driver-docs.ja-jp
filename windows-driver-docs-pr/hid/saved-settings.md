---
title: 保存された設定
description: 保存された設定
ms.assetid: fa3eb2c9-b0ae-4872-b0f4-13fdd3745265
keywords:
- WDK ジョイスティックのレジストリ設定を保存
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 60b861a24a6d2cc5674b5f5362f35c876bfd3901
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570333"
---
# <a name="saved-settings"></a>保存された設定





保存すると、現在のジョイスティック設定は、REGSTR\_VAL\_JOYNCONFIG に保存されている、REGSTR\_キー\_JOYCURR キーが、REGSTR で書かれても\_キー\_JOYSETTINGS キーOEM が定義した設定の取得元となるものと同じ名前のサブキー (型の数を足す非 OEM 設定が"predef"のサブキーに保存されます)。 ジョイスティックが置き換えられると、保存された設定のままになり、現在の設定に保存された設定が再度検疫ジョイスティックが復元された場合。 これらのレジストリ値は、コントロール パネルでのみ使用されます。

 

 




