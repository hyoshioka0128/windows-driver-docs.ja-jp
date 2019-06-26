---
title: NDIS ポートの状態
description: NDIS ポートの状態
ms.assetid: bb13edd2-815b-488a-b36c-21a48809a143
keywords:
- WDK NDIS、状態のポート
- NDIS ポート WDK、状態
- WDK NDIS ポートの状態
- 認証は、WDK NDIS ポートを状態します。
- リンク状態 WDK NDIS ポート
- 初期化状態 WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 831188b8fba144458b373d54b2411f76ac2df4f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354957"
---
# <a name="ndis-port-states"></a>NDIS ポートの状態





NDIS ポートがある動作の初期化状態で指定されている状態は、状態、 [ **NDIS\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)構造体。 ポートの状態は、次のカテゴリに合わせます。

<a href="" id="initialization-states"></a>初期化状態  
NDIS ポートの状態は、スタートアップの初期化に関連付けられているし、プラグ アンド プレイ (PnP) イベントに初期化します。 NDIS またはミニポート ドライバーは、最初にポートを割り当てますとき、に、ポートが、*割り当てられている状態*します。 NDIS またはミニポート ドライバーにポートがアクティブ化した後にポートが、*状態をアクティブ化される*します。 非アクティブなポートことはできません送受信したりデータ、状態インジケーターを作成、OID の要求を受信したり PnP イベントを開始します。

<a href="" id="link-states"></a>リンクの状態  
NDIS ポート リンクの状態はミニポート アダプターに関連付けられているしで指定された状態のリンクに似ています、 [ **NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体。 ポートのリンクの状態は、メディア リンクの接続状態とのリンク速度を示します。 ポートのリンクの状態は、関連付けられているミニポート アダプターのリンクの状態を異なっていてもかまいません。

<a href="" id="authentication-states"></a>認証の状態  
NDIS ポート認証の状態、ポートが制御されるかどうかを示します (承認が必要)、データ転送の方向 (send、receive、またはその両方)、およびポート (承認または許可されていません) の承認の状態。 ポートが制御されていない場合は、認証と、未認証の状態は無視されます。

ミニポート ドライバーでは、ポートをアクティブ化したり、PnP イベントでのポートを非アクティブ化することができます。 アクティブ化して、ポートを非アクティブ化の詳細については、次を参照してください。[ライセンス NDIS ポート](activating-an-ndis-port.md)と[Deactivating NDIS ポート](deactivating-an-ndis-port.md)します。

ドライバーの使用が重なって、 [OID\_GEN\_ポート\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)で指定されているポートの現在の状態を取得する OID、 **PortNumber** のメンバー[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 NDIS が、この OID を処理し、ミニポート ドライバーには、この OID クエリは受け取りません。

NDIS ポートをサポートするミニポート ドライバーを使用する必要があります、 [ **NDIS\_状態\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state) NDIS ポートの状態の変化を示すステータスを示す値。 ミニポート ドライバー ポート番号を設定する必要があります、 **PortNumber**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体。

NDIS および上にあるドライバーを使用して、 [OID\_GEN\_ポート\_認証\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters) NDIS ポートの現在の認証状態を設定する OID。 NDIS ポートをサポートするミニポート ドライバーでは、この OID をサポートする必要があります。

 

 





