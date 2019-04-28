---
title: 高パフォーマンスのバスとアダプターに関するデバイスの状態
description: 高パフォーマンスのバスとアダプターに関するデバイスの状態
ms.assetid: 7a6b8048-d9aa-4169-aac5-150dc805f61b
keywords:
- Storport ドライバー WDK、エラー
- WDK Storport のエラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10dbf15b1c58d58ed773837b02d682966a02deeb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365286"
---
# <a name="device-status-for-high-performance-buses-and-adapters"></a>高パフォーマンスのバスとアダプターに関するデバイスの状態


## <span id="ddk_device_status_for_high_performance_buses_and_adapters_kg"></span><span id="DDK_DEVICE_STATUS_FOR_HIGH_PERFORMANCE_BUSES_AND_ADAPTERS_KG"></span>


Storport ドライバーは、いくつかのトランスポート固有のエラーおよび SCSI ポート ドライバーが報告しない条件を報告する設計されています。 たとえば、Storport は、ファイバー チャネル ホスト バス アダプター (HBA) の間の接続が失われたか、通知の送信を停止すると HBA ファイバー チャネルの「リンクがダウンした」エラーなどのファイバー チャネルで発生するエラー状態を報告します。 Storport サポートするファイバー チャネルのリンク サービスを拡張し、登録済みの状態を報告できる変更の通知 (RSCNs) およびファイバー チャネルのループの初期化のプロトコル (LIP) に関連付けられたエラー。

 

 




