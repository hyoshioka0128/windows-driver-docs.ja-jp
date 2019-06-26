---
title: 事前解析データ
description: 事前解析データ
ms.assetid: 50ac2877-4c45-4d55-b5cc-013486892fbf
keywords:
- WDK を非表示に解析されたデータ
- WDK の HID preparsed データ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4371d61c2cfb523993b7f7c1855780d1a5a03bc9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385820"
---
# <a name="preparsed-data"></a>事前解析データ





*データを preparsed*レポート記述子のデータに関連付けられている、[最上位のコレクション](top-level-collections.md)します。 アプリケーションのユーザー モードまたはカーネル モード ドライバーを取得し、デバイスの全体のレポート記述子を解釈するのにことがなく特定の HID コントロールに関する情報を抽出するのに preparsed データを使用します。 ユーザー モード アプリケーションを使用してコレクションの preparsed データを取得する[ **HidD\_GetPreparsedData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidsdi/nf-hidsdi-hidd_getpreparseddata)カーネル モード ドライバーを使用して、 [ **IOCTL\_HID\_取得\_コレクション\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidclass/ni-hidclass-ioctl_hid_get_collection_descriptor)要求。

次[HIDClass サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)抽出し、ボタンをクリックし、値のデータの設定のサポートします。

[**HidP\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_SetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_UnsetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_GetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagevalue)

[**HidP\_SetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusagevalue)

[**HidP\_GetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getscaledusagevalue)

[**HidP\_SetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setscaledusagevalue)

[**HidP\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagevaluearray)

[**HidP\_SetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusagevaluearray)

 

 




