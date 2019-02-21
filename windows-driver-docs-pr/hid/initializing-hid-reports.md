---
title: 初期化の HID レポート
description: 初期化の HID レポート
ms.assetid: 14229315-3928-4421-a8d8-c3f7837bf1c3
keywords:
- HID WDK、レポートの初期化
- WDK を非表示にレポートの初期化
- レポートの初期化
- WDK を非表示コントロール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37f424e6fab021ced41e0bf829be151ebf43ccb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558990"
---
# <a name="initializing-hid-reports"></a>初期化の HID レポート





このセクションでは、どのユーザー モード アプリケーションとカーネル モード ドライバー、この HID レポートを使用する前に初期化について説明します、 [HIDClass サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff538865)または HID クラス ドライバーの Ioctl します。

レポートのバッファーを初期化するためにアプリケーション、ドライバーはレポートの種類 (バイト) ゼロ初期化、必要なサイズのバッファーを作成します。 *Xxx*HID コレクションのメンバーを ReportByteLength [ **HIDP\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff539697)構造体は、入力、出力、および機能のレポートに必要なサイズを指定します。 アプリケーションやドライバーを使用できるレポートのバッファーを初期化した後 **HidP\_設定 * * * Xxx*ルーチンをレポートでデータの制御を設定します。 レポートの初回使用時、**HidP\_設定 * * * Xxx*ルーチンでは、レポート ID を設定に関連付けられた、指定された 1 つに[HID usage](hid-usages.md)します。 レポート id に、互換性がない使用法を設定しようと、その後、アプリケーションまたはドライバーの場合、**HidP\_設定 * * * Xxx* HIDP の状態を返すルーチン\_状態\_互換性のないです。\_レポート\_id。

 

 




