---
title: WDI_TLV_OFFLOAD_SCOPE
description: WDI_TLV_OFFLOAD_SCOPE は、Rx 結合オフロード機能を含む TLV です。
ms.assetid: 2E00659F-4A41-4907-AEA6-92EAFBFF2149
ms.date: 10/05/2017
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_OFFLOAD_SCOPE
ms.localizationpriority: medium
ms.openlocfilehash: 570e0ba1bd44ba1082105347c03cb5a2b7ff4f80
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968529"
---
# <a name="wdi_tlv_offload_scope"></a>WDI_TLV_OFFLOAD_SCOPE


WDI_TLV_OFFLOAD_SCOPE は、ネットワークのオフロードの範囲を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x143

## <a name="length"></a>長さ


以下の値のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | [説明] |
| --- | --- |
| UINT8 | すべてのポートにチェックサムオフロードパラメーターを適用するかどうかを指定します。 <p>指定できる値</p> <ul><li>0: 該当なし</li><li>1: 該当する</li></ul> |
| UINT8 | LsoV1 オフロードパラメーターをすべてのポートで適用できるかどうかを指定します。 <p>指定できる値</p> <ul><li>0: 該当なし</li><li>1: 該当する</li></ul> |
| UINT8 | LsoV2 オフロードパラメーターをすべてのポートで適用できるかどうかを指定します。 <p>指定できる値</p> <ul><li>0: 該当なし</li><li>1: 該当する</li></ul> |
| UINT8 | RSC オフロードパラメーターをすべてのポートに適用するかどうかを指定します。 <p>指定できる値</p> <ul><li>0: 該当なし</li><li>1: 該当する</li></ul> |
 

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1709

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Wditypes




