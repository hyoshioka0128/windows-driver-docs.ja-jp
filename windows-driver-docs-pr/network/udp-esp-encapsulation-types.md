---
title: UDP ESP カプセル化の種類
description: UDP ESP カプセル化の種類
ms.assetid: 126d2fd5-778e-43ff-87f6-5b0b54a83bac
keywords:
- WDK の IPsec ESP パケットを UDP カプセル化オフロード、カプセル化のタイプし、サブタイプ
- WDK の UDP ESP をカプセル化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1dc8ff441c908c7b1e9a395ace740e5601dfed6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549526"
---
# <a name="udp-esp-encapsulation-types"></a>UDP ESP カプセル化の種類

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




次の図は、インターネット キー交換 (IKE) パケットと受信ポート 4500 ESP で保護されたデータ パケットの UDP カプセル化を示します。

![ポート 4500 の基本的な udp esp カプセル化を示す図](images/4500-encap-types.png)

IKE パケットの UDP ヘッダーに続くゼロの 4 バイトに注意してください。 このフィールドをゼロでは、ポート 4500 で ESP の UDP カプセル化パケットから IKE パケットが区別されます。 0 ではなく ESP ヘッダーは、パケットのこの場所で 0 以外の場合、ESP ヘッダーがあります。

### <a name="udp-esp-encapsulation-subtypes"></a>UDP ESP カプセル化のサブタイプ

ポート 4500 で ESP パケットは、次の UDP ESP カプセル化のサブタイプのいずれかに従って書式設定できます。

-   トランスポートの UDP カプセル化します。

    Udp トランスポート モードの ESP でカプセル化パケットをカプセル化されます。

-   トンネルの UDP カプセル化します。

    パケットのトンネル モードの部分は、UDP カプセル化します。 パケットのトランスポート モードの部分では、UDP カプセル化があり、ESP により保護されたではありません。

-   UDP カプセル化されたトンネル経由で転送します。

    パケットのトンネル モードの部分は、UDP カプセル化します。 パケットのトランスポート モードの部分では、UDP カプセル化ではありませんが、ESP で保護されています。

-   トンネル経由でトランスポートを UDP カプセル化します。

    パケットのトンネル モードの部分は、UDP カプセル化されません。 パケットのトランスポート モードの部分は、UDP カプセル化し、ESP で保護されています。

UDP カプセル化されたトンネルを経由の UDP カプセル化されたトランスポートがサポートされているカプセル化のサブタイプではないことに注意してください。

次の図は、ポート 4500 の UDP ESP カプセル化のサブタイプを示します。

![ポート 4500 の udp esp カプセル化のサブタイプを示す図](images/4500-encap-subtypes.png)

 

 





