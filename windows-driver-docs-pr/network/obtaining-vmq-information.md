---
title: VMQ の情報を取得します。
description: VMQ の情報を取得します。
ms.assetid: e851b656-ef59-42e7-b734-17ce9830096a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a23719346a95b8825ae66037e11a56c130054235
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557234"
---
# <a name="obtaining-vmq-information"></a>VMQ の情報を取得します。





VMQ インターフェイスには、OID 要求と重なってドライバーとアプリケーションを基になる VMQ 構成に関する情報を取得できるようにする WMI の Guid が含まれています。

[OID\_受信\_フィルター\_ENUM\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569788)ネットワーク アダプターに割り当てられているキューを列挙します。 キューを列挙する詳細については、次を参照してください。[割り当てられているキューを列挙する](enumerating-the-allocated-queues.md)します。

メソッドの OID 要求としてを使用してドライバーを後続ことができます、 [OID\_受信\_フィルター\_キュー\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569794) OID を特定のキューのパラメーターの設定を取得します。 パラメーターのキューの設定を取得する方法の詳細については、次を参照してください。 [VM キュー パラメーターの更新の取得と](obtaining-and-updating-vm-queue-parameters.md)します。

[OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)特定のキューに割り当てられているフィルターを列挙します。 キューに設定されているフィルターの列挙の詳細については、次を参照してください。 [、VMQ を列挙するフィルター](enumerating-filters-on-a-vmq.md)します。

メソッドの OID 要求としてを使用してドライバーを後続ことができます、 [OID\_受信\_フィルター\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569792)フィルターのパラメーター設定を取得する OID。 フィルター パラメーターの設定を取得する方法の詳細については、次を参照してください。 [VM キュー パラメーターの更新の取得と](obtaining-and-updating-vm-queue-parameters.md)します。

ドライバーとアプリケーションの関連機能で、VMQ 機能を取得する次の OID クエリ要求を発行できます。

[OID\_受信\_フィルター\_ハードウェア\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569791)

[OID\_受信\_フィルター\_現在\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569786)

[OID\_RECEIVE\_FILTER\_GLOBAL\_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff569790)

VMQ 機能を取得する方法の詳細については、次を参照してください。[ネットワーク アダプターの VMQ 機能を判断する](determining-the-vmq-capabilities-of-a-network-adapter.md)します。

 

 





