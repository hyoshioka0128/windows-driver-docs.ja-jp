---
title: HID トランスポートの概要
description: HID トランスポートの概要
ms.assetid: E442CB87-992B-475A-A97F-9C22468BA877
keywords:
- HID トランスポート
- USB トランスポート
- Bluetooth トランスポート
- Bluetooth
- Bluetooth LE
- I2C
- トランスポートミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc7dcd173b88e1af43462e8ee01ba116a82c890
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565585"
---
# <a name="hid-transport-overview"></a>HID トランスポートの概要


HID トランスポートは、現在と以前のバージョンの Windows でサポートされています。

| [トランスポート]    | インボックスミニドライバー | バージョン               |  メモ |
| ------------ | ----------------- | --------------------- | ---------- | 
| USB          | Hidusb .sys        | Windows 7 以降。  | Windows 2000 に戻る前に、Windows オペレーティングシステムで USB HID 1.11 + のサポートが提供されています。       |
| Bluetooth    | Hidbth. sys        | Windows 7 以降。  | Windows Vista 以降では、Windows オペレーティングシステムで Bluetooth HID 1.1 以降がサポートされています。 |
| Bluetooth LE | HidBthLE .dll      | Windows 8 以降。  | Windows 8 では、Bluetooth LE に対する HID のサポートが導入されています。                                               |
| I ² C          | Hidi2c        | Windows 8 以降。  | Windows 8 では、I2C に対する HID のサポートが導入されています。                                                        |
| GPIO         | Hidinterrupt .sys  | Windows 10 以降。 | Windows 10 では、汎用 i/o (GPIO) ボタンのサポートが導入されています。                         |

 

Microsoft では、可能な限り、前の表に記載されているトランスポートにインボックスドライバーを使用することをお勧めします。

デバイスで USB、Bluetooth、Bluetooth LE、I ² C 以外のトランスポートが必要な場合は、「 [Transport ミニドライバー](transport-minidrivers.md) 」トピックで説明されているミニポートドライバーを開発できます。

## <a name="hid-transport-limits"></a>HID トランスポートの制限


-   **レポート記述子の長さ**

    トランスポートミニドライバーは、 [**HID\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidport/ns-hidport-_hid_descriptor)構造内の Hidclass にレポート記述子を送信します。 HID レポート記述子をデバイスに転送するためにトランスポートプロトコルによって定義されるサイズに関係なく、実際のレポート記述子のサイズは Hidclass と HID ミニドライバー間の通信中に制限されます。

-   **レポート記述子での TLCs**

    Hidclass/Hidparse ドライバーペアは、レポート記述子に含まれる TLCs の数を認識します。 HID ミニポートドライバーでは、その情報は認識されません。 各 TLC は、コレクションを開始するために少なくとも2バイト、コレクションを終了するために1バイトを持ちます。

-   **入力/出力/機能レポートの長さ**

    Hidclass/Hidparse ドライバーペアは、HID 入力、出力、および機能レポートの長さを定義します。 制限は 8 KB (-1 ビット) です。 HID ミニドライバーがレポートに対して 8 KB を超える転送を要求できる場合でも、8 KB より小さいレポートのみが正常に転送されます。

| インボックスミニドライバー | レポート記述子の長さ | 1つのレポート記述子での TLCs | 入力/出力/機能レポートの長さ |
| ----------------- | ------------------------ | ----------------------------- | ---------------------------------- |
| Hidclass/Hidparse | 65535バイト              | 21845                         | 8 KB-1 ビット                       |
| Hidusb            | 65535バイト              | なし                           | 64 KB                              |
| Hidbth            | 65535バイト              | なし                           | 64 KB                              |
| HidBthLE          | 65535バイト              | なし                           | 64 KB                              |
| Hidi2c            | 65535バイト              | なし                           | 64 KB                              |

 

 

 




