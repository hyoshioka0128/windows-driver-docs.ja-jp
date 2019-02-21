---
title: HYPER-V 拡張可能スイッチの構成のクエリを実行します。
description: HYPER-V 拡張可能スイッチの構成のクエリを実行します。
ms.assetid: AF646860-01AB-4F4B-84F8-B570054B10FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2116ba6b1927e9a17aaeaffb7926618ae1781b4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553055"
---
# <a name="querying-the-hyper-v-extensible-switch-configuration"></a>HYPER-V 拡張可能スイッチの構成のクエリを実行します。


HYPER-V 拡張可能スイッチのインターフェイスには、拡張可能スイッチ、ポート、およびそのネットワーク アダプターの接続の現在の構成を照会する拡張可能スイッチ拡張機能によって発行されるオブジェクト識別子 (OID) 要求が含まれています。 これらの要求には、次の Oid が含まれます。

<a href="" id="oid-switch-nic-array"></a>[OID\_スイッチ\_NIC\_配列](https://msdn.microsoft.com/library/windows/hardware/hh598261)  
この OID クエリ要求では、配列を返します。 配列内の各要素には、拡張可能スイッチ ポートに関連付けられているネットワーク アダプターの構成パラメーターを指定します。

<a href="" id="oid-switch-parameters"></a>[OID\_スイッチ\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh598270)  
この OID クエリ要求は、拡張可能スイッチの現在の構成を返します。

<a href="" id="oid-switch-port-array"></a>[OID\_スイッチ\_ポート\_配列](https://msdn.microsoft.com/library/windows/hardware/hh598271)  
この OID クエリ要求では、配列を返します。 配列内の各要素には、拡張可能スイッチ ポートの構成パラメーターを指定します。

<a href="" id="oid-switch-port-property-enum"></a>[OID\_スイッチ\_ポート\_プロパティ\_列挙型](https://msdn.microsoft.com/library/windows/hardware/hh598277)  
この OID メソッド要求は、配列を返します。 配列内の各要素には、指定した拡張可能スイッチ ポートのポリシーのプロパティを指定します。

<a href="" id="oid-switch-property-enum"></a>[OID\_スイッチ\_プロパティ\_列挙型](https://msdn.microsoft.com/library/windows/hardware/hh598282)  
この OID メソッド要求は、配列を返します。 配列内の各要素には、拡張可能スイッチのポリシーのプロパティを指定します。

**注**  最初に発行する必要がありますが、スイッチ拡張機能は、の hyper-v 拡張可能スイッチのバインド、ときに、 [OID\_切り替える\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh598270)スイッチの基本的な情報を取得する OID。 場合、 **IsActive**のメンバー、 [ **NDIS\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598220)構造が FALSE で、拡張機能は、その他のクエリの Oid を発行する必要がありますまで、スイッチには、アクティブ化が完了しました。 ここで、 **NetEventSwitchActivate** [ **NET\_PNP\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff568751)通知スイッチのアクティブ化イベントを指定します。 場合、 **IsActive**メンバーは、TRUE をバインドで、拡張機能は安全に他のクエリの Oid を発行します。 Hyper-v 拡張可能なスイッチが完了していないアクティブ化中に、構成のクエリを実行すると、スイッチの構成の不完全な初期ビューを持つ拡張機能が発生します。

 

**注**  拡張機能は、独自の OID 要求を生成するときでは、この同じと同様の NDIS フィルター ドライバー。 これを行う方法の詳細については、次を参照してください。 [NDIS フィルター ドライバーから OID の要求を生成する](generating-oid-requests-from-an-ndis-filter-driver.md)します。

 

拡張可能スイッチ OID 要求の管理パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ コントロール パスの OID 要求](hyper-v-extensible-switch-control-path-for-oid-requests.md)します。

 

 





