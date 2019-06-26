---
title: Windows でサポートされる HID トランスポート
description: Windows では、次のトランスポートがサポートされます。
ms.assetid: 03B66788-A930-4C18-A019-CA906634DC4C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a01c8ce049970aa1dfd524be3b826aff7076084
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363560"
---
# <a name="hid-transports-supported-in-windows"></a>Windows でサポートされる HID トランスポート


Windows では、次のトランスポートがサポートされます。

| [トランスポート]    | Windows 7 | Windows 8 | メモ                                                                                                 |
|--------------|-----------|-----------|-------------------------------------------------------------------------------------------------------|
| USB          | 〇       | 〇       | USB HID 1.11 + のサポートは、Windows 2000 年代の Windows オペレーティング システムで提供されます。       |
| Bluetooth    | 〇       | 〇       | Bluetooth HID 1.1 + のサポートは、Windows Vista までさかのぼる Windows オペレーティング システムで提供されます。 |
| Bluetooth LE | X        | 〇       | Windows 8 では、Bluetooth LE 経由での HID サポートが導入されています。                                               |
| I2C          | X        | 〇       | Windows 8 の I2C 経由での HID サポートが導入されています                                                         |

 

(Windows 7) より前の Windows の以前のバージョンには、次のサポートも含まれています。

-   HidGame.sys - HID ミニドライバー ゲーム ポート (I/O ポート 201) デバイス。 HID クラス ドライバーは、ゲーム ポートのデバイスの機能のデバイス オブジェクト (FDO) を作成し、ゲーム ポート デバイスをサポートする HID コレクションごとに物理デバイス オブジェクト (PDO) を作成します。
-   Gameenum.sys – ゲーム ポート バス ドライバー。 ゲーム ポート バス ドライバーでは、デイジー チェーン接続ゲーム ポートには、各ゲーム ポート デバイスの PDO を作成します。

今すぐと見なされるレガシ (USB とその他の最新のトランスポートによって置換される) 先進のコンピューターで、ハードウェアが見つかりません。

## <a name="recommended-transports-for-keyboards-mice-and-touchpads"></a>キーボード、マウス、およびタッチパッドの推奨されるトランスポート


次の表は、(ラップトップとスレート) などのポータブルおよび (すべて 1 つとデスクトップ) などのポータブルでないシステムで、キーボード、マウス、およびタッチパッドのデバイスの推奨されるトランスポートを示します。

| システムの種類                  | 移植性があります。                                 | 非ポータブル                                |
|------------------------------|------------------------------------------|---------------------------------------------|
| レガシ システム               | 内部:Ps/2、外部:Bluetooth、USB | 内部:該当なし、外部:Bluetooth、USB     |
| チップ (SoC) システム上のシステム | 内部:I2C、外部:Bluetooth、USB  | 内部:I2C、USB 外部:Bluetooth、USB |

 

[**USB 汎用 HID テスト**](https://docs.microsoft.com/windows-hardware/test/hlk/testref/f7949ab5-dd13-4c74-876f-6d54ff85e213) HidUsb と HidClass ドライバーが Windows ハードウェア ラボ キット (HLK) にについて説明します。 サード パーティ製の HID ミニ ドライバー HLK テストはありません。 
 




