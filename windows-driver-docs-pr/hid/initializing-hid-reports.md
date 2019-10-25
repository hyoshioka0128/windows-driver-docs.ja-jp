---
title: HID レポートを初期化する
description: HID レポートを初期化する
ms.assetid: 14229315-3928-4421-a8d8-c3f7837bf1c3
keywords:
- HID レポート WDK, 初期化
- WDK HID をレポートし、初期化します。
- レポートの初期化
- WDK HID を制御します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33d5ec11b0545ec914cbb7a42f7ff5bf7d4ec6e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841582"
---
# <a name="initializing-hid-reports"></a>HID レポートを初期化する





このセクションでは、 [HIDClass サポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)または hid クラスドライバーの ioctl を使用する前に、ユーザーモードアプリケーションとカーネルモードドライバーが hid レポートを初期化する方法について説明します。

レポートバッファーを初期化するために、アプリケーションまたはドライバーによって、レポートの種類に必要なサイズ (バイト単位) のゼロ初期化バッファーが作成されます。 HID コレクションの[**Hidp\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)構造体の*Xxx*ReportByteLength メンバーは、入力、出力、および機能レポートの必要なサイズを指定します。 レポートバッファーを初期化した後、アプリケーションまたはドライバーは、 **Hidp\_set**_Xxx_ルーチンを使用して、レポートにコントロールデータを設定できます。 レポートを初めて使用するとき、 **Hidp\_set**_Xxx_ルーチンは、指定された[HID 使用法](hid-usages.md)に関連付けられているレポート ID にレポート ID を設定します。 その後、アプリケーションまたはドライバーが、レポート ID と互換性のない使用状況を設定しようとすると、 **hidp\_set**_Xxx_ルーチンは、状態が "hidp\_ステータス\_互換性のない\_レポート\_ID に返されます。

 

 




