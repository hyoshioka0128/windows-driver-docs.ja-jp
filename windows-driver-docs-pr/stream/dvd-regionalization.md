---
title: DVD のリージョン処理
description: DVD のリージョン処理
ms.assetid: 931441c8-9521-43c9-86f1-dbf75d36e190
keywords:
- DVD デコーダー ミニドライバー WDK
- 加入 WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ce15b20792b82520e0570d2e0ff373d7e307acc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363574"
---
# <a name="dvd-regionalization"></a>DVD のリージョン処理





DVD デコーダーのミニドライバーを加入プロセスの一部にすることはできません。 ストリーミング アーキテクチャの他の部分では、加入を適用します。 ほとんどの状況では、デコーダー ミニドライバーは実装していません、 [ **KS\_DVDCOPY\_リージョン**](https://msdn.microsoft.com/library/windows/hardware/ff567638)プロパティ。

デコーダーが (ハードウェアまたは他の考慮事項) では、特定の地域に制限のかどうかに応答する必要があります、 **KS\_DVDCOPY\_リージョン**に他のすべてのシステム領域をオーバーライドするプロパティ。 DVD デコーダーのミニドライバーは、正確に、デコーダーがで指定されたリージョンに対応する 1 つのビットを設定する必要があります。 ロジックは*反転*メディアには、リージョンのコーディングから。 たとえば、デコーダーでリージョン 1 (米国のみ) を使用するように設計に 0x01 を返します、 **KS\_DVDCOPY\_リージョン**プロパティ。

デコーダーは、領域を提供する場合、システムの地域は、アプリケーションは機能を変更します。 システムの他のデコーダーがある場合は、システムの地域を変更します。 Windows DVD の再生がシステムの地域とデコーダーのリージョンが一致している場合に関数のみことに注意してください。

 

 




