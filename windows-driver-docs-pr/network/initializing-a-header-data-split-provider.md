---
title: ヘッダー データの分割プロバイダーの初期化
description: ヘッダー データの分割プロバイダーの初期化
ms.assetid: 19a01906-6a05-4f57-a22a-911138095c84
keywords:
- ヘッダー データ プロバイダーの初期化、WDK の分割
- プロバイダーを分割ヘッダー データの初期化
- ヘッダー データ プロバイダー WDK の分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0428bda9564f93e23cc94dba634057ddd4443f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371828"
---
# <a name="initializing-a-header-data-split-provider"></a>ヘッダー データの分割プロバイダーの初期化





ヘッダー データをサポートするには、分割、ミニポート ドライバーは、NDIS 6.1 またはそれ以降のドライバーとして登録する必要があります。 ソース ファイル、ミニポート ドライバーが DNDIS61 を指定する必要がありますの\_ミニポート DNDIS60 ではなく 1 を =\_ミニポート = 1。 ミニポート ドライバーには、NDIS 6.1 またはそれ以降のバージョンでもを指定する必要があります、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)構造体。

NDIS 6.1 のミニポート ドライバーを呼び出してそのヘッダー データの分割属性を登録する、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数からその[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数を渡します**NdisMSetMiniportAttributes**初期化された[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性の構造体には、次の情報が含まれています。

-   **HDSplitAttributes**の NDIS メンバー\_ミニポート\_アダプター\_ハードウェア\_支援\_属性にはへのポインターが含まれています、 [ **NDIS\_HD\_分割\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_hd_split_attributes)ヘッダー データを指定する構造体がミニポート アダプターが用意されている機能を分割します。

-   **HardwareCapabilities**の NDIS メンバー\_HD\_分割\_属性には、ミニポート アダプターをサポートするヘッダー データ分割機能が含まれています。 これらの機能は、INF ファイルの設定、または、現在無効になっている機能を含めることができます、**詳細**プロパティ ページ。

-   **CurrentCapabilities**の NDIS メンバー\_HD\_分割\_属性には、ミニポート アダプターがサポートしている現在のヘッダー データ分割機能が含まれています。 を通じてヘッダー データの分割が有効になっている場合、  **\*HeaderDataSplit**標準化された INF キーワード、ミニポート ドライバーとして同じフラグを使用して、 **HardwareCapabilities**メンバーを示すために、現在のヘッダー データは、構成を分割します。 詳細については **\*HeaderDataSplit**を参照してください[ヘッダー データの分割の標準化された INF キーワード](standardized-inf-keywords-for-header-data-split.md)します。

-   **HDSplitFlags**の NDIS メンバー\_HD\_分割\_属性にはヘッダー データ分割構成のフラグにはが含まれています。 ミニポート ドライバーは、このメンバーを呼び出す前に 0 を設定する必要があります[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。 NDIS は、構成のフラグのビットごとの OR と共にこのメンバーを設定します。 後**NdisMSetMiniportAttributes**正常に戻り値は、ミニポート ドライバーする必要があります確認フラグの設定**HDSplitFlags**し、それに応じてハードウェアを構成します。

NDIS は、NDIS\_HD\_分割\_を有効にする\_ヘッダー\_データ\_ヘッダー データ ミニポート アダプターの分割を有効にするフラグを分割します。 NDIS は NDIS 設定されていない\_HD\_分割\_を有効にする\_ヘッダー\_データ\_ミニポート ドライバーでは、NDIS を設定しなかった場合、分割\_HD\_分割\_CAP\_サポート\_ヘッダー\_データ\_分割フラグ、 **CurrentCapabilities**のメンバー、 [ **NDIS\_HD\_分割\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_hd_split_attributes)構造体。 ミニポート ドライバーには、ヘッダー データ NDIS NDIS を設定する場合は、NIC で分割が有効にする必要があります\_HD\_分割\_を有効にする\_ヘッダー\_データ\_分割フラグ。

ミニポート ドライバーを設定する必要があります、 **BackfillSize**の NDIS メンバー\_HD\_分割\_属性の構造体を呼び出す前にゼロに[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。 NDIS セット、 **BackfillSize**メンバーの場合、ミニポート ドライバーは、分割フレームのデータ バッファー内のバックフィル記憶域を割り当てる事前する必要があります。 後**NdisMSetMiniportAttributes**正常に返されます、ミニポート ドライバーを使用する必要があります、 **BackfillSize**値の指定されたその NDIS と事前にデータ バッファーを割り当てています。 データ バッファーのバックフィル サイズの詳細については、次を参照してください。[データ バッファーの割り当てのバックフィル](allocating-backfill-for-the-data-buffer.md)します。

ミニポート ドライバーを設定する必要があります、 **MaxHeaderSize**のメンバー、 [ **NDIS\_HD\_分割\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_hd_split_attributes)構造体を呼び出しの前に 0 **NdisMSetMiniportAttributes**します。 NDIS は、このメンバーを分割フレームのヘッダーのバッファーで許可される最大サイズに設定します。 後**NdisMSetMiniportAttributes**正常に返されます、ミニポート ドライバーを使用する必要があります、 **MaxHeaderSize**その NDIS が指定された値します。 ヘッダーの最大サイズの詳細については、次を参照してください。[ヘッダーのバッファーを割り当てる](allocating-the-header-buffer.md)します。

 

 





