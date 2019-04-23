---
title: OID_WWAN_UICC_ACCESS_BINARY
description: OID_WWAN_UICC_ACCESS_BINARY は UICC バイナリ ファイルの場合は、そのうち WwanUiccFileStructureTransparent または WwanUiccFileStructureBerTLV は、構造体型にアクセスします。
ms.assetid: D93939DB-3879-4B84-B7C9-7E6098C82786
ms.date: 04/10/2019
keywords: -OID_WWAN_UICC_ACCESS_BINARY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0c233c6cfb9cfded3cec6f813ec665da8b8daf73
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905417"
---
# <a name="oidwwanuiccaccessbinary"></a>OID_WWAN_UICC_ACCESS_BINARY

OID_WWAN_UICC_ACCESS_BINARY、構造型が、UICC バイナリ ファイルにアクセスする**WwanUiccFileStructureTransparent**または**WwanUiccFileStructureBerTLV**します。

クエリ要求は、バイナリ ファイルを読み取ります。 クエリのペイロードを含む、 [ **NDIS_WWAN_UICC_ACCESS_BINARY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_binary)を読み取るファイルに関する情報を指定する構造体。 ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE](ndis-status-wwan-uicc-binary-response.md)状態通知を含む、 [ **NDIS_WWAN_UICC_RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response) UICC の応答を記述する構造体。 

要求のセットは、バイナリ ファイルを更新します。 セットのペイロードを含む、 [ **NDIS_WWAN_UICC_ACCESS_BINARY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_binary)を書き込むファイルに関する情報を指定する構造体。 ミニポート ドライバーする必要がありますセット要求を非同期に処理、最初に NDIS_STATUS_INDICATION_REQUIRED を後で送信する前に、元の要求を返す、 [NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE](ndis-status-wwan-uicc-binary-response.md)状態の通知含む、 [ **NDIS_WWAN_UICC_RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response) UICC の応答を記述する構造体。 

## <a name="remarks"></a>注釈

この OID の使用状況に関する詳細については、次を参照してください。 [MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)します。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10、バージョンが 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE](ndis-status-wwan-uicc-binary-response.md)

[**NDIS_WWAN_UICC_ACCESS_BINARY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_binary) 

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
