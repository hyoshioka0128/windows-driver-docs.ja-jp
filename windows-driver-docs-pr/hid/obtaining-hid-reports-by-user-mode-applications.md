---
title: ユーザーモードアプリケーションによる HID レポートの取得
description: このトピックでは、ReadFile または HidD_GetXxx ルーチンを使用するユーザーモードアプリケーションによる、HID 入力レポートまたは HID 機能レポートの取得について説明します。
ms.assetid: 28f560dd-b919-4652-93f6-691051a0ffbe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ee38b45236cd9590fe66cef591b9d8b29dcf0d8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841567"
---
# <a name="obtaining-hid-reports-by-user-mode-applications"></a>ユーザーモードアプリケーションによる HID レポートの取得


このトピックでは、 [ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)または**Hidd\_Get**_Xxx_ルーチンを使用しているユーザーモードアプリケーションによる、hid 入力レポートまたは hid 機能レポートの取得について説明します。

ただし、アプリケーションでは、デバイスの現在の状態を取得するために、 **Hidd\_Get**_Xxx_ルーチンのみを使用する必要があります。 アプリケーションが[**Hidd\_GetInputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport)を使用して継続的に入力レポートを取得しようとすると、レポートが失われる可能性があります。 また、一部のデバイスでは、 **Hidd\_GetInputReport**がサポートされていない場合があり、このルーチンが使用されると、応答しなくなります。

以下のセクションで詳細を説明します。

### <a name="using-readfile"></a>ReadFile の使用

アプリケーションでは、CreateFile を使用して取得した open file ハンドルを使用して、コレクションでファイルを開きます。 アプリケーションが[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)を呼び出す場合は、 [HID クライアントドライバー](hid-client-drivers.md)がリングバッファー内のレポートをバッファーするため、重複する i/o を指定する必要はありません。 ただし、アプリケーションで重複 i/o を使用して、複数の未処理の読み取り要求を行うことができます。

### <a href="" id="using-hid-getxx-routines"></a>HidD\_GetXxx ルーチンの使用

アプリケーションでは、次の[HIDClass サポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用して、HID コレクションから最新の入力レポートと機能レポートを取得できます。

<a href="" id="hidd-getinputreport"></a>[**HidD\_GetInputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport)  
HID コレクションから入力レポートを返します (Windows XP 以降のバージョン)。

<a href="" id="hidd-getfeature"></a>[**HidD\_GetFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getfeature)  
HID コレクションから機能レポートを返します。

アプリケーションは、特定のレポートの返却を要求できます。 これらのルーチンを使用して特定のレポートを取得するために、アプリケーションはレポートの出力バッファーを割り当て、バッファーをゼロで初期化して、バッファーの最初のバイトを特定のレポート ID に設定します。 詳細については、「 [HID レポートの初期化](initializing-hid-reports.md)」を参照してください。

 

 




