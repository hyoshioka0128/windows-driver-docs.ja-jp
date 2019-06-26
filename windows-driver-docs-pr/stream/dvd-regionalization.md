---
title: DVD のリージョン処理
description: DVD のリージョン処理
ms.assetid: 931441c8-9521-43c9-86f1-dbf75d36e190
keywords:
- DVD デコーダー ミニドライバー WDK
- 加入 WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bf9536cf9620b571f18683090d6c3f48d70fe5a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384148"
---
# <a name="dvd-regionalization"></a>DVD のリージョン処理





DVD デコーダーのミニドライバーを加入プロセスの一部にすることはできません。 ストリーミング アーキテクチャの他の部分では、加入を適用します。 ほとんどの状況では、デコーダー ミニドライバーは実装していません、 [ **KS\_DVDCOPY\_リージョン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_region)プロパティ。

デコーダーが (ハードウェアまたは他の考慮事項) では、特定の地域に制限のかどうかに応答する必要があります、 **KS\_DVDCOPY\_リージョン**に他のすべてのシステム領域をオーバーライドするプロパティ。 DVD デコーダーのミニドライバーは、正確に、デコーダーがで指定されたリージョンに対応する 1 つのビットを設定する必要があります。 ロジックは*反転*メディアには、リージョンのコーディングから。 たとえば、デコーダーでリージョン 1 (米国のみ) を使用するように設計に 0x01 を返します、 **KS\_DVDCOPY\_リージョン**プロパティ。

デコーダーは、領域を提供する場合、システムの地域は、アプリケーションは機能を変更します。 システムの他のデコーダーがある場合は、システムの地域を変更します。 Windows DVD の再生がシステムの地域とデコーダーのリージョンが一致している場合に関数のみことに注意してください。

 

 




