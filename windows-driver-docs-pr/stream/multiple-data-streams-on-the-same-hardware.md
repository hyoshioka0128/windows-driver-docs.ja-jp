---
title: 同じハードウェア上の複数のデータ ストリーム
description: 同じハードウェア上の複数のデータ ストリーム
ms.assetid: 23133022-6d00-44ad-8c0d-24715204cacc
keywords:
- 複数のデータストリーム WDK DVD デコーダー
- サポートされている、ストリーミング番号、WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d86d3b0375e83339d6f8d352c37c2e7427deb506
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842130"
---
# <a name="multiple-data-streams-on-the-same-hardware"></a>同じハードウェア上の複数のデータ ストリーム





多くのデコーダーには、同じデコーダーハードウェアを使用する複数のストリームがあります。 これらのデバイスでは、ストリームごとにキーネゴシエーションを個別に実行する必要はありません。 これを DVD デコーダーモデルに示すには、 [**KS\_DVDCOPY\_SET\_\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)プロパティを使用します。 このプロパティで get 操作が発行されると、デコーダーは次のいずれかの方法で応答する可能性があります。

KS\_DVDCOPYSTATE\_認証\_必要\_ない

KS\_DVDCOPYSTATE\_認証\_必要

KS\_DVDCOPYSTATE\_AUTHENTICATION\_は必要\_ありません。これは、同じハードウェア上の別のストリームで既に実行されているため、指定したストリームにキーネゴシエーションが必要ないことを示します。 たとえば、デコーダーが最初にオーディオストリームで**Get**プロパティを受信した場合、オーディオストリームと KS\_DVDCOPYSTATE で必要とされる**ks\_DVDCOPYSTATE\_認証\_** に応答し **\_認証\_** 、他のすべてのストリームで\_必要はありません。 認証を使用して応答した後\_\_は必要ありません。そのストリームは、次のタイトルキーがネゴシエートされるまで、他のキー交換プロパティを受け取りません。 その時点で、デコーダーは認証を使用して応答するように選択できますが、\_\_必要はありません。

デコーダーが1つのストリームに対して著作権保護を実行する必要がある場合は、1つ目のストリームでネゴシエーションを実行して、 **KS\_DVDCOPY の Get プロパティ呼び出しを受信します。** ストリームを開いた後\_\_の状態をコピー\_設定します。 1つのストリームでのみ機能するように著作権保護のプロパティをハードコーディングしないでください。

 

 




