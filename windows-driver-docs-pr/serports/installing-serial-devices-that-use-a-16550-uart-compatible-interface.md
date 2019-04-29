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
ms.openlocfilehash: aa98a5ba8cce978138a7065463ab199e7a46f960
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331149"
---
# <a name="installing-serial-devices-that-use-a-16550-uart-compatible-interface"></a>16550 UART 互換インターフェイスを使用するシリアル デバイスをインストールする





低レベル デバイス フィルター ドライバーとしてシリアルを使用するプラグ アンド プレイ デバイスをインストールするには、次の操作を行います。

-   デバイスの INF ファイルでの低レベル デバイス フィルター ドライバーとしてシリアルを指定するを参照してください--[フィルター ドライバーをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff547595)します。

-   設定、 **SerialSkipExternalNaming** 0 以外の値をデバイスのエントリの値を参照してください[プラグ アンド プレイ シリアル デバイス用のレジストリ設定](registry-settings-for-a-plug-and-play-serial-device.md)します。

 

 




