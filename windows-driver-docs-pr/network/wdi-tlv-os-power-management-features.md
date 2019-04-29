---
title: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES
description: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES では、OS の電源管理機能のフラグを含む TLV です。
ms.assetid: 4F104956-1B26-47DF-A58F-53C24B75DB77
ms.date: 03/30/2018
keywords:
- WDI_TLV_OS_POWER_MANAGEMENT_FEATURES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5fdf117dc5ee231a7bf17e2ef2f2e2dd179ceed2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385253"
---
# <a name="wditlvospowermanagementfeatures"></a>WDI_TLV_OS_POWER_MANAGEMENT_FEATURES

WDI_TLV_OS_POWER_MANAGEMENT_FEATURES では、OS の電源管理機能のフラグを含む TLV です。 これにより、Ihv Nic 自動 Power セーバー (NAP) と呼ばれる高度な電源管理機能をサポートしている OS に示すためにできます。 NAP により、ワイヤレス アダプターを入力する*DX*ネットワーク アクティビティがアイドル状態の場合。

## <a name="tlv-type"></a>TLV 型

0x144

## <a name="length"></a>長さ


次の値のバイト単位でサイズ。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| [**WDI_OS_POWER_MANAGEMENT_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_os_power_management_flags) | ビットごとの OR **WDI_OS_POWER_MANAGEMENT_FLAGS**値を定義するには、NAP の有効化のシナリオがサポートされています。 |
 

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1803 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
