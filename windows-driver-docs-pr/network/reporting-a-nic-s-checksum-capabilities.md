---
title: NIC のチェックサム機能の報告
description: NIC のチェックサム機能の報告
ms.assetid: a90f8d01-8318-44de-acf0-7903ef7e85e0
keywords:
- タスクのオフロード WDK TCP/IP トランスポート、チェックサム タスク
- チェックサム タスク WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a00faa6a5cbe908f075c4fa822ffa2adce92d3de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530214"
---
# <a name="reporting-a-nics-checksum-capabilities"></a>NIC のチェックサム機能の報告





NDIS ミニポート ドライバーは、NIC が計算しでの IP、TCP、および UDP チェックサムの検証に現在構成されているかどうかを報告する[ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567878)構造体。 ミニポート ドライバーで現在のチェックサム オフロードの構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565930)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数を[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数を渡す、NDIS 情報\_ミニポート\_アダプター\_オフロード\_属性。

存在する場合、ミニポート ドライバーは現在のチェックサム オフロードの構成の変更を報告する必要がありますで、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_構成** ](https://msdn.microsoft.com/library/windows/hardware/ff567424)状態を示す値。

クエリに対する応答で[OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)、NDIS には、NDIS が含まれています\_TCP\_IP\_チェックサム\_オフロード構造、 [ **NDIS\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566599) NDIS を表す構造体、 **InformationBuffer**のメンバー、 [**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

ミニポート ドライバーは、IPv4 と IPv6 の送信および受信パケット、次のチェックサム情報を示します。

-   NIC を選択し、送信パケットを計算できますを検証できるチェックサム (IP、TCP または UDP) の型は、パケットを受信します。

-   カプセル化の設定で、**カプセル化**メンバー。 このメンバーの詳細については、「解説」セクションを参照してください。 [ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567878)します。

-   できるかどうか、NIC を計算または検証 (または計算検証) パケットのチェックサムが IP ヘッダーは、IPv4 のオプションを含めます。

-   できるかどうか、NIC を計算または検証 (または計算検証)、IPv6 パケットのチェックサムが IP ヘッダーは、IPv6 拡張ヘッダーを含めます。

-   NIC できますを計算または検証 (または計算し、検証) パケットのチェックサムかどうかを TCP ヘッダーには TCP オプションが含まれます。

## <a name="related-topics"></a>関連トピック


[タスクのオフロード機能を判断します。](determining-task-offload-capabilities.md)

 

 






