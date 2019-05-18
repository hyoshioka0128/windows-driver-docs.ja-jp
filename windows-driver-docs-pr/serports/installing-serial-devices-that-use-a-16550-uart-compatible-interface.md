---
title: 16550 UART と互換性のあるインターフェイスを備えたシリアル デバイスをインストールします。
description: 16550 UART 互換インターフェイスを使用するシリアル デバイスをインストールする
ms.assetid: d80db651-b890-44dc-98ad-32e72e244d8c
keywords:
- シリアル ドライバー WDK、16550 UART と互換性のあるインターフェイス
- ユニバーサル非同期の受信側の送信機 WDK シリアル デバイス
- UART WDK シリアル デバイス
- 16550 UART と互換性のあるインターフェイス WDK シリアル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e335fb41be0169cd752d0fb924dc2cab3741c1bc
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836362"
---
# <a name="installing-serial-devices-that-use-a-16550-uart-compatible-interface"></a>16550 UART 互換インターフェイスを使用するシリアル デバイスをインストールする

低レベル デバイス フィルター ドライバーとしてシリアルを使用するプラグ アンド プレイ デバイスをインストールするには、次の操作を行います。

- デバイスの INF ファイルでの低レベル デバイス フィルター ドライバーとしてシリアルを指定するを参照してください--[フィルター ドライバーをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff547595)します。

- 設定、 **SerialSkipExternalNaming** 0 以外の値をデバイスのエントリの値を参照してください[プラグ アンド プレイ シリアル デバイス用のレジストリ設定](registry-settings-for-a-plug-and-play-serial-device.md)します。
