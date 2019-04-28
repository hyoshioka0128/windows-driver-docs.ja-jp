---
title: NIC からのセキュリティ アソシエーションの削除
description: NIC からのセキュリティ アソシエーションの削除
ms.assetid: 739a3fef-f0b4-4d7c-9d92-df52fd27915d
keywords:
- セキュリティ アソシエーション WDK IPsec オフロードします。
- SAs の WDK IPsec オフロード
- WDK の IPsec ESP により保護されたパケットのオフロード、セキュリティ アソシエーション
- AH で保護されたパケット WDK IPsec オフロード、セキュリティ アソシエーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4383bcc985733b0e130945a9f70d77108ee64d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364238"
---
# <a name="deleting-a-security-association-from-a-nic"></a>NIC からのセキュリティ アソシエーションの削除

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




必要に応じて、TCP/IP トランスポート設定できます[OID\_TCP\_タスク\_IPSEC\_削除\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569810)ミニポート ドライバーが、セキュリティ アソシエーション (SA) を削除することを要求するにはNIC から

NIC で SA をもう 1 つのスペースを作成するミニポート ドライバーを設定できます、 **SaDeleteReq**フラグ、 [ **NDIS\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565801)受信パケットの構造体。 TCP/IP トランスポートは、OID を後で発行\_TCP\_タスク\_IPSEC\_削除\_SA にパケットが受信された受信セキュリティ アソシエーション (SA) を削除する 1 つの時間と別の日時に削除された着信 SA に対応する送信の SA を削除します。 NIC を削除しないでこれらの SAs のいずれかの対応する OID を受信する前に\_TCP\_タスク\_IPSEC\_削除\_SA 要求。 ミニポート ドライバーを設定できます**SaDeleteReq**とは無関係に、 **CryptoDone**フラグ。
