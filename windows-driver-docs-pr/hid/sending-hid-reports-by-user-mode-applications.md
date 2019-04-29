---
title: ユーザー モード アプリケーションでの HID レポートを送信します。
description: ユーザー モード アプリケーションでの HID レポートを送信します。
ms.assetid: 265d7393-62be-41ad-8f87-efcfa462de1f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fc130997ee844e70ab5e11268820ed60b649c6ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384453"
---
# <a name="sending-hid-reports-by-user-mode-applications"></a>ユーザー モード アプリケーションでの HID レポートを送信します。


ユーザー モード アプリケーションが WriteFile (に従って使用、Microsoft Windows SDK) の主なアプローチとして HID コレクションに出力レポートを継続的に送信します。 アプリケーションでも使用できます **HidD\_設定 * * * Xxx*出力レポートを送信し、機能のコレクションにレポートするためのルーチンです。 ただし、アプリケーションでは、コレクションの現在の状態を設定するのにこれらのルーチンが使用するだけです。 一部のデバイスをサポートしていない**HidD\_SetOutputReport**され、このルーチンを使用する場合に応答しなくなります。

詳細については、次を参照してください。[を使用して WriteFile](#using-writefile)と[を使用して HidD\_SetXxx ルーチン](#using-hidd-setxxx-routines)します。

### <a name="using-writefile"></a>WriteFile を使用します。

アプリケーションは、書き込み要求を使用して、HID コレクションに出力レポートを送信する必要があります。 ユーザー モード アプリケーションには、レポートの出力が作成、WriteFile を使用してコレクションに出力レポートを送信できます。

### <a href="" id="using-hidd-setxxx-routines"></a>HidD を使用して\_SetXxx ルーチン

アプリケーションは、次を使用できます[HIDClass サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff538865)HID レポート HID コレクションを送信します。

<a href="" id="hidd-setoutputreport"></a>[**HidD\_SetOutputReport**](https://msdn.microsoft.com/library/windows/hardware/ff539690)  
HID のコレクション (Windows XP およびそれ以降のバージョン) を出力レポートを送信します。

<a href="" id="hidd-setfeature"></a>[**HidD\_SetFeature**](https://msdn.microsoft.com/library/windows/hardware/ff539684)  
HID コレクションには、機能のレポートを送信します。

 

 




