---
title: OID_WWAN_UICC_APP_LIST
description: OID_WWAN_UICC_APP_LIST は、UICC 内のアプリケーションの一覧と、それらに関する情報を取得します。
ms.assetid: C2E8CDBC-453A-4697-9BD9-1197FBDA2455
ms.date: 04/08/2019
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_UICC_APP_LIST
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: da57f9d8586c957cb49d2da8f25e45ac8ca2531c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916593"
---
# <a name="oid_wwan_uicc_app_list"></a>OID_WWAN_UICC_APP_LIST

OID_WWAN_UICC_APP_LIST は、UICC 内のアプリケーションの一覧と、それらに関する情報を取得します。

ミニポートドライバーでは、クエリ要求を非同期的に処理し、その後、UICC のアプリリストを記述する[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)構造を含む[NDIS_STATUS_WWAN_UICC_UICC_APP_LIST](ndis-status-wwan-uicc-app-list.md)状態通知を送信する前に、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に返す必要があります。

Set 要求は適用できません。

## <a name="remarks"></a>注釈

モデムの UICC が完全に初期化され、携帯電話会社に登録する準備ができたら、UICC アプリケーションを登録用に選択する必要があります。この OID を使用したクエリ要求では、選択したアプリケーションが応答で使用される[**WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_uicc_app_list)構造体の**activeappindex**フィールドで返されます。

この OID の使用方法の詳細については、「 [MB UICC アプリケーションとファイルシステムアクセス](mb-uicc-application-and-file-system-access.md)」を参照してください。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1903**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_UICC_APP_LIST](ndis-status-wwan-uicc-app-list.md)

[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)

[**WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_uicc_app_list)
