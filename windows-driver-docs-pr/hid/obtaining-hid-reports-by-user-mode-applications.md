---
title: ユーザー モード アプリケーションでの HID レポートを取得します。
description: このトピックでは、ReadFile や HidD_GetXxx ルーチンを使用してユーザー モード アプリケーションが、HID 入力レポートまたは HID 機能のレポートの取得について説明します。
ms.assetid: 28f560dd-b919-4652-93f6-691051a0ffbe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3e718257c2cf5e14e71a8eed9dbfdb708223d218
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365454"
---
# <a name="obtaining-hid-reports-by-user-mode-applications"></a>ユーザー モード アプリケーションでの HID レポートを取得します。


このトピックでは、HID 入力レポートまたは HID 機能のレポートの取得を使用してユーザー モード アプリケーションで[ReadFile](https://msdn.microsoft.com/library/windows/desktop/aa365467.aspx)または **HidD\_取得 * * * Xxx*ルーチン。

ただし、アプリケーションで使用するだけ、**HidD\_取得 * * * Xxx*ルーチンは、デバイスの現在の状態を取得します。 アプリケーション使用を試みる場合[ **HidD\_GetInputReport** ](https://msdn.microsoft.com/library/windows/hardware/ff538945)入力のレポートを継続的に取得するレポートは削除できます。 さらに、一部のデバイスをサポート可能性がありますいない**HidD\_GetInputReport**、され、このルーチンを使用する場合に応答しなくなります。

次のセクションでは、詳細を提供します。

### <a name="using-readfile"></a>Readfile 関数を使用します。

アプリケーションが開いているファイル ハンドルを使用して、コレクションでファイルを開くに CreateFile を使用して取得にします。 アプリケーションを呼び出すと[ReadFile](https://msdn.microsoft.com/library/windows/desktop/aa365467.aspx)、ために、重複 I/O を指定することはありません、[クライアント ドライバーを非表示に](hid-client-drivers.md)リング バッファーにレポートをバッファーします。 ただし、アプリケーションでは、重複 I/O を使用して、未処理の 1 つ以上の読み取り要求があります。

### <a href="" id="using-hid-getxx-routines"></a>HidD を使用して\_GetXxx ルーチン

アプリケーションは、次を使用できます[HIDClass サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff538865)最新を取得するレポートと HID コレクションからのレポートの機能を入力します。

<a href="" id="hidd-getinputreport"></a>[**HidD\_GetInputReport**](https://msdn.microsoft.com/library/windows/hardware/ff538945)  
(Windows XP およびそれ以降のバージョン) は、HID コレクションから入力のレポートを返します。

<a href="" id="hidd-getfeature"></a>[**HidD\_GetFeature**](https://msdn.microsoft.com/library/windows/hardware/ff538910)  
HID コレクションから機能のレポートを返します。

アプリケーションでは、特定のレポートの戻り値を要求できます。 これらのルーチンを使用して特定のレポートを取得するには、アプリケーション レポートの出力バッファーを割り当て、バッファーを 0 に初期化および特定のレポート ID に、バッファー内の最初のバイトを設定 詳細については、次を参照してください。 [HID レポートの初期化](initializing-hid-reports.md)します。

 

 




