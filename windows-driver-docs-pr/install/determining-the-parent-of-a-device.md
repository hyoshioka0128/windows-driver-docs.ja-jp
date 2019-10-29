---
title: デバイスの親の判断
description: デバイスの親の判断
ms.assetid: 61458911-222f-46aa-bc0e-a61ee25337bb
keywords:
- Setupapi.log 関数 WDK、親の決定
- WDK Setupapi.log を決定する親デバイス
- デバイスの親 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60028c3aa9baa324e4e1d6cc6f770ee61c454b77
ms.sourcegitcommit: fe0b8b8b162c6fc0afd82dd03e83d41be0bc5d12
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72980749"
---
# <a name="determining-the-parent-of-a-device"></a>デバイスの親の判断





デバイスの親にアクセスすることが必要になる場合があります。 たとえば、一部の種類のハードウェアデバイスの操作は、特定の親デバイスと子デバイスのセットの間の固定関係に依存します。 このようなハードウェアデバイスをアンインストールするには、すべての子デバイスに加えて、親をアンインストールする必要があります。 親をアンインストールするには、親の[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)構造体を取得する必要があります。 多機能プリンターなどのユニバーサルシリアルバス (USB) 複合デバイスは、このようなデバイスです。 システムでは、親複合デバイスと1つ以上の子インターフェイスデバイス (「 [USB ドライバースタックアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照) によって表されます。 多機能プリンターをアンインストールするには、すべての子インターフェイスデバイスに加えて、その親複合デバイスもアンインストールする必要があります。

プラグアンドプレイ (PnP) マネージャーは、システム内のデバイスを構成するときに、デバイスのデバイスノード (*devnode*) をデバイス[ツリー](../kernel/device-tree.md)に追加します。 PnP マネージャは、システムからデバイスを削除すると、デバイスツリーからデバイスの devnode を削除し、デバイスは存在しない*デバイス*になります。  デバイスの親を決定するために使用する方法は、次のように、デバイスがシステムでどのように構成されているかによって異なります。

-   デバイスのデバイスツリーに devnode がある場合は、 [**CM_Get_Parent**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)を使用して、その親のデバイスインスタンスハンドルを取得します。 デバイスインスタンスハンドルを指定すると、デバイスのデバイス[インスタンス ID](device-instance-ids.md)と[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)構造体を取得できます。 詳細については、「[デバイスツリーでデバイスの親を取得する](obtaining-the-parent-of-a-device-in-the-device-tree.md)」を参照してください。

-   デバイスに親との固定関係がある場合は、その親のデバイスインスタンス ID を保存および取得できます。 デバイスが存在しない状態になった場合は、そのデバイスのインスタンスハンドルを使用して、デバイスの SP_DEVINFO_DATA 構造体を取得できます。 詳細については、「存在しない[デバイスの親の特定](determining-the-parent-of-a-nonpresent-device.md)」を参照してください。

 

 





