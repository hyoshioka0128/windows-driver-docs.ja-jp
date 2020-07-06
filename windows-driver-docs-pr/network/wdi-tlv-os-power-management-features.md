---
title: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES
description: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES は、OS 電源管理機能のフラグを含む TLV です。
ms.assetid: 4F104956-1B26-47DF-A58F-53C24B75DB77
ms.date: 03/30/2018
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_OS_POWER_MANAGEMENT_FEATURES
ms.localizationpriority: medium
ms.openlocfilehash: f92da82ba80ac3d4104e3f01b7b56811d9a6aad8
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967939"
---
# <a name="wdi_tlv_os_power_management_features"></a>WDI_TLV_OS_POWER_MANAGEMENT_FEATURES

WDI_TLV_OS_POWER_MANAGEMENT_FEATURES は、OS 電源管理機能のフラグを含む TLV です。 これにより、Ihv は、Nic の自動省電力 (NAPS) と呼ばれる高度な電源管理機能をサポートすることを OS に示すことができます。 NAPS は、ネットワークアクティビティがアイドル状態の場合に、ワイヤレスアダプターが*DX*に入ることを許可します。

## <a name="tlv-type"></a>TLV 型

0x144

## <a name="length"></a>長さ


次の値のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | [説明] |
| --- | --- |
| [**WDI_OS_POWER_MANAGEMENT_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_os_power_management_flags) | サポートされている NAPS 有効化シナリオを定義する**WDI_OS_POWER_MANAGEMENT_FLAGS**値のビットごとの or。 |
 

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1803

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Wditypes

