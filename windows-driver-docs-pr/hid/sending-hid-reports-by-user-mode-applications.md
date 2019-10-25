---
title: ユーザーモードアプリケーションによる HID レポートの送信
description: ユーザーモードアプリケーションによる HID レポートの送信
ms.assetid: 265d7393-62be-41ad-8f87-efcfa462de1f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c62e33ad40beef78a42724c9aad0781c3d855a92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841556"
---
# <a name="sending-hid-reports-by-user-mode-applications"></a>ユーザーモードアプリケーションによる HID レポートの送信


ユーザーモードアプリケーションでは、出力レポートを HID コレクションに継続的に送信するための主なアプローチとして、WriteFile (Microsoft Windows SDK で説明されているように) を使用する必要があります。 アプリケーションでは、**Hidd\_Set * * * Xxx*ルーチンを使用して、出力レポートと機能レポートをコレクションに送信することもできます。 ただし、アプリケーションでは、これらのルーチンを使用して、コレクションの現在の状態を設定するだけで済みます。 一部のデバイスでは、 **Hidd\_SetOutputReport**がサポートされていないため、このルーチンが使用されている場合は応答しなくなります。

詳細については、「 [WriteFile の使用](#using-writefile)」および「 [Hidd\_Setxxx ルーチンの使用](#using-hidd-setxxx-routines)」を参照してください。

### <a name="using-writefile"></a>WriteFile の使用

アプリケーションでは、書き込み要求を使用して、HID コレクションに出力レポートを送信する必要があります。 ユーザーモードアプリケーションが出力レポートを作成した後は、WriteFile を使用して、出力レポートをコレクションに送信できます。

### <a href="" id="using-hidd-setxxx-routines"></a>HidD\_SetXxx ルーチンの使用

アプリケーションでは、次の[HIDClass サポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用して、hid レポートを hid コレクションに送信できます。

<a href="" id="hidd-setoutputreport"></a>[**HidD\_SetOutputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setoutputreport)  
出力レポートを HID コレクションに送信します (Windows XP 以降のバージョン)。

<a href="" id="hidd-setfeature"></a>[**HidD\_SetFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setfeature)  
機能レポートを HID コレクションに送信します。

 

 




