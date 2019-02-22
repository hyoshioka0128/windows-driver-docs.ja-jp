---
title: 仮想関数のパラメーターのクエリを実行します。
description: 仮想関数のパラメーターのクエリを実行します。
ms.assetid: D834762D-9141-4F0F-B76D-5C8ABB016B64
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c2e2ca1b03bd73611583a102902e1455887a8ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560884"
---
# <a name="querying-the-parameters-of-a-virtual-function"></a>仮想関数のパラメーターのクエリを実行します。


上にある、ドライバーまたはユーザー モード アプリケーションを取得できます、現在のパラメーターの PCI Express (PCIe) 仮想機能 (VF) シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターで。 ドライバーまたはアプリケーションのオブジェクト識別子 (OID) メソッド要求を発行[OID\_NIC\_スイッチ\_VF\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451824)これらのパラメーターを取得します。

上にあるドライバーはこの OID メソッド要求を発行前に初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。 ドライバーまたはアプリケーションを設定する必要があります、 **VFId**メンバーのパラメーターが返されるは VF の識別子。 VF 識別子は、次の方法で取得できます。

-   OID メソッド要求を発行して[OID\_NIC\_スイッチ\_ENUM\_VFS](https://msdn.microsoft.com/library/windows/hardware/hh451820)します。

    この OID 要求が正常に完了すると、上にあるドライバーまたはユーザー モード アプリケーションは、ネットワーク アダプターに割り当てられているすべての VFs の一覧を受け取ります。 リスト内の各要素は、 [ **NDIS\_NIC\_スイッチ\_VF\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451591)構造は、指定された、 VFid**VFId**メンバー。

-   OID メソッド要求を発行して[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。

    上にあるドライバーがで新しく作成された VF の識別子を受け取るこの OID 要求が正常に完了している場合、 **VFId** 、返されたメンバー [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。

    **注**  専用ドライバーの関連でこの方法で VF 識別子を取得できます。

     

OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。 この構造体には、指定した VF の構成パラメーターが含まれています。

NDIS ハンドル、 [OID\_NIC\_スイッチ\_VF\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451824)ミニポート ドライバーに要求します。 NDIS は、次のソースを調べることから保持されているデータの内部キャッシュから情報を返します。

-   OID メソッド要求[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。

-   OID の要求を設定する[OID\_NIC\_スイッチ\_VF\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451824)します。

 

 





