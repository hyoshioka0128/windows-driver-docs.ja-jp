---
title: フィルター ドライバーでのデバイス オブジェクトの作成
description: フィルター ドライバーでのデバイス オブジェクトの作成
ms.assetid: f5a4851d-7caf-467d-9500-11f341fdf680
keywords:
- PnP WDK KMDF、フィルター ドライバー
- プラグ アンド プレイ WDK KMDF、フィルター ドライバー
- 電源管理 WDK KMDF、フィルター ドライバー
- フィルター ドライバー WDK KMDF
- DOs WDK KMDF をフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 587ff9cab9b7ff1f2bb6dfa7990c365245fe7c91
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581547"
---
# <a name="creating-device-objects-in-a-filter-driver"></a>フィルター ドライバーでのデバイス オブジェクトの作成


各[フィルター ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff545890)システム上に存在する、サポートされているデバイスの各フレームワーク デバイス オブジェクトを作成します。 フィルター ドライバーでは、これらのデバイス オブジェクトが作成される、ため、デバイス オブジェクトをフィルター (フィルター DOs) が呼び出されます。 デバイスのフィルター ドライバーの表現は、各フィルター操作を行います。

フィルター関数のドライバーのように、ドライバー、提供、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)を識別するハンドルを受け取るコールバック関数を[ **WDFDEVICE\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体。 ドライバーは、同じセットを呼び出すことができます[framework デバイス オブジェクトの初期化メソッド](https://msdn.microsoft.com/library/windows/hardware/dn265631#device-init-methods)、WDFDEVICE で情報を格納するドライバー呼び出し関数を\_INIT 構造体。 関数のドライバーのようなフィルター ドライバーを呼び出すことも[framework FDO 初期化メソッド](https://msdn.microsoft.com/library/windows/hardware/dn265631#fdo-init-methods)します。

フィルター ドライバーの数が少ないは列挙子のソフトウェア専用デバイスです。 このようなフィルター ドライバーが呼び出せる[framework PDO 初期化メソッド](https://msdn.microsoft.com/library/windows/hardware/dn265631#pdo-init-methods)します。

フィルター ドライバーを呼び出す必要があります[ **WdfFdoInitSetFilter**](https://msdn.microsoft.com/library/windows/hardware/ff547273)します。

デバイス オブジェクトを作成する最後の手順を呼び出すことです。 [ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)します。

 

 





