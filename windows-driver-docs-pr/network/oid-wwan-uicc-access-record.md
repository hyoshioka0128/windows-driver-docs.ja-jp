---
title: OID_WWAN_UICC_ACCESS_RECORD
description: OID_WWAN_UICC_ACCESS_RECORD は、WwanUiccFileStructureCyclic または WwanUiccFileStructureLinear の構造型である UICC 線形固定または循環ファイルにアクセスします。
ms.assetid: 450F397E-AC91-4239-BF60-B0DEB2F065DA
ms.date: 04/10/2019
keywords: -Windows Vista 以降の OID_WWAN_UICC_ACCESS_RECORD ネットワークドライバー
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 283f8ea15e012d62a531ac73501a5c5225c7c3e4
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443008"
---
# <a name="oid_wwan_uicc_access_record"></a>OID_WWAN_UICC_ACCESS_RECORD

OID_WWAN_UICC_ACCESS_RECORD は、 **WwanUiccFileStructureCyclic**または**WwanUiccFileStructureLinear**の構造型である uicc 線形固定または循環ファイルにアクセスします。

クエリ要求は、レコードの内容を読み取ります。 クエリペイロードには、読み取るファイルに関する情報を指定する[**NDIS_WWAN_UICC_ACCESS_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)構造体が含まれています。 ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に戻してから、 [NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)ステータス通知[**を**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)UICC の応答を記述する NDIS_WWAN_UICC_RESPONSE 構造体。 

## <a name="remarks"></a>注釈

この OID の使用方法の詳細については、「 [MB UICC アプリケーションとファイルシステムアクセス](mb-uicc-application-and-file-system-access.md)」を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイルシステムアクセス](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)

[**NDIS_WWAN_UICC_ACCESS_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
