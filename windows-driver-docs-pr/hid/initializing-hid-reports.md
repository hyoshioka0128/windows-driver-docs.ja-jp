---
title: HID レポートを初期化する
description: HID レポートを初期化する
ms.assetid: 14229315-3928-4421-a8d8-c3f7837bf1c3
keywords:
- HID WDK、レポートの初期化
- WDK を非表示にレポートの初期化
- レポートの初期化
- WDK を非表示コントロール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e208c7081894d72052c6ede979e1aba1c4b775cc
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716833"
---
# <a name="initializing-hid-reports"></a>HID レポートを初期化する





このセクションでは、どのユーザー モード アプリケーションとカーネル モード ドライバー、この HID レポートを使用する前に初期化について説明します、 [HIDClass サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)または HID クラス ドライバーの Ioctl します。

レポートのバッファーを初期化するためにアプリケーション、ドライバーはレポートの種類 (バイト) ゼロ初期化、必要なサイズのバッファーを作成します。 *Xxx*HID コレクションのメンバーを ReportByteLength [ **HIDP\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)構造体は、入力、出力、および機能のレポートに必要なサイズを指定します。 アプリケーションやドライバーを使用できるレポートのバッファーを初期化した後**HidP\_設定**_Xxx_ルーチンをレポートでデータの制御を設定します。 レポートの初回使用時、 **HidP\_設定**_Xxx_ルーチンでは、レポート ID を設定に関連付けられた、指定された 1 つに[HID usage](hid-usages.md)します。 レポート id に、互換性がない使用法を設定しようと、その後、アプリケーションまたはドライバーの場合、 **HidP\_設定**_Xxx_ HIDP の状態を返すルーチン\_状態\_互換性のない\_レポート\_id。

 

 




