---
title: フレームワーク オブジェクトのプロパティ
description: フレームワーク オブジェクトのプロパティ
ms.assetid: d95a7f51-fe22-4cd6-8c46-6d571f7d9169
keywords:
- framework オブジェクト WDK KMDF、プロパティ
- WDK KMDF のプロパティ
- get WDK KMDF メソッド
- WDK KMDF の set メソッド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0903785c1f69c7e1bcfd97369c2802538bff96c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384447"
---
# <a name="framework-object-properties"></a>フレームワーク オブジェクトのプロパティ





ほとんどのフレームワーク オブジェクトには、プロパティのセットが含まれます。 プロパティは、ドライバーを使用できる情報を表します。 ドライバーの観点からいくつかのプロパティは読み取り専用と読み取り/書き込みをいくつか。

"Get"を定義するために、フレームワーク、読み取り可能な各プロパティの[メソッド](framework-object-methods.md)ドライバーは、プロパティの値を取得する呼び出すことができます。 各"get"メソッドでは、プロパティの現在の値を返します。

書き込み可能の各プロパティは、フレームワークは、ドライバーを呼び出すことができるプロパティの値を変更する「設定」のメソッドを定義します。 ドライバーは、"set"メソッドへの入力パラメーターとして、プロパティの新しい値を提供します。

たとえば、フレームワークのデバイス オブジェクトは 2 つのメソッドを定義します[ **WdfDeviceGetDeviceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestate)と[ **WdfDeviceSetDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)、。プラグ アンド プレイ (PnP) の状態のドライバーは、デバイスの設定を取得または呼び出すことができます。

 

 





