---
title: ポート認証パラメーターの設定
description: ポート認証パラメーターの設定
ms.assetid: 88ac8229-d1d5-4287-8b5d-3a7b9b1f2e89
keywords:
- ポート WDK NDIS、OID 要求
- NDIS ポート WDK、OID 要求
- OID が WDK NDIS ポートを要求する
- 認証パラメーター WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9d87dd9bf52821b4dedc280b6d32cfc5a6bb036
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841936"
---
# <a name="setting-port-authentication-parameters"></a>ポート認証パラメーターの設定





NDIS およびそれ以降のドライバーでは、 [oid\_GEN\_ポート\_認証\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters) oid セット要求を使用して、ndis ポートの現在の状態を設定します。 NDIS ポートをサポートするミニポートドライバーは、この OID をサポートする必要があります。

設定要求が成功した場合、ミニポートドライバーは、 [**NDIS\_ポート\_認証\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)構造からの受信ポートの方向、ポート制御状態、および認証状態を使用します。

ミニポートは、状態が変化したときにドライバーに通知するために、 [**NDIS\_ステータス\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)の状態の表示を生成する必要があります。

 

 





