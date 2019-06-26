---
title: ポート認証パラメーターの設定
description: ポート認証パラメーターの設定
ms.assetid: 88ac8229-d1d5-4287-8b5d-3a7b9b1f2e89
keywords:
- WDK の NDIS OID 要求をポートします。
- NDIS ポート WDK、OID 要求
- OID 要求 WDK NDIS ポート
- WDK NDIS ポートの認証パラメーター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b5f4136862c496ce934dd0d395b5ecfeeb9dab1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375144"
---
# <a name="setting-port-authentication-parameters"></a>ポート認証パラメーターの設定





NDIS および上にあるドライバーを使用して、 [OID\_GEN\_ポート\_認証\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters) OID は、NDIS ポートの現在の状態を設定する要求を設定します。 NDIS ポートをサポートするミニポート ドライバーでは、この OID をサポートする必要があります。

ミニポート ドライバーが、受信ポートの方向、ポートのコントロールの状態を使用して状態からの認証とセットの要求が成功した場合、 [ **NDIS\_ポート\_認証\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)構造体。

ミニポートを生成する必要があります、 [ **NDIS\_状態\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)状態の変更の上にあるドライバーに通知する状態を示す値。

 

 





