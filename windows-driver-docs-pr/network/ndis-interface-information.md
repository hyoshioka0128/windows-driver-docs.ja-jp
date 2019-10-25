---
title: NDIS インターフェイス情報
description: NDIS インターフェイス情報
ms.assetid: 35187fda-a239-4801-b0be-53fcbee7d24e
keywords:
- 管理情報ベースの WDK ネットワーク
- Mib WDK ネットワーク
- NDIS WDK、インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fce0c042aca1937373c49f0785554f48eb90723b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843545"
---
# <a name="ndis-interface-information"></a>NDIS インターフェイス情報





NDIS 管理情報ベース (Mib) に対してクエリを実行するための標準化されたインターフェイスにより、より簡単にネットワークインターフェイスに関する情報をクエリするために、より簡単にドライバーやユーザーモードアプリケーションを使用できるようになります。 MIB クライアントは、基になる NDIS インターフェイスプロバイダーから情報を要求するために、NDIS によって提供される関数を呼び出します。 これにより、NDIS は OID 要求を発行して情報を取得します。 クライアントに情報を提供するために、NDIS はクライアントが NDIS に登録したコールバック関数を呼び出します。

NDIS ネットワークインターフェイスサービスの詳細については、「 [Ndis ネットワークインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

NDIS では、Management Instrumentation (WMI) のサポートが強化されています。 WMI の NDIS 6.0 サポートの詳細については、「 [wmi の Ndis サポート](ndis-support-for-wmi.md)」を参照してください。

## <a name="related-topics"></a>関連トピック


[**NDIS\_インターフェイス\_情報**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)

 

 






