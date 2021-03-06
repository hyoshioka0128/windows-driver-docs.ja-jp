---
title: デバイスの親の判断
description: デバイスの親の判断
ms.assetid: 61458911-222f-46aa-bc0e-a61ee25337bb
keywords:
- SetupAPI 関数 WDK、保護者の方を決定します。
- WDK SetupAPI を決定する親デバイス
- デバイスの親 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c255879083ca9d700c37a58da149646799823ff5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374244"
---
# <a name="determining-the-parent-of-a-device"></a>デバイスの親の判断





デバイスの親にアクセスするために必要な場合があります。 たとえば、一部の種類のハードウェア デバイスの操作は、特定の親と子デバイスのセットの間で固定的な関係に依存します。 このようなハードウェア デバイスをアンインストールするには、すべての子デバイスだけでなく、親をアンインストールしてください。 取得する必要があります、親をアンインストールする、 [ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)親構造体。 ユニバーサル シリアル バス (USB) 複合デバイスでは、多機能プリンターでは、このようなデバイスは、次のようにします。 親複合デバイスと 1 つまたは複数の子インターフェイス デバイスによって、システムで表されます (を参照してください[USB ドライバー スタック アーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index))。 多機能プリンターをアンインストールするには、すべての子インターフェイス デバイスだけでなく、親複合デバイスをアンインストールする必要があります。

ときに、プラグ アンド プレイ)、デバイス、デバイス ツリーにします。 使用するデバイスの親を確認する方法は、方法、デバイスは現在構成されているシステムでは、次のように依存します。

-   デバイスでは、デバイス ツリーに devnode が含まれる場合は、使用[ **CM_Get_Parent** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)親のデバイスのインスタンス ハンドルを取得します。 取得できますのデバイスのインスタンス ハンドルを指定する、[デバイス インスタンス ID](device-instance-ids.md)と[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)デバイスの構造体。 詳細については、次を参照してください。[デバイス ツリー内のデバイスの親を取得する](obtaining-the-parent-of-a-device-in-the-device-tree.md)します。

-   デバイスに、親の固定的な関係がある場合は、保存し、親のデバイス インスタンス ID を取得できます。 デバイスの存在になると、デバイスの SP_DEVINFO_DATA 構造体を取得するのにデバイスのインスタンス ハンドルを使用できます。 詳細については、次を参照してください。 [Nonpresent デバイスの親を判断する](determining-the-parent-of-a-nonpresent-device.md)します。

 

 





