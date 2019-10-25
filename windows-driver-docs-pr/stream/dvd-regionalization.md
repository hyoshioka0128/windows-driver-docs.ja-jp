---
title: DVD のリージョン処理
description: DVD のリージョン処理
ms.assetid: 931441c8-9521-43c9-86f1-dbf75d36e190
keywords:
- DVD デコーダーミニドライバー WDK
- regionalization WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f6b456e2f27c01ef9a62bf9b6c93a712106104a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843213"
---
# <a name="dvd-regionalization"></a>DVD のリージョン処理





DVD デコーダーミニドライバーは、regionalization プロセスのどの部分にも参加しないようにしてください。 ストリーミングアーキテクチャのその他の部分では、regionalization が適用されます。 ほとんどの状況で、デコーダーミニドライバーは[**KS\_DVDCOPY\_REGION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_region)プロパティを実装していません。

デコーダーが特定の地域に限定されている場合 (ハードウェアやその他の考慮事項によって)、 **KS\_DVDCOPY\_region**プロパティに応答して、他のすべてのシステム領域を上書きすることがあります。 DVD デコーダーミニドライバーは、デコーダーが指定されているリージョンに対応する1ビットだけを設定する必要があります。 ロジックは、メディア上の領域のコーディングから*逆*になっていることに注意してください。 たとえば、地域 1 (USA) でのみ機能するように設計されたデコーダーは、 **KS\_DVDCOPY\_Region**プロパティに0x01 を返します。

デコーダーがリージョンを提供する場合、システム領域の変更アプリケーションは引き続き機能します。 システム内に他のデコーダーがある場合に備えて、システム領域を変更します。 Windows DVD 再生は、システム領域とデコーダー領域が一致する場合にのみ機能することに注意してください。

 

 




