---
title: VMQ フィルターをクリア
description: VMQ フィルターをクリア
ms.assetid: 34efeb28-dcd6-4a8b-89d2-6065830e03ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c2174e0490c1f94040acbc3289141c6ed67b978
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549907"
---
# <a name="clearing-a-vmq-filter"></a>VMQ フィルターをクリア





上にある、ドライバーの問題を受信キューにフィルターを解放する、 [OID\_受信\_フィルター\_クリア\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569785) OID 要求のセット。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_クリア\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567166)構造体。

プロトコル ドライバーでは、フィルターの識別子を取得、以前から[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)メソッド要求の OID。 フィルターの設定の詳細については、次を参照してください。 [VMQ フィルター設定](setting-a-vmq-filter.md)します。

プロトコル ドライバーには、設定されると、キューを解放する前に、キューのすべてのフィルターをクリアする必要があります。 プロトコル ドライバーも設定されると、ネットワーク アダプターには、そのバインドが閉じる前に、既定のキューのすべてのフィルターをオフにする必要があります。

OID が完了しなかった場合、ミニポート ドライバーは既定以外のキューでパケットを示していませんする必要があります\_受信\_フィルター\_オフ\_フィルター OID 要求キューの最後のフィルターをクリアまたは、が完了したかどうか[OID\_受信\_フィルター\_FREE\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569789) OID 要求キューを解放します。

 

 





