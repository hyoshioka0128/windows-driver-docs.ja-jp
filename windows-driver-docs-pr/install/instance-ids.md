---
title: インスタンス ID
description: インスタンス ID は、コンピューター上の同じ種類の他のデバイスとデバイスを区別するためのデバイス識別文字列です。
ms.assetid: 093063a6-1855-4e36-9465-1eedaa3cd0f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d199b92b45c3df39be8d125572a11147cd480d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837477"
---
# <a name="instance-id"></a>インスタンス ID


インスタンス ID は、コンピューター上の同じ種類の他のデバイスとデバイスを区別するためのデバイス識別文字列です。 インスタンス ID には、シリアル番号情報が含まれています (基になるバスでサポートされている場合)。または、何らかの場所情報が含まれています。 文字列に "\\" 文字を含めることはできません。それ以外の場合、文字列の汎用形式はバスに固有です。




NULL ターミネータを除く、インスタンス ID の文字数は、MAX_DEVICE_ID_LEN よりも小さくする必要があります。 さらに、インスタンス ID をデバイス[id](device-ids.md)に連結してデバイスインスタンス id を作成する場合、デバイス id とインスタンス id の長さは、デバイスインスタンス id の可能な最大長によってさらに制限されます。

デバイスの[**DEVICE_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)構造体の**UniqueID**メンバーは、次のように、バスから提供されたインスタンス ID がシステム全体で一意であるかどうかを示します。

-   **UniqueID**が**FALSE**の場合、デバイスのバスによって指定されたインスタンス ID は、デバイスのバスに対してのみ一意です。 プラグアンドプレイ (PnP) マネージャーは、バスから提供されたインスタンス ID を変更し、それを対応するデバイス ID と組み合わせて、システム内で一意のデバイスインスタンス ID を作成します。

-   **UniqueID**が**TRUE**の場合、バスが提供したデバイス id とインスタンス id で構成されるデバイスインスタンス id によって、システム内のデバイスが一意に識別されます。

インスタンス ID は、システムの再起動にわたって保持されます。

バスによって提供されるデバイスのインスタンス ID を取得するには、 [**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)要求を使用し、 **QueryId**メンバーを**busqueryinstanceid**に設定します。

 

 





