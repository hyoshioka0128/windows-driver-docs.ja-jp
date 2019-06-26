---
title: インスタンス ID
description: インスタンス ID は、コンピューターで同じ種類の他のデバイスからデバイスを区別するデバイスの識別文字列です。
ms.assetid: 093063a6-1855-4e36-9465-1eedaa3cd0f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 353527552205fa383d1b13a35975acad465416a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370928"
---
# <a name="instance-id"></a>インスタンス ID


インスタンス ID は、コンピューターで同じ種類の他のデバイスからデバイスを区別するデバイスの識別文字列です。 インスタンス ID には、基になるバス、またはある種の位置情報でサポートされている場合、シリアル番号の情報が含まれます。 文字列は、いずれかを含めることはできません"\\"文字です。 それ以外の場合、文字列の一般的な形式は、バスに固有です。




NULL ターミネータを除く、インスタンス ID の文字数は、MAX_DEVICE_ID_LEN 未満である必要があります。 インスタンス ID が連結された場合にさらに、[デバイス ID](device-ids.md)デバイス ID とインスタンス ID の長さをさらに、デバイス インスタンス ID の可能な最大長で制約デバイス インスタンス ID を作成するには

**UniqueID**のメンバー、 [ **DEVICE_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)デバイスかどうかをバスが指定したインスタンス ID を一意なシステム全体で次のようの構造体します。

-   場合**UniqueID**は**FALSE**デバイスのバスが提供するインスタンス ID は、デバイスのバスにのみ一意です。 プラグ アンド プレイ (PnP) マネージャーは、バスが提供するインスタンス ID を変更し、対応するデバイスの ID をシステム内で一意であるデバイス インスタンス ID を作成すると、それを結合します。

-   場合**UniqueID**は**TRUE**、デバイス インスタンス ID、バスが指定したデバイス ID とインスタンスの ID を使って生成されますが、システム内のデバイスを一意に識別します。

インスタンス ID は、システムの再起動の間で永続的です。

デバイスのバスが提供するインスタンス ID を取得するには、使用、 [ **IRP_MN_QUERY_ID** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)を要求し、設定、 **Parameters.QueryId.IdType**メンバー **BusQueryInstanceID**します。

 

 





