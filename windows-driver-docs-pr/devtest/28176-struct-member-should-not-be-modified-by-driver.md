---
title: C28176
description: 警告 C28176 が構造体のメンバーは、ドライバーによっては変更しないでください。
ms.assetid: 837b2dcd-0682-460f-a3ae-ebd82bcc451b
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28176
ms.openlocfilehash: bbf48ababf2ce0be16ea35978aa91b76de5dc1d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371478"
---
# <a name="c28176"></a>C28176


C28176 を警告します。構造体のメンバーは、ドライバーによっては変更しないでください。

この警告は、ドライバーがドライバーを決して変更ドキュメントに未記載の構造体メンバーを変更することを示します。

ドライバーは、指定されたドキュメントに未記載の構造体のメンバーには記述しないでください。 非透過または部分的に非透過構造体のメンバーの最も文書化されていない場合は、この禁止は絶対です。 ただし、ドライバーは、特定するルーチン内から特定のドキュメントに未記載の構造体メンバーを記述することがあります。 たとえば、 [**デバイス\_オブジェクト。NextDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)メンバーは、ドライバー内でのみ記述できます\_ドライバーの初期化または\_アンロード ルーチン。

 

 





