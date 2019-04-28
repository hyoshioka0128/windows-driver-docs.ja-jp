---
title: HID の新機能
description: このトピックでは、新機能とのヒューマン インターフェイス デバイス (HID) で Windows 10 の機能強化をまとめたものです。
Search.SourceType: Video
ms.assetid: AA8590B4-AAEA-4D41-972F-38149CE328E2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a267b4477edf11779e36af9533e0d1976e83de7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376718"
---
# <a name="whats-new-in-hid"></a>HID の新機能


このトピックでは、新機能とのヒューマン インターフェイス デバイス (HID) で Windows 10 の機能強化をまとめたものです。

## <a name="hid-winrt-api"></a>HID WinRT API


[Windows.Devices.HumanInterfaceDevice](https://msdn.microsoft.com/library/windows/apps/xaml/dn263140) API は、ヒューマン インターフェイス デバイス (HID) プロトコルをサポートする UWP アプリへのアクセスのデバイスを使用できます。

次の短いビデオでは、MSDN サンプル ギャラリーからダウンロードすることは HID、エンド ツー エンドのサンプル ソリューションをについて説明します。 (このソリューションには、新しい HID WinRT API を使用して作成されたサンプル アプリが含まれています)。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/2d4da9fc-c2ea-4933-949d-eb0cff3c9c4e]

## <a name="design-guide"></a>設計ガイド

[設計ガイド](index.md)を含めるいくつかの新しいトピックが更新されました。 既存のコンテンツが変更されている該当する場合、Windows 10 の HID サポートの強化を表示することも、します。 ここで、新規および更新されたトピックの一部を示します。

**新しいトピック**

-   [ACPI ボタン デバイス](acpi-button-device.md)

**更新されたトピック**

-   [HID トランスポート](hid-transports.md)

-   [HID ボタン ドライバー](buttons.md)

-   [Windows でサポートされる HID クライアント](hid-clients-supported-in-windows.md)

## <a name="hid-over-ic"></a>I²C 経由で非表示


最初に対象とヒューマン インターフェイス デバイスなどの HID プロトコル: キーボード、マウス、ジョイスティック。 もともとは、USB 経由で実行する開発されました。 Windows 8 では、Microsoft は、Inter-Integrated 回線 (I²C) バス経由で通信するためにデバイスを許可する新しい HID ミニポート ドライバーを作成します。

## <a name="related-topics"></a>関連トピック
[設計ガイド](index.md)  
[I2C 経由で非表示](hid-over-i2c-guide.md)  



