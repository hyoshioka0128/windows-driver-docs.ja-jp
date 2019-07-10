---
title: ユーザー モード アプリケーションでの HID レポートを取得します。
description: このトピックでは、ReadFile や HidD_GetXxx ルーチンを使用してユーザー モード アプリケーションが、HID 入力レポートまたは HID 機能のレポートの取得について説明します。
ms.assetid: 28f560dd-b919-4652-93f6-691051a0ffbe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0bfa1bfc3766a4122850ea91326c175ae114a6d9
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716808"
---
# <a name="obtaining-hid-reports-by-user-mode-applications"></a>ユーザー モード アプリケーションでの HID レポートを取得します。


このトピックでは、HID 入力レポートまたは HID 機能のレポートの取得を使用してユーザー モード アプリケーションで[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)または**HidD\_取得**_Xxx_ルーチン。

ただし、アプリケーションで使用するだけ、 **HidD\_取得**_Xxx_ルーチンは、デバイスの現在の状態を取得します。 アプリケーション使用を試みる場合[ **HidD\_GetInputReport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidsdi/nf-hidsdi-hidd_getinputreport)入力のレポートを継続的に取得するレポートは削除できます。 さらに、一部のデバイスをサポート可能性がありますいない**HidD\_GetInputReport**、され、このルーチンを使用する場合に応答しなくなります。

次のセクションでは、詳細を提供します。

### <a name="using-readfile"></a>Readfile 関数を使用します。

アプリケーションが開いているファイル ハンドルを使用して、コレクションでファイルを開くに CreateFile を使用して取得にします。 アプリケーションを呼び出すと[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)、ために、重複 I/O を指定することはありません、[クライアント ドライバーを非表示に](hid-client-drivers.md)リング バッファーにレポートをバッファーします。 ただし、アプリケーションでは、重複 I/O を使用して、未処理の 1 つ以上の読み取り要求があります。

### <a href="" id="using-hid-getxx-routines"></a>HidD を使用して\_GetXxx ルーチン

アプリケーションは、次を使用できます[HIDClass サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)最新を取得するレポートと HID コレクションからのレポートの機能を入力します。

<a href="" id="hidd-getinputreport"></a>[**HidD\_GetInputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidsdi/nf-hidsdi-hidd_getinputreport)  
(Windows XP およびそれ以降のバージョン) は、HID コレクションから入力のレポートを返します。

<a href="" id="hidd-getfeature"></a>[**HidD\_GetFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidsdi/nf-hidsdi-hidd_getfeature)  
HID コレクションから機能のレポートを返します。

アプリケーションでは、特定のレポートの戻り値を要求できます。 これらのルーチンを使用して特定のレポートを取得するには、アプリケーション レポートの出力バッファーを割り当て、バッファーを 0 に初期化および特定のレポート ID に、バッファー内の最初のバイトを設定 詳細については、次を参照してください。 [HID レポートの初期化](initializing-hid-reports.md)します。

 

 




