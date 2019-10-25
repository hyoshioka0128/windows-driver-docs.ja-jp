---
title: ヘッダー データの分割のアーキテクチャ
description: ヘッダー データの分割のアーキテクチャ
ms.assetid: a2594360-cbac-4f77-840a-2572a2381646
keywords:
- ヘッダー-データ分割 WDK、アーキテクチャ
- ヘッダー-データ分割プロバイダー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a12823d8ed28a48662059dda78535717801e432
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842544"
---
# <a name="header-data-split-architecture"></a>ヘッダー データの分割のアーキテクチャ





ヘッダーデータ分割プロバイダーは、受信したイーサネットフレーム内のヘッダーとデータを別々のバッファーに分割することで、ネットワークパフォーマンスを向上させます。 ヘッダーデータ分割プロバイダーには、ネットワークインターフェイスカード (NIC) と、NIC にサービスを提供する NDIS 6.1 以降のミニポートドライバーが含まれています。

次の図は、ヘッダーデータの分割アーキテクチャを示しています。

![ヘッダーデータの分割アーキテクチャを示す図](images/hdsplitarchitecture.png)

ミニポートドライバーは、NDIS から構成情報を受け取り、ヘッダーデータの分割受信操作用に NIC を設定します。 また、ミニポートドライバーは、送信操作や受信操作などの実行時操作のために、NIC のサービスを NDIS に公開します。

ヘッダーデータの分割操作が可能な NIC は、イーサネットフレームを受信し、ヘッダーとデータを別々の受信バッファーに分割します。

ミニポートドライバーは、NDIS に受信したデータを示すために通常の NDIS 受信機能を使用します。 また、ドライバーは、受信したデータを示すときに、net [ **\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体に厳密に1つの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体を割り当てる必要があります。 詳細については、「[受信したイーサネットフレームを示す](indicating-received-ethernet-frames.md)」を参照してください。

ヘッダーデータの分割の場合、受信表示の[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造は、ヘッダーとデータに個別のメモリ記述子リスト (mdls) を使用して、受信したイーサネットフレームを分割します。 また、 [**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体には、NET\_BUFFER\_リスト情報のヘッダーデータの分割情報が含まれています。

次の図は、受信フレーム、分割バッファー、およびヘッダーバッファーのメモリレイアウトを示しています。

![受信フレーム、分割バッファー、およびヘッダーバッファーのメモリレイアウトを示す図](images/hdspllitbuffers.png)

ヘッダーバッファーは、すべて連続したストレージブロック内に存在する必要があります。

*上位層プロトコル*は、TCP、UDP、ICMP などの IP トランスポートプロトコルです。

**注**  ヘッダーデータの分割要件を定義するために、IPsec は上位層のプロトコルとは見なされません。 IPsec フレームの分割の詳細については、「 [Ipsec フレームの分割](splitting-ipsec-frames.md)」を参照してください。

 

 

 





