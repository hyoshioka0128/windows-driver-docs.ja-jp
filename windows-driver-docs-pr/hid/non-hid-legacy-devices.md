---
title: 非 HID のレガシ デバイス
description: このセクションでは、非 HID のキーボードとマウスに対応したドライバー、トランスポート、およびフィルター ドライバーについて説明します。 これらのデバイスは主に PS/2 トランスポートで実行されます。
ms.assetid: 4726DD47-C22E-4B92-A7BD-EB37BA53496F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b8733769a44e5fbda86c942c86cf5931bc6561e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346215"
---
# <a name="non-hid-legacy-devices"></a>非 HID のレガシ デバイス


このセクションでは、非 HID のキーボードとマウスに対応したドライバー、トランスポート、およびフィルター ドライバーについて説明します。 これらのデバイスは主に PS/2 トランスポートで実行されます。

このセクションでは、Sermouse、シリアル マウス用の Windows システム関数ドライバーに関する情報は含まれません。 Sermouse I8042prt に適用される運用上の制約は適用されないことに注意してください。 さらに、上位レベルのフィルター ドライバーは併用できません Sermouse シリアル マウスの操作をカスタマイズします。 代わりに、ベンダーは、デバイスのデバイス固有の関数のドライバーをインストールする必要があります。 デバイス固有の関数のドライバーと Sermouse は互いに独立して同時に操作できます。

## <a name="non-hid-driver-stack"></a>非 HID ドライバー スタック


Windows 8 では、非 HID キーボード、マウス、およびタッチパッドのハードウェアを次のドライバー スタックを使用します。 のみ非-HID トランスポート Windows 8 でサポートされていますが PS2 します。

![非 hid ドライバー スタック](images/non-hid-driver-stack.png)

 

 




