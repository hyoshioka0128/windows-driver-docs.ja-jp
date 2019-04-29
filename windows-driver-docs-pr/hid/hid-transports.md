---
title: HID トランスポート
description: HID トランスポート
ms.assetid: E442CB87-992B-475A-A97F-9C22468BA877
keywords:
- HID トランスポート
- USB トランスポート
- Bluetooth のトランスポート
- Bluetooth
- Bluetooth LE
- I2C
- トランスポート ミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83f89c9240993851680fa20d755447edbc3b0a00
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388787"
---
# <a name="hid-transports"></a>HID トランスポート


HID トランスポートが Windows の現在と以前のバージョンでサポートされています。

| [トランスポート]    | インボックス ミニドライバー | バージョン               |  メモ |
| ------------ | ----------------- | --------------------- | ---------- | 
| USB          | Hidusb.sys        | Windows 7 以降。  | USB HID 1.11 + のサポートは、Windows 2000 年代の Windows オペレーティング システムで提供されます。       |
| Bluetooth    | Hidbth.sys        | Windows 7 以降。  | Bluetooth HID 1.1 + のサポートは、Windows Vista までさかのぼる Windows オペレーティング システムで提供されます。 |
| Bluetooth LE | HidBthLE.dll      | Windows 8 以降。  | Windows 8 では、Bluetooth LE 経由での HID サポートが導入されています。                                               |
| I²C          | Hidi2c.sys        | Windows 8 以降。  | Windows 8 では、I2C 経由での HID サポートが導入されています。                                                        |
| GPIO         | Hidinterrupt.sys  | Windows 10 以降。 | Windows 10 の Windows には、汎用の I/O (GPIO) ボタンのサポートが導入されています。                         |

 

マイクロソフトを可能であれば、上記の表に示したトランスポート インボックス ドライバーを使用して推奨します。

説明されているミニポート ドライバーを開発するには、デバイスは、USB、Bluetooth、Bluetooth LE、I²C 以外のトランスポートを必要とする場合、[トランスポート ミニドライバー](transport-minidrivers.md)トピック

## <a name="hid-transport-limits"></a>HID のトランスポートの制限


-   **レポート記述子の長さ**

    トランスポート ミニドライバーで Hidclass へのレポート記述子の送信、 [ **HID\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539885)構造体。 自分のデバイスでの HID レポート記述子を転送するためのトランスポート プロトコルによって定義されたサイズに関係なく、実際のレポート記述子のサイズは Hidclass と HID ミニドライバーの間の通信中に制限されます。

-   **レポート記述子 TLCs**

    Hidclass Hidparse/ドライバーのペアは TLCs レポート記述子の数に注意してください。 HID のミニポート ドライバーには、その情報がわかりません。 各 TLC では、コレクションとコレクションを終了する 1 バイトを開始するには少なくとも 2 バイトを持ちます。

-   **入力/出力/機能をレポートの長さ**

    Hidclass Hidparse/ドライバーのペアは、非表示の入力、出力、および機能のレポートの長さを定義します。 (マイナス 1 ビット) は 8 KB を制限します。 場合でも、HID ミニドライバーは、レポートの複数の 8 KB の転送を要求できます、8 KB 未満のレポートのみが正常に転送されます。

| インボックス ミニドライバー | レポート記述子の長さ | 1 つのレポート記述子 TLCs | 入力/出力/機能をレポートの長さ |
| ----------------- | ------------------------ | ----------------------------- | ---------------------------------- |
| Hidclass/Hidparse | サイズが 65535 バイト              | 21845                         | 8 KB の 1 ビット                       |
| Hidusb            | サイズが 65535 バイト              | なし                           | 64 KB                              |
| Hidbth            | サイズが 65535 バイト              | なし                           | 64 KB                              |
| HidBthLE          | サイズが 65535 バイト              | なし                           | 64 KB                              |
| Hidi2c            | サイズが 65535 バイト              | なし                           | 64 KB                              |

 

 

 




