---
title: NDIS でサポートされている WMI の操作
description: NDIS でサポートされている WMI の操作
ms.assetid: 78dfe8a6-25aa-40d4-bc32-19bd1d4a41b1
keywords:
- Windows Management Instrumentation WDK ネットワー キング、NDIS 操作
- WMI の WDK は、ネットワーク NDIS 操作
- 仮想接続 WDK NDIS WMI
- VCs WDK NDIS WMI
- ミニポート アダプタ WDK ネットワーク、列挙します。
- アダプター WDK ネットワーク、列挙します。
- QU
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eedbbd90727ca5cba19f1675fe5fa2c5bf32fc1e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384383"
---
# <a name="ndis-supported-wmi-operations"></a>NDIS でサポートされている WMI の操作





NDIS は、次の WMI 操作をサポートしています。

-   アダプターを列挙し、仮想接続 (VC) を列挙します。

    NDIS グローバル Guid を登録します ( [GUID\_NDIS\_ENUMERATE\_アダプター\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/guid-ndis-enumerate-adapters-ex)と GUID\_NDIS\_ENUMERATE\_VC) wmi を(つまり、ミニポート ドライバーのインスタンス) のすべてのミニポート アダプターを列挙する WMI クライアントを有効にするという名前のすべての VCs とします。 NDIS は、すべての読み込まれたミニポート ドライバーとそのすべての名前付きの VCs を追跡、ため、NDIS はこのような情報のミニポート ドライバーをクエリできません。

-   クエリの 1 つのインスタンスと 1 つのインスタンスの設定

    NDIS、を通じて WMI クライアントがクエリか、1 つの OID に対応するデータ ブロックの 1 つのインスタンスを設定できます。 クエリの場合は、NDIS は、すべてのアダプターまたは VC に関連付けられている情報を返します。 WMI クライアントでは、クエリまたは OID 内にあるデータ項目を設定できません。 たとえば、GUID のクエリ\_NDIS\_GEN\_CO\_リンク\_速度の GUID は、送信および受信速度の両方を返します。 WMI クライアントには、送信速度のみまたは受信速度のみをクエリできません。

-   すべてのデータを照会します。

    NDIS 適切なデータを取得し、WMI に GUID のインスタンスのすべての結合されたデータを返すことで特定の GUID のすべてのデータのクエリ要求に応じます。 たとえば、クエリのすべてのデータの要求に対して応答で[GUID\_NDIS\_ENUMERATE\_アダプター\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/guid-ndis-enumerate-adapters-ex)NDIS が WMI にすべての読み込まれたミニポート ドライバーの一覧を返します。 OID にマップされる GUID のクエリすべてのデータに対して\_GEN\_CO\_XMIT\_PDU\_NDIS が、各接続指向のミニポート ドライバーでは、各 VC の OID を照会し、WMI に組み合わされたデータを返します。 すべてのデータのクエリ要求のオーバーヘッドは非常に高くなる可能性があります、ために、WMI クライアントは、アダプターと VCs 列挙にのみクエリのすべてのデータ要求を使用する必要があります。 アダプターまたは VC 対象を決定した後、クライアントは、個々 のインスタンスの GUID を照会できます。

-   EVENT NOTIFICATION

    WMI クライアントは、特定の状態を示す値を通知する NDIS を登録できます。 このような状態の表示が発生したときに NDIS は WMI にステータス情報を適切な GUID を WMI イベントとして、クライアントに配信するために渡します。

-   メソッドを実行します。

    NDIS、を通じて WMI クライアントは、1 つの OID に対応するデータ ブロックに関連付けられているメソッドを実行できます。 WMI クライアントでは、NDIS メソッドを実行する必要がある情報を提供します。 メソッドの要求は、ミニポート アダプター、NDIS ポートまたは VCs を関連付けることができます。 NDIS は、メソッドが正常に実行した後、結果として得られる情報を返します。

 

 





