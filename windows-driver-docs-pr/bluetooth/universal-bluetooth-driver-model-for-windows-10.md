---
title: Windows 10 向けの Bluetooth ユニバーサル Windows ドライバー モデル
description: Windows 10 ですべてのデバイスの Bluetooth トランスポート ドライバー インターフェイスは集約し、ユニバーサル Windows ドライバー モデルを使用します。
ms.assetid: E65A71D3-C0D2-4E13-9E19-1E6C6C1A172E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eef5c6812ec27632b0c81dc3f09eb3c575d12c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364606"
---
# <a name="bluetooth-universal-windows-driver-model-for-windows-10"></a>Windows 10 向けの Bluetooth ユニバーサル Windows ドライバー モデル


Windows 10 ですべてのデバイスの Bluetooth トランスポート ドライバー インターフェイスは集約し、ユニバーサル Windows ドライバー モデルを使用します。 つまり、すべての Windows デバイス プラットフォームで動作する単一のドライバーを作成できます。

Bluetooth オーディオ ドライバーの表層部は Windows 10 用に分かれ、次の 2 つのオプションを選択できるようになっています。

-   デスクトップとモバイルの両方のデバイスに合った新しいオーディオ ユニバーサル Windows ドライバーを作成することができます。
-   既存の Windows Phone 8.1 Bluetooth オーディオ ドライバーは、Windows 10 Mobile でも動作します。

## <a name="span-idhowtowriteabluetoothuniversalwindowsdriverspanspan-idhowtowriteabluetoothuniversalwindowsdriverspanspan-idhowtowriteabluetoothuniversalwindowsdriverspanhow-to-write-a-bluetooth-universal-windows-driver"></a><span id="How_to_write_a_Bluetooth_Universal_Windows_driver"></span><span id="how_to_write_a_bluetooth_universal_windows_driver"></span><span id="HOW_TO_WRITE_A_BLUETOOTH_UNIVERSAL_WINDOWS_DRIVER"></span>Bluetooth のユニバーサル Windows ドライバーを作成する方法


Bluetooth のユニバーサル Windows ドライバーを作成するを参照してください[ユニバーサル Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers)、」の手順に従います*ユニバーサル Windows ドライバーをビルド*Universal を構築するには。カーネル モード ドライバー (KMDF) テンプレートを使用して Windows ドライバー。

次に、実装のガイダンスについては、Bluetooth デザインおよび参照セクションを参照してください。

-   [Bluetooth のプロファイルのドライバー](bluetooth-profile-drivers-overview.md)
-   [デバイスの Bluetooth のリファレンス](https://msdn.microsoft.com/library/windows/hardware/ff536585)

 

 





