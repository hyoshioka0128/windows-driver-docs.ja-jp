---
title: NDIS ポートの状態
description: NDIS ポートの状態
ms.assetid: bb13edd2-815b-488a-b36c-21a48809a143
keywords:
- ポート WDK NDIS、状態
- NDIS ポート WDK、状態
- WDK NDIS ポートの状態
- '認証の状態: WDK NDIS ポート'
- リンクの状態 WDK NDIS ポート
- '初期化の状態: WDK NDIS ポート'
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ca4a1df62f3f4b65a29dae0aa35972f353db86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826916"
---
# <a name="ndis-port-states"></a>NDIS ポートの状態





NDIS ポートには、 [**ndis\_PORT\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)構造体で指定された初期化状態と状態を含む動作状態があります。 ポートの状態は次のカテゴリに分類されます。

<a href="" id="initialization-states"></a>初期化状態  
NDIS ポートの初期化状態は、スタートアップ初期化およびプラグアンドプレイ (PnP) イベントに関連付けられています。 NDIS またはミニポートドライバーによって最初にポートが割り当てられると、ポートは*割り当て済みの状態*になります。 NDIS の後、またはミニポートドライバーによってポートがアクティブ化されると、ポートは*アクティブ化*された状態になります。 非アクティブなポートは、データの送受信、状態の表示、OID 要求の受信、または PnP イベントの開始を行うことはできません。

<a href="" id="link-states"></a>リンクの状態  
NDIS ポートリンクの状態は、ミニポートアダプターに関連付けられているリンクの状態に似ています。リンクの状態は、 [**ndis\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造体で指定されています。 ポートリンクの状態は、メディアリンクの接続状態とリンク速度を示します。 ポートのリンクの状態は、関連付けられているミニポートアダプターのリンクの状態とは異なる場合があります。

<a href="" id="authentication-states"></a>認証の状態  
[NDIS ポートの認証状態] は、ポートが制御されている (承認が必要) かどうか、データ転送の方向 (送信、受信、またはその両方)、およびポートの承認状態 (承認済み、または承認されていない) を示します。 ポートが制御されていない場合、認証された状態と認証されていない状態は無視されます。

ミニポートドライバーは、ポートをアクティブ化するか、PnP イベントを使用してポートを非アクティブ化することができます。 ポートのアクティブ化と非アクティブ化の詳細については、「 [Ndis ポートのアクティブ化](activating-an-ndis-port.md)」および「 [Ndis ポートの非](deactivating-an-ndis-port.md)アクティブ化」をご覧ください。

それまでのドライバーでは、 [oid\_GEN\_port\_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state) oid を使用して、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造**のポート番号メンバーに**指定されているポートの現在の状態を取得します。 NDIS はこの OID を処理し、ミニポートドライバーはこの OID クエリを受信しません。

NDIS ポートをサポートするミニポートドライバーでは、ndis [ **\_ステータス\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)の状態の表示を使用して、ndis ポートの状態の変更を示す必要があります。 ミニポートドライバーは、 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体のポート**番号メンバーに**ポート番号を設定する必要があります。

NDIS およびそれ以降のドライバーでは、 [oid\_GEN\_ポート\_認証\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters) oid を使用して、ndis ポートの現在の認証状態を設定します。 NDIS ポートをサポートするミニポートドライバーは、この OID をサポートする必要があります。

 

 





