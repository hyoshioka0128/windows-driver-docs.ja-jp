---
title: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES
description: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES は、OS 電源管理機能のフラグを含む TLV です。
ms.assetid: 4F104956-1B26-47DF-A58F-53C24B75DB77
ms.date: 03/30/2018
keywords:
- WDI_TLV_OS_POWER_MANAGEMENT_FEATURES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: b5bb2af3ba5af3856fba8ba58f031c29dfa544a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824374"
---
# <a name="wdi_tlv_os_power_management_features"></a>WDI_TLV_OS_POWER_MANAGEMENT_FEATURES

WDI_TLV_OS_POWER_MANAGEMENT_FEATURES は、OS 電源管理機能のフラグを含む TLV です。 これにより、Ihv は、Nic の自動省電力 (NAPS) と呼ばれる高度な電源管理機能をサポートすることを OS に示すことができます。 NAPS は、ネットワークアクティビティがアイドル状態の場合に、ワイヤレスアダプターが*DX*に入ることを許可します。

## <a name="tlv-type"></a>TLV 型

0x144

## <a name="length"></a>長さ


次の値のサイズ (バイト単位)。

## <a name="values"></a>値

| タスクバーの検索ボックスに | 説明 |
| --- | --- |
| [**WDI_OS_POWER_MANAGEMENT_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_os_power_management_flags) | サポートされている NAPS 有効化シナリオを定義する**WDI_OS_POWER_MANAGEMENT_FLAGS**値のビットごとの or。 |
 

## <a name="requirements"></a>要件

| | |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1803 |
| サポートされている最小のサーバー | WIN ENT LTSB 2016 Estonian 64 Bits |
| Header | Wditypes |
