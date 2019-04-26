---
title: フィルター ドライバーのコントロール デバイス オブジェクト
description: フィルター ドライバーのコントロール デバイス オブジェクト
ms.assetid: ac49b5d0-110d-4e47-814b-05f59791de41
keywords:
- デバイス オブジェクトの WDK ファイル システムを制御します。
- CDOs WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f93fe614dc97a10f571e7eb443415312c190135e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344326"
---
# <a name="the-filter-drivers-control-device-object"></a>フィルター ドライバーのコントロール デバイス オブジェクト


## <span id="ddk_the_filter_drivers_control_device_object_if"></span><span id="DDK_THE_FILTER_DRIVERS_CONTROL_DEVICE_OBJECT_IF"></span>


作成し、名前付きコントロール デバイス オブジェクト (CDO) を使用する必要は、ファイル システムとは異なり、ファイル システム フィルター ドライバーは、CDO させる必要はありません。 場合は、この CDO では、必要に応じて名前を指定できますは、システムに、フィルター ドライバーを表します。 役割、ユーザー モード アプリケーションからの I/O 要求を受信することです (または頻度の低い別のカーネル モード ドライバー)、およびを適切に行うことです。

ほとんどのファイル システム フィルター ドライバーは、作成し、CDO を使用します。 ただし、CDO の I/O 要求のサポートは、省略可能です。 フィルター ドライバーを呼び出すときに、このサポートを提供する[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397) CDO を作成するには、オブジェクトのデバイス名を指定にする必要があります。 ユーザー モード アプリケーションが呼び出すことで名前付き CDO を識別するハンドルを取得しできます[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)デバイス名のユーザー モードのバージョンを指定します。

たとえば、仮想的な"MyLegacyFilter"カーネル モード ドライバーを検討してください。 このドライバーは、名前を持つ、CDO を作成できます。

```cpp
\Device\MyLegacyFilter
```

呼び出しと[ **IoCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff549043)同等のユーザー モード表示名にこの名前をリンクします。 これは、MyLegacyFilter のユーザー モード アプリケーションが、名前を指定することによって、カーネル モード ドライバーの CDO を識別するハンドルを開けるようにします。

```cpp
\\.\MyLegacyFilter
```

呼び出し時に[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)します。

### <a name="span-idtypesofiorequeststhataresenttothefilterdriverscontroldevspanspan-idtypesofiorequeststhataresenttothefilterdriverscontroldevspantypes-of-io-requests-that-are-sent-to-the-filter-drivers-control-device-object"></a><span id="types_of_i_o_requests_that_are_sent_to_the_filter_driver_s_control_dev"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_THE_FILTER_DRIVER_S_CONTROL_DEV"></span>フィルター ドライバーの制御デバイス オブジェクトに送信される I/O 要求の種類

ファイル システム フィルター ドライバーは、制御デバイス オブジェクト (CDO) で I/O 操作をサポートする必要はありません。 ただし、ほとんどのフィルターは、次の種類のフィルターの CDO への送信 I/O 要求を許可します。

-   [**IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630) (対象のデバイス オブジェクトを識別するハンドルを開いて、ユーザー アプリケーションにそのハンドルを提供する)

-   [**IRP\_MJ\_クリーンアップ**](https://msdn.microsoft.com/library/windows/hardware/ff548608) (ハンドルを閉じることをユーザー モード アプリケーションのターゲット デバイス オブジェクトを)

-   [**IRP\_MJ\_閉じます**](https://msdn.microsoft.com/library/windows/hardware/ff548621) (を対象のデバイス オブジェクトの最後の残り開いているハンドルを閉じる)

-   [**IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff548649)、 [ **IRP\_MJ\_ファイル\_システム\_コントロール** ](https://msdn.microsoft.com/library/windows/hardware/ff548670)、または**FastIoDeviceControl** (または送信するプライベート Ioctl FSCTLs フィルター ドライバー)

すべての他のデバイス オブジェクト、ファイル システム フィルター ドライバーを作成するとは異なり、CDO にアタッチされていないドライバー スタックに注意してください。 フィルター ドライバーの CDO より上または下のデバイス オブジェクトはされていません。 そのため、受け取ったすべての I/O 要求の CDO と想定できる唯一の目的の受信者であります。 デバイス オブジェクトをフィルターまたはファイル システム CDOs に対して true ではありません。 したがって、CDO は IRP が受け取るすべてを最終的に完了する必要があります。 高速の I/O 要求を返す必要があります**TRUE**または**FALSE**します。

 

 




