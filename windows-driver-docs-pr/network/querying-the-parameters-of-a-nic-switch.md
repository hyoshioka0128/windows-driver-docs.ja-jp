---
title: NIC スイッチのパラメーターのクエリ
description: NIC スイッチのパラメーターのクエリ
ms.assetid: 8C1F0F8A-D290-4552-A324-062DB92F6B5D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c855acc3df5f563500d76f68783b79720c2b713
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340004"
---
# <a name="querying-the-parameters-of-a-nic-switch"></a>NIC スイッチのパラメーターのクエリ


上にあるドライバーやユーザー アプリケーションでは、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターで作成された NIC スイッチ パラメーターを取得できます。 ドライバーまたはアプリケーションのオブジェクト識別子 (OID) メソッド要求を発行[OID\_NIC\_スイッチ\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451823)これらのパラメーターを取得します。

上にあるドライバーまたはユーザーのアプリケーションでは、この OID メソッド要求を発行、前に初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体。 ドライバーまたはアプリケーションを設定する必要があります、 **SwitchId**メンバーのパラメーターが返されるには、NIC のスイッチの識別子。

**注**  以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、 *NIC スイッチの既定*、NDIS によって参照されている\_既定\_スイッチ\_ID です。

 

この OID メソッド要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体。 この構造体には、指定されたスイッチのパラメーターが含まれています。

NDIS ハンドル、 [OID\_NIC\_スイッチ\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451823)ミニポート ドライバーに要求します。 NDIS は、次のソースから保持されているデータの内部キャッシュから情報を返します。

-   レジストリの標準化された設定の SR-IOV キーワード。 これらのキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

-   OID 要求[OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)と[OID\_NIC\_スイッチ\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451823).

 

 





