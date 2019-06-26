---
title: VMQ 情報の取得
description: VMQ 情報の取得
ms.assetid: e851b656-ef59-42e7-b734-17ce9830096a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ea9d407739e4d17a8105bc6eb653caeb579b90b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354500"
---
# <a name="obtaining-vmq-information"></a>VMQ 情報の取得





VMQ インターフェイスには、OID 要求と重なってドライバーとアプリケーションを基になる VMQ 構成に関する情報を取得できるようにする WMI の Guid が含まれています。

[OID\_受信\_フィルター\_ENUM\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)ネットワーク アダプターに割り当てられているキューを列挙します。 キューを列挙する詳細については、次を参照してください。[割り当てられているキューを列挙する](enumerating-the-allocated-queues.md)します。

メソッドの OID 要求としてを使用してドライバーを後続ことができます、 [OID\_受信\_フィルター\_キュー\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters) OID を特定のキューのパラメーターの設定を取得します。 パラメーターのキューの設定を取得する方法の詳細については、次を参照してください。 [VM キュー パラメーターの更新の取得と](obtaining-and-updating-vm-queue-parameters.md)します。

[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)特定のキューに割り当てられているフィルターを列挙します。 キューに設定されているフィルターの列挙の詳細については、次を参照してください。 [、VMQ を列挙するフィルター](enumerating-filters-on-a-vmq.md)します。

メソッドの OID 要求としてを使用してドライバーを後続ことができます、 [OID\_受信\_フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)フィルターのパラメーター設定を取得する OID。 フィルター パラメーターの設定を取得する方法の詳細については、次を参照してください。 [VM キュー パラメーターの更新の取得と](obtaining-and-updating-vm-queue-parameters.md)します。

ドライバーとアプリケーションの関連機能で、VMQ 機能を取得する次の OID クエリ要求を発行できます。

[OID\_受信\_フィルター\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)

[OID\_受信\_フィルター\_現在\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

[OID\_RECEIVE\_FILTER\_GLOBAL\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)

VMQ 機能を取得する方法の詳細については、次を参照してください。[ネットワーク アダプターの VMQ 機能を判断する](determining-the-vmq-capabilities-of-a-network-adapter.md)します。

 

 





