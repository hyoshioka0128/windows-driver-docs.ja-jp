---
title: ヘッダー データ分割による受信表示
description: ヘッダー データ分割による受信表示
ms.assetid: 76abeac8-ca6e-40b1-a46e-83ae90d9192e
keywords:
- ヘッダー-データ分割 WDK、受信通知
- 受信したデータ形式 WDK ヘッダー-データ分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e9fdcba79c33acbd4a08db85e058d0d96f6f915
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844862"
---
# <a name="receive-indications-with-header-data-split"></a>ヘッダー データ分割による受信表示





ヘッダーデータの分割をサポートするミニポートドライバーは、ヘッダーデータの分割に必要な形式で受信したデータを示す必要があります。 たとえば、ヘッダーバッファーはすべて連続したストレージブロック内に存在する必要があり、データバッファーにはバックフィル領域が含まれている必要があります。

分割フレーム内のヘッダー情報には、仮想 LAN (VLAN) タグを含めないでください。 ヘッダーデータを分割するには、ハードウェアでの VLAN のサポートが必要です。また、受信フレームから VLAN タグを削除し、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の**Ieee8021QNetBufferListInfo** OOB 情報に配置する必要があります。 ミニポートドライバーでは、 [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造の**macoptions**メンバー、および[OID\_GEN\_MAC への応答として、VLAN のサポートを指定する必要があり\_オプション](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-mac-options)の OID クエリ。

NDIS およびそれ以降のドライバーまたはユーザーモードアプリケーションでは、 [oid\_GEN\_HD\_分割\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters) oid を使用して、ミニポートアダプターの現在のヘッダーデータ分割設定を設定します。 NDIS\_HD\_SPLIT\_を組み合わせると、 [**ndis\_hd\_split\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)構造体の**Hdsplit連結 eflags**メンバー内のすべての\_HEADERS フラグが組み\_合わされます。では、ミニポートアダプターですべての分割フレームを結合する必要があります。 ハードウェアでヘッダーデータの分割が有効になっている場合、ミニポートドライバーは、フレームを NDIS に示す前にヘッダーとデータを結合する必要があります。 OID\_GEN\_HD\_分割\_パラメーター、およびその他の管理と構成の問題の詳細については、「[ヘッダー-データの分割管理と構成](header-data-split-administration-and-configuration.md)」を参照してください。

このセクションの内容:

[ヘッダーバッファーを割り当てています](allocating-the-header-buffer.md)

[データバッファーのバックフィルの割り当て](allocating-backfill-for-the-data-buffer.md)

[ネットワーク\_バッファー\_リスト情報を設定しています](setting-net-buffer-list-information.md)

 

 





