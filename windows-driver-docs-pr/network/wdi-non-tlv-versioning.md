---
title: WDI の TLV 以外のバージョン管理
description: このセクションでは、WDI TLV 以外のバージョン管理を説明します。
ms.assetid: 19B5BEE1-BE17-40E3-99FA-D9BF4492D020
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0bc4495562384a904e542575e85e66fdc59c1f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381154"
---
# <a name="wdi-non-tlv-versioning"></a>WDI の TLV 以外のバージョン管理


WDI および IHV ミニポート間で渡され、含まれているデータ構造を[ **NDIS\_オブジェクト\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header) (など[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)) 標準の NDIS バージョン管理モデルに従います。 ミニポートを確認する必要があります、**リビジョン**と**サイズ**フィールドを関連するフィールドが存在することを確認し、余分なフィールドやエラーのないデータを無視します。 新しいバージョンまたはより大きなこのような構造のサイズが除外されていないことを確認します。

せず、すべてのデータ構造、 [ **NDIS\_オブジェクト\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header) (など[ **WDI\_フレーム\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)) WDI およびミニポートが低い方によって決まりますサイズ/リビジョン使用して、TLV バージョン管理モデルに従ってください**WdiVersion**値から[ **NDIS\_WDI\_INIT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)と[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics).

たとえば、WDI 設定**WdiVersion**で[ **NDIS\_WDI\_INIT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)に**WDI\_バージョン\_1\_0**、およびミニポート セット**WdiVersion**で[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)に**WDI\_バージョン\_2\_0**、WDI およびミニポートの両方が、構造体のサイズを使用する必要があり、定義と互換性のある**WDI\_バージョン\_1\_0**ことがなくすべての構造体[ **NDIS\_オブジェクト\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)フィールド。 ただし、同じ状況が構造体を持つ、 **NDIS\_オブジェクト\_ヘッダー**フィールド、WDI およびミニポート限り大きくまたは新しい構造体を使用できます、**リビジョン**と**サイズ**フィールドが正しく設定されています。

 

 





