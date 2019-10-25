---
title: 事前解析データ
description: 事前解析データ
ms.assetid: 50ac2877-4c45-4d55-b5cc-013486892fbf
keywords:
- 解析されたデータ WDK HID
- preparsed data WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b578e7c443fc7b1c73f6369ff73c75f7e5a08868
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841562"
---
# <a name="preparsed-data"></a>事前解析データ





*Preparsed data*は、[最上位レベルのコレクション](top-level-collections.md)に関連付けられたレポート記述子データです。 ユーザーモードアプリケーションまたはカーネルモードドライバーは、preparsed データを使用して、特定の HID コントロールに関する情報を抽出します。その際、デバイスのレポート記述子全体を取得して解釈する必要はありません。 ユーザーモードアプリケーションは、 [**Hidd\_GetPreparsedData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata)を使用してコレクションの preparsed データを取得します。また、カーネルモードドライバーは、 [**IOCTL\_HID\_GET\_collection\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_collection_descriptor)要求を使用します。

次の[HIDClass サポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)では、ボタンと値のデータの抽出と設定がサポートされています。

[**HidP\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_SetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_UnsetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_Getの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)

[**HidP\_Setの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)

[**HidP\_Get/Edの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)

[**HidP\_Setスケール Edの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue)

[**HidP\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)

[**HidP\_SetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray)

 

 




