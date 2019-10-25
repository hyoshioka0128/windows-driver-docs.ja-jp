---
title: コネクションレス ミニポート ドライバーの情報の設定
description: コネクションレス ミニポート ドライバーの情報の設定
ms.assetid: 406d844a-cc83-4cd6-a2d2-78e614aab900
keywords:
- コネクションレスドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96da894b88fa723ed6e5e3b5080dca66e4b087f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841943"
---
# <a name="setting-information-for-a-connectionless-miniport-driver"></a>コネクションレス ミニポート ドライバーの情報の設定





コネクションレスミニポートドライバーによって保持される OID を設定するために、バインドされたプロトコルは[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出し、要求構造を[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)渡します。この構造は、クエリ対象のオブジェクト (oid) を指定し、それがバッファーを指します。オブジェクトを設定する必要がある値を格納している。 **NdisOidRequest**を呼び出すと、NDIS はミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数を呼び出します。この関数は、指定された値を使用してオブジェクトを設定します。

*Miniportoidrequest*の呼び出しは、同期または非同期で完了できます。 呼び出しを非同期に完了するために、ミニポートドライバーは[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)を呼び出します。 次の図は、コネクションレスミニポートドライバー (バインドごと) の情報を設定する方法を示しています。

![コネクションレスミニポートドライバーの設定情報を示す図 (バインドごと)](images/fig5-4.png)

 

 





