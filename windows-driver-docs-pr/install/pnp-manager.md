---
title: プラグアンドプレイマネージャー
description: プラグアンドプレイマネージャー
ms.assetid: b1890b3c-fc7b-4a2e-b48a-8266f237c9b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fdd2151ae2d6027730d3546aff06a8b714df118
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837381"
---
# <a name="plug-and-play-manager"></a>プラグアンドプレイマネージャー


プラグアンドプレイ (PnP) マネージャーは、Windows の PnP 機能のサポートを提供し、次の PnP 関連のタスクを担当します。

-   システムの起動中のデバイスの検出と列挙

-   システムの実行中にデバイスを追加または削除する

カーネルモードの PnP マネージャーは、新しいデバイスがシステムに存在すること、およびインストールされている必要があることをユーザーモードの PnP マネージャーに通知します。

また、カーネルモードの PnP マネージャーは、デバイスのドライバーの[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンと[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出し、デバイスを起動する[**IRP_MN_START_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求を送信します。

PnP マネージャーは、システム内のデバイスを追跡する[デバイスツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)を保持します。 デバイスツリーには、システム上に存在するデバイスに関する情報が含まれています。 コンピューターの起動時に、PnP マネージャーはドライバーやその他のコンポーネントからの情報を使用してこのツリーを構築し、デバイスの追加または削除に応じてツリーを更新します。

 

 





