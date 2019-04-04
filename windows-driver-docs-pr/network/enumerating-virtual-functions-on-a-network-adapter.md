---
title: ネットワーク アダプターに仮想関数を列挙します。
description: ネットワーク アダプターに仮想関数を列挙します。
ms.assetid: 3AAF2D8B-9C7A-4E5B-86B6-264ACA5EA492
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e173ef1dbbe084bc3960e64761ed4831e95bc2ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556541"
---
# <a name="enumerating-virtual-functions-on-a-network-adapter"></a>ネットワーク アダプターに仮想関数を列挙します。


上にあるドライバーやユーザー アプリケーションは、すべて PCI Express (PCIe) 仮想機能 (Vf) でシングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの一覧を取得できます。 ドライバーまたはアプリケーションのオブジェクト識別子 (OID) メソッド要求を発行[OID\_NIC\_スイッチ\_ENUM\_VFS](https://msdn.microsoft.com/library/windows/hardware/hh451820)この一覧を取得します。

ドライバーまたはアプリケーションは、OID 要求を発行して、前に初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_VF\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451592)要求と共に渡される構造体。 ドライバーまたはアプリケーションは、初期化するときに、次のガイドラインに従う必要があります、 **NDIS\_NIC\_スイッチ\_VF\_情報\_配列**構造体。

-   場合は、NDIS\_NIC\_スイッチ\_VF\_情報\_配列\_ENUM\_ON\_特定\_スイッチ フラグに設定されて、**フラグ**メンバー、上にあるドライバーまたはアプリケーションを設定する必要があります、 **SwitchId** SR-IOV ネットワーク アダプターで NIC スイッチの識別子にメンバー。 この方法でこれらのメンバーを設定して指定された NIC スイッチ、SR-IOV ネットワーク アダプターに対してのみ、VF の情報が返されます。

    **注**上にあるドライバーとユーザー モード アプリケーションの OID クエリ要求を発行して NIC スイッチの識別子を取得できます[OID\_NIC\_切り替える\_ENUM\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451819).

-   場合、**フラグ**メンバーが 0 に設定されている、ドライバーまたはアプリケーションを設定する必要があります、 **SwitchId**メンバーをゼロにします。 この方法でこれらのメンバーを設定して VF 情報は、SR-IOV ネットワーク アダプター上のすべての NIC スイッチに返されます。

    **注**以降 Windows Server 2012 では、Windows サポート NIC スイッチの既定値のみ、ネットワーク アダプター。 設定されているフラグに関係なく、**フラグ**、メンバー、 **SwitchId** NDIS にメンバーを設定する必要があります\_既定\_スイッチ\_id。

この OID クエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体以下を含むバッファーへのポインターが含まれます。

-   [ **NDIS\_NIC\_スイッチ\_VF\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451592)配列内の要素の数を定義する構造体。

-   配列の[ **NDIS\_NIC\_スイッチ\_VF\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451591)構造体。 各構造体には、NIC のスイッチのネットワーク アダプターの 1 つの VF に関する情報が含まれています。 VF がアタッチされている NIC の OID メソッド要求をスイッチに[OID\_NIC\_スイッチ\_割り当て\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。

    **注**VFs が添付されていない場合、ネットワーク アダプター上の NIC スイッチに、 **NumElements**のメンバー、 [ **NDIS\_NIC\_切り替える\_VF\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451592)構造を設定に 0 と no [ **NDIS\_NIC\_スイッチ\_VF\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451591)構造体が返されます。

    NIC のスイッチの詳細については、[NIC スイッチ](nic-switches.md)を参照してください。

NDIS ハンドル、 [OID\_NIC\_スイッチ\_ENUM\_VFS](https://msdn.microsoft.com/library/windows/hardware/hh451820)ミニポート ドライバーに要求します。 NDIS は、次のソースを調べることから保持されているデータの内部キャッシュから情報を返します。

-   OID メソッド要求[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。

-   OID の要求を設定する[OID\_NIC\_スイッチ\_VF\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451824)します。