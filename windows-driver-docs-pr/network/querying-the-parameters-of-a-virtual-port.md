---
title: 仮想ポートのパラメーターのクエリを実行します。
description: 仮想ポートのパラメーターのクエリを実行します。
ms.assetid: 482DA041-2C70-438A-8D29-0F338CDCF935
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afb90e36f69cd108e752d3f30e2ff2a75dc0a54e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539481"
---
# <a name="querying-the-parameters-of-a-virtual-port"></a>仮想ポートのパラメーターのクエリを実行します。


上にある、ドライバーは、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの NIC スイッチの仮想ポート (VPort) のパラメーターを取得できます。 ドライバーの問題のオブジェクト識別子 (OID) メソッド要求[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825)これらのパラメーターを取得します。

上にあるドライバーはこの OID メソッド要求を発行前に初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。 ドライバーは、次のようにこの構造体のメンバーを設定する必要があります。

-   **SwitchId**メンバーは、パラメーターが返されるには、NIC のスイッチの識別子を設定する必要があります。

    **注**  以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、*既定 NIC スイッチ*します。 **SwitchId** NDIS にメンバーを設定する必要があります\_既定\_スイッチ\_id。

     

-   **VPortId** VPort に関連付けられている識別子にメンバーを設定する必要があります。 上にあるドライバーは、次の方法のいずれかで VPort 識別子を取得します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_ENUM\_拡張](https://msdn.microsoft.com/library/windows/hardware/hh451821)します。

この OID メソッド要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。 この構造体には、指定した VPort のパラメーターが含まれています。

NDIS ハンドル、 [OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825)ミニポート ドライバーに要求します。 NDIS は、次のソースを調べることから保持されているデータの内部キャッシュから情報を返します。

-   OID メソッド要求[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。

-   OID の要求を設定する[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825)します。

 

 





