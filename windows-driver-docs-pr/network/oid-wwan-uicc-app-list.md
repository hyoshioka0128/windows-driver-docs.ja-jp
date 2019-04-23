---
title: OID_WWAN_UICC_APP_LIST
description: OID_WWAN_UICC_APP_LIST、UICC 内のアプリケーションとそれらについての情報の一覧を取得します。
ms.assetid: C2E8CDBC-453A-4697-9BD9-1197FBDA2455
ms.date: 04/08/2019
keywords: -OID_WWAN_UICC_APP_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1661b5eb4baf57a302e1e12b96c74fb9e4f88b47
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905455"
---
# <a name="oidwwanuiccapplist"></a>OID_WWAN_UICC_APP_LIST

OID_WWAN_UICC_APP_LIST、UICC 内のアプリケーションとそれらについての情報の一覧を取得します。

ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_UICC_UICC_APP_LIST](ndis-status-wwan-uicc-app-list.md)状態の通知含む、 [ **NDIS_WWAN_UICC_APP_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list) UICC のアプリの一覧を記述する構造体。

要求のセットには適用されません。

## <a name="remarks"></a>注釈

ときにモデムで UICC が完全に初期化されると携帯電話会社に登録する準備ができて、UICC アプリケーションを選択してください登録とこの OID とクエリの要求で選択したアプリケーションを返す必要があります、 **ActiveAppIndex**のフィールド、 [ **WWAN_UICC_APP_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_uicc_app_list)応答で使用される構造です。

この OID の使用状況に関する詳細については、次を参照してください。 [MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)します。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10、バージョンが 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_UICC_APP_LIST](ndis-status-wwan-uicc-app-list.md)

[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)

[**WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_uicc_app_list)
