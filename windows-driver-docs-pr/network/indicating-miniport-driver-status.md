---
title: ミニポート ドライバーの状態の表示
description: ミニポート ドライバーの状態の表示
ms.assetid: 366caecb-6c4b-42f3-927d-b72db764d6cf
keywords:
- WDK いる CoNDIS のステータス情報
- 接続指向 NDIS WDK、ミニポート ドライバー
- いる CoNDIS WDK ネットワー キング、ミニポート ドライバー
- ミニポート ドライバー WDK ネットワー キング、いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b998cc9d22959f273b4366c5824a63c0a632fea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327750"
---
# <a name="indicating-miniport-driver-status"></a>ミニポート ドライバーの状態の表示





ミニポート ドライバーでは、ドライバーに関連する状態インジケーターを提供します。 いる CoNDIS 状態を示す値の関数は、コネクションレスの状態を示す値の関数に似ています。

接続指向のミニポート ドライバーを呼び出し、NIC の接続指向の NIC のステータスの変更または特定の VC アクティブの状態の変更を報告する[ **NdisMCoIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563562)します。 提供されている場合は、ミニポート ドライバーが特定の VC のステータスの変更を報告、 *NdisVcHandle* VC を識別します。

ここでは、次のトピックについて説明します。

[いる CoNDIS ミニポート ドライバーの状態インジケーター](condis-miniport-driver-status-indications.md)

[いる CoNDIS プロトコル ドライバーの処理状態のインジケーター](handling-status-indications-in-a-condis-protocol-driver.md)

 

 





