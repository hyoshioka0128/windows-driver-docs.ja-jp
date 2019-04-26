---
title: MB ミニポート ドライバーの初期化
description: MB ミニポート ドライバーの初期化
ms.assetid: cf332eb4-faea-40e3-b313-512f81718267
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9fa73ca04d98e4fb0b848fccb19f187420ced88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343327"
---
# <a name="mb-miniport-driver-initialization"></a>MB ミニポート ドライバーの初期化


次の図は、MB インターフェイスとしてインターフェイスを修飾するかどうかを判断すると、デバイスの機能に関する情報を収集するプロセスを表します。 次の手順は、サービスの起動時、MB も新しい各インターフェイスが届くと、サービスの実行中に列挙された各 MB インターフェイスに対して実行されます。 太字表す OID の識別子またはトランザクションのフロー制御には、ラベルと通常のテキストに表示されるラベルは、OID 構造内で重要なフラグを表します。

![インターフェイスは mb インターフェイスとして修飾されているかどうかを確立して、デバイスの機能に関する情報を収集するかを示すを示す図](images/wwandriverinitproc.png)

MB のミニポート ドライバーを初期化するには、次の手順を使用します。

1.  MB サービスは、同期 (ブロック) を送信[OID\_GEN\_物理\_MEDIUM](https://msdn.microsoft.com/library/windows/hardware/ff569621) MB デバイスの種類を識別するためにクエリ要求。 ミニポート ドライバーで応答した**NdisPhysicalMediumWirelessWan** MB デバイスが WWAN デバイスであることを示します。

2.  MB サービスは、同期 (ブロック) を送信[OID\_GEN\_メディア\_サポートされている](https://msdn.microsoft.com/library/windows/hardware/ff569609)MB デバイスでの使用のメディアの種類を識別するために、ミニポート ドライバーにクエリ要求。 ミニポート ドライバーで応答した**NdisMedium802\_3**をイーサネット エミュレーションを使用しているかを示します。

3.  MB サービスは、同期 (ブロック) を送信[OID\_WWAN\_ドライバー\_CAP](https://msdn.microsoft.com/library/windows/hardware/ff569825)クエリ要求にどのようなドライバー モデルのバージョンを識別するために、ミニポート ドライバー、ミニポート ドライバーをサポートしています。 ミニポート ドライバーで応答した WWAN\_バージョン。

4.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_デバイス\_CAP](https://msdn.microsoft.com/library/windows/hardware/ff569824) MB デバイスの機能を識別するために、ミニポート ドライバーにクエリ要求。 ミニポート ドライバーは、要求を受信したことに必要な情報、今後の通知は送信 provisional 受信確認応答します。

5.  ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_デバイス\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff567845)の機能を示す MB サービスへの通知MB デバイス ミニポート ドライバーをサポートします。 たとえば、ミニポート ドライバーでは、GSM ベースのデバイスをサポートする場合は指定する必要が、 **WwanCellularClassGsm**値、 **DeviceCaps.WwanCellularClass**のメンバー、 [ **NDIS\_WWAN\_デバイス\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff567907)構造体。 これを指定する必要があるかどうか、ミニポート ドライバーは、CDMA ベースのデバイスをサポートする**WwanCellularClassCdma**します。

 

 





