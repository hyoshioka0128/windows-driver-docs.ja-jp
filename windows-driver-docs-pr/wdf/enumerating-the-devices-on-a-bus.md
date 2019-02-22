---
title: バス上のデバイスを列挙します。
description: バス上のデバイスを列挙します。
ms.assetid: 5731db82-2bc8-4a8d-98f1-3977845f572c
keywords:
- PnP WDK KMDF、バスの列挙型
- プラグ アンド プレイ WDK KMDF、バスの列挙型
- バスの WDK KMDF 列挙型
- WDK KMDF 列挙型
- WDK KMDF の子デバイス
- WDK KMDF の子デバイスの一覧を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4952b68f29f3b0ce539255941764b63861182c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527498"
---
# <a name="enumerating-the-devices-on-a-bus"></a>バス上のデバイスを列挙します。


*列挙体のバス*はどの子デバイスは、親デバイスに接続を確認する動作。 親デバイスは通常、バス アダプターですが、各関数が、別の一連のドライバーが必要です、サウンド カードなどの複数の関数をサポートするデバイスにもできます。

カーネル モード ドライバー フレームワーク (KMDF) は、バスの列挙体の 2 つの種類をサポートします。

-   [列挙体の静的](static-enumeration.md)は簡単に実装できるとは、番号が最適です。、、および子デバイスの種類のシステムに固有でないと、ハードウェアが接続された後は変更できません。

-   [動的な列挙](dynamic-enumeration.md)数や子デバイスの種類、別に 1 台のコンピューターから変更した場合にこれを使用する必要があります。

バス ドライバーには、バスの列挙体のいずれかまたは両方の型を使用できます。

KMDF バス ドライバーの記述方法の詳細については、次を参照してください。[バス ドライバー開発に基づいて KMDF](https://msdn.microsoft.com/windows/hardware/gg463281)します。

 

 





