---
title: OID_WWAN_UICC_ACCESS_RECORD
description: OID_WWAN_UICC_ACCESS_RECORD は、UICC 線形固定ファイルまたは循環ファイルにアクセスします。構造型は WwanUiccFileStructureCyclic または WwanUiccFileStructureLinear です。
ms.assetid: 450F397E-AC91-4239-BF60-B0DEB2F065DA
ms.date: 04/10/2019
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_UICC_ACCESS_RECORD
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 2f853fe0585d16a30400f208f4062752e06f6d90
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916595"
---
# <a name="oid_wwan_uicc_access_record"></a>OID_WWAN_UICC_ACCESS_RECORD

OID_WWAN_UICC_ACCESS_RECORD は、UICC 線形固定ファイルまたは循環ファイルにアクセスします。構造型は**WwanUiccFileStructureCyclic**または**WwanUiccFileStructureLinear**です。

クエリ要求は、レコードの内容を読み取ります。 クエリペイロードには、読み取るファイルに関する情報を指定する[**NDIS_WWAN_UICC_ACCESS_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)構造が含まれています。 ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に元の要求に NDIS_STATUS_INDICATION_REQUIRED を返してから、UICC の応答を記述する[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)構造を含む[NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)状態通知を送信する必要があります。 

## <a name="remarks"></a>注釈

この OID の使用方法の詳細については、「 [MB UICC アプリケーションとファイルシステムアクセス](mb-uicc-application-and-file-system-access.md)」を参照してください。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1903**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)

[**NDIS_WWAN_UICC_ACCESS_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
