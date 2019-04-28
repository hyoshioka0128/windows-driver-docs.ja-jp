---
title: 事前解析データ
description: 事前解析データ
ms.assetid: 50ac2877-4c45-4d55-b5cc-013486892fbf
keywords:
- WDK を非表示に解析されたデータ
- WDK の HID preparsed データ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec1402e9c9deca3745b03476bb0eed4160ad7c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372960"
---
# <a name="preparsed-data"></a>事前解析データ





*データを preparsed*レポート記述子のデータに関連付けられている、[最上位のコレクション](top-level-collections.md)します。 アプリケーションのユーザー モードまたはカーネル モード ドライバーを取得し、デバイスの全体のレポート記述子を解釈するのにことがなく特定の HID コントロールに関する情報を抽出するのに preparsed データを使用します。 ユーザー モード アプリケーションを使用してコレクションの preparsed データを取得する[ **HidD\_GetPreparsedData** ](https://msdn.microsoft.com/library/windows/hardware/ff539679)カーネル モード ドライバーを使用して、 [ **IOCTL\_HID\_取得\_コレクション\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541089)要求。

次[HIDClass サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff538865)抽出し、ボタンをクリックし、値のデータの設定のサポートします。

[**HidP\_GetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539708)

[**HidP\_SetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539779)

[**HidP\_UnsetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539812)

[**HidP\_GetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539748)

[**HidP\_SetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539797)

[**HidP\_GetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539729)

[**HidP\_SetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539787)

[**HidP\_GetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539750)

[**HidP\_SetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539801)

 

 




