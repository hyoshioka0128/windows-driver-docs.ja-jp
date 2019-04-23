---
title: OID_WWAN_UICC_ACCESS_RECORD
description: OID_WWAN_UICC_ACCESS_RECORD は UICC 線形固定または循環がファイルを構造型の WwanUiccFileStructureCyclic または WwanUiccFileStructureLinear にアクセスします。
ms.assetid: 450F397E-AC91-4239-BF60-B0DEB2F065DA
ms.date: 04/10/2019
keywords: -OID_WWAN_UICC_ACCESS_RECORD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7e92bd5d5a8e5ffc5f3277b95e5acd31e16f0dca
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905351"
---
# <a name="oidwwanuiccaccessrecord"></a>OID_WWAN_UICC_ACCESS_RECORD

OID_WWAN_UICC_ACCESS_RECORD ファイルにアクセスする UICC 線形固定または循環、構造型が**WwanUiccFileStructureCyclic**または**WwanUiccFileStructureLinear**します。

クエリ要求は、レコードの内容を読み取ります。 クエリのペイロードを含む、 [ **NDIS_WWAN_UICC_ACCESS_RECORD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)を読み取るファイルに関する情報を指定する構造体。 ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)状態通知を含む、 [ **NDIS_WWAN_UICC_RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response) UICC の応答を記述する構造体。 

要求のセットは、線形の固定または循環ファイルを更新します。 セットのペイロードを含む、 [ **NDIS_WWAN_UICC_ACCESS_RECORD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)を書き込むファイルに関する情報を指定する構造体。 ミニポート ドライバーする必要がありますセット要求を非同期に処理、最初に NDIS_STATUS_INDICATION_REQUIRED を後で送信する前に、元の要求を返す、 [NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)状態の通知含む、 [ **NDIS_WWAN_UICC_RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response) UICC の応答を記述する構造体。 

## <a name="remarks"></a>注釈

この OID の使用状況に関する詳細については、次を参照してください。 [MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)します。

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| バージョン | Windows 10、バージョンが 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)

[**NDIS_WWAN_UICC_ACCESS_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
