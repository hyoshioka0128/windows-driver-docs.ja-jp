---
title: ヘッダー データの分割プロバイダーの初期化
description: ヘッダー データの分割プロバイダーの初期化
ms.assetid: 19a01906-6a05-4f57-a22a-911138095c84
keywords:
- ヘッダー-データ分割 WDK、初期化プロバイダー
- ヘッダーデータ分割プロバイダーの初期化
- ヘッダー-データ分割プロバイダー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc4995dc85ec29d87474eb110ee7d0275a899e5f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824598"
---
# <a name="initializing-a-header-data-split-provider"></a>ヘッダー データの分割プロバイダーの初期化





ヘッダーデータの分割をサポートするには、ミニポートドライバーを NDIS 6.1 以降のドライバーとして登録する必要があります。 ミニポートドライバーのソースファイルでは、DNDIS60 ではなく DNDIS61\_ミニポート = 1 を指定する必要があります\_ミニポート = 1 です。 また、ミニポートドライバーでは、ndis 6.1 以降のバージョンを[**ndis\_ミニポート\_ドライバーの\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造に指定する必要があります。

ヘッダーデータの分割属性を登録するために、NDIS 6.1 ミニポートドライバーは[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、初期化された ndis**を渡します**。 [ **\_ミニポート\_アダプター\_ハードウェア\_\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の構造をサポートします。

NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性構造には、次の情報が含まれています。

-   NDIS\_ミニポート\_アダプターの**Hdsplitattributes**メンバー\_ハードウェア\_アシスト\_属性には、 [**ndis\_HD\_SPLIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)\_のポインターが含まれています。ミニポートアダプターによって提供されるヘッダーデータの分割機能。

-   NDIS\_HD\_SPLIT\_属性の**HardwareCapabilities**メンバーには、ミニポートアダプターがサポートするヘッダーデータの分割機能が含まれています。 これらの機能には、INF ファイルの設定によって現在無効になっている機能や、 **[詳細設定**] プロパティページがあります。

-   NDIS\_HD\_SPLIT\_ATTRIBUTES の**Currentcapabilities**メンバーには、ミニポートアダプターがサポートする現在のヘッダーデータの分割機能が含まれています。 ヘッダーデータの分割が **\*HeaderDataSplit**標準化された INF キーワードを使用して有効になっている場合、ミニポートドライバーは、現在のヘッダーデータの分割構成を示すために**HardwareCapabilities**メンバーと同じフラグを使用します。 **HeaderDataSplit\*** の詳細については、「[ヘッダーデータの分割に関する標準化](standardized-inf-keywords-for-header-data-split.md)された INF キーワード」を参照してください。

-   NDIS\_HD\_SPLIT\_属性には、ヘッダーデータの分割構成フラグを含む**Hdsplitflags**メンバーが含まれています。 ミニポートドライバーは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出す前に、このメンバーを0に設定する必要があります。 NDIS は、このメンバーに構成フラグのビットごとの OR を設定します。 **NdisMSetMiniportAttributes**が正常にを返した後、ミニポートドライバーは**Hdsplitflags**のフラグ設定を確認し、それに応じてハードウェアを構成する必要があります。

Ndis は、NDIS\_HD\_SPLIT\_使用して\_ヘッダー\_データ\_分割フラグを有効にして、ミニポートアダプターのヘッダーデータの分割を有効にします。 Ndis では、NDIS\_HD\_SPLIT\_有効にされません。ミニポートドライバーでは、\_がサポート\_する NDIS\_HD\_SPLIT が設定されていない場合、データ\_分割\_t_10_ HEADER\_データ\_、 [**NDIS\_HD\_split\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)構造体の**CURRENTCAPABILITIES**メンバーの分割フラグ。 NDIS で NDIS\_HD\_\_SPLIT に設定されている場合は、ミニポートドライバーでヘッダーデータの分割を有効にする必要があります。これにより、\_ヘッダー\_データ\_分割フラグが有効になります。

ミニポートドライバーでは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出す前に、NDIS\_HD\_SPLIT\_ATTRIBUTES 構造体の**backfillsize**メンバーを0に設定する必要があります。 ミニポートドライバーが分割フレームのデータバッファーにバックフィルストレージを事前に割り当てる必要がある場合、NDIS は**Backfillsize**メンバーを設定します。 **NdisMSetMiniportAttributes**が正常にを返した後、ミニポートドライバーは、NDIS によって指定された**backfillsize**値を使用し、データバッファーを事前に割り当てている必要があります。 データバッファーのバックフィルサイズの詳細については、「[データバッファーのバックフィルの割り当て](allocating-backfill-for-the-data-buffer.md)」を参照してください。

ミニポートドライバーは、 **NdisMSetMiniportAttributes**を呼び出す前に、 [**NDIS\_HD\_SPLIT\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)構造体の**maxheadersize**メンバーを0に設定する必要があります。 NDIS は、このメンバーを分割フレームのヘッダーバッファーで許可される最大サイズに設定します。 **NdisMSetMiniportAttributes**が正常にを返した後、ミニポートドライバーは、NDIS が指定した**maxheadersize**値を使用する必要があります。 ヘッダーの最大サイズの詳細については、「[ヘッダーバッファーの割り当て](allocating-the-header-buffer.md)」を参照してください。

 

 





