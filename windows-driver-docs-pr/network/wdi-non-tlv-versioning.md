---
title: WDI の TLV 以外のバージョン管理
description: このセクションでは、WDI の非 TLV バージョン管理について説明します。
ms.assetid: 19B5BEE1-BE17-40E3-99FA-D9BF4492D020
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86e4781e32ec0f4c24b068bc5b689ea65d64627a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842913"
---
# <a name="wdi-non-tlv-versioning"></a>WDI の TLV 以外のバージョン管理


WDI と IHV ミニポートの間で渡され、 [**ndis\_オブジェクト\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header) ( [**NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)など) を含むデータ構造は、標準の NDIS に従います。バージョン管理モデル。 ミニポートは、必要なフィールドが存在することを確認するために、**リビジョン**フィールドと**Size**フィールドを確認し、余分なフィールドやデータをエラーなしで無視する必要があります。 このような構造体の新しいリビジョンや大きなサイズが除外されていないことを確認します。

[**HEADER\_オブジェクト\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)を持たないすべてのデータ構造 ( [**WDI\_FRAME\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)など) は、TLV のバージョン管理モデルに従います。 WDI とミニポートでは、最も低い WdiVersion によって決定されるサイズ/リビジョンが使用されます。 [**NDIS\_WDI\_INIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)および[**ndis\_ミニポート\_ドライバー\_WDI\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)の値。

たとえば、WDI が\_Ndis で**WdiVersion**を設定した場合、 [**WDI\_INIT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)を**WDI\_VERSION\_1\_0**に設定し、ミニポートで ndis\_ミニポートに**WdiVersion**を設定し[ **\_DRIVER\_WDI\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)は**WDI\_version\_2\_0**になります。 WDI とミニポートの両方で、 **WDI\_version\_1 と互換性のある構造のサイズと定義を使用する必要があります。** [**NDIS\_OBJECT\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)フィールドのないすべての構造体に対して0を\_します。 ただし、同じ状況において、 **NDIS\_オブジェクト\_ヘッダー**フィールドを持つ構造体では、 **Revision**フィールドと**Size**フィールドが正しく設定されている限り、WDI とミニポートではより大きなまたはより新しい構造を使用する場合があります。

 

 





