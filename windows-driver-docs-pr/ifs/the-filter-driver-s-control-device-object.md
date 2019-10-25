---
title: フィルター ドライバーのコントロール デバイス オブジェクト
description: フィルター ドライバーのコントロール デバイス オブジェクト
ms.assetid: ac49b5d0-110d-4e47-814b-05f59791de41
keywords:
- デバイスオブジェクトの管理 WDK ファイルシステム
- CDOs WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cb335797db6104cd220d2228e5405de784f0b03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840956"
---
# <a name="the-filter-drivers-control-device-object"></a>フィルター ドライバーのコントロール デバイス オブジェクト


## <span id="ddk_the_filter_drivers_control_device_object_if"></span><span id="DDK_THE_FILTER_DRIVERS_CONTROL_DEVICE_OBJECT_IF"></span>


名前付きコントロールデバイスオブジェクト (CDO) を作成して使用するために必要なファイルシステムとは異なり、ファイルシステムフィルタードライバーには CDO が必要ではありません。 設定されている場合、この CDO は、オプションで名前を付けることができ、システムへのフィルタードライバーを表します。 その役割は、ユーザーモードアプリケーション (または、より一般的ではないカーネルモードドライバー) から i/o 要求を受信し、適切に動作させることです。

ほとんどのファイルシステムフィルタードライバーは、CDO を作成して使用します。 ただし、CDO での i/o 要求のサポートはオプションです。 このサポートを提供するには、フィルタードライバーが[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)を呼び出して CDO を作成するときに、オブジェクトのデバイス名を指定する必要があります。 ユーザーモードアプリケーションは、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を呼び出して、名前付き CDO へのハンドルを取得し、デバイス名のユーザーモードバージョンを提供できます。

たとえば、"MyLegacyFilter" という架空のカーネルモードドライバーを考えてみます。 このドライバーは、次の名前の CDO を作成できます。

```cpp
\Device\MyLegacyFilter
```

とは、この名前を同等のユーザーモードで表示される名前にリンクするために、 [**ioを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink)呼び出します。 これは、MyLegacyFilter のユーザーモードアプリケーションが名前を指定して、カーネルモードドライバーの CDO へのハンドルを開くことができるようにするためです。

```cpp
\\.\MyLegacyFilter
```

が[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を呼び出すとき。

### <a name="span-idtypes_of_i_o_requests_that_are_sent_to_the_filter_driver_s_control_devspanspan-idtypes_of_i_o_requests_that_are_sent_to_the_filter_driver_s_control_devspantypes-of-io-requests-that-are-sent-to-the-filter-drivers-control-device-object"></a><span id="types_of_i_o_requests_that_are_sent_to_the_filter_driver_s_control_dev"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_THE_FILTER_DRIVER_S_CONTROL_DEV"></span>フィルタードライバーのコントロールデバイスオブジェクトに送信される i/o 要求の種類

ファイルシステムフィルタードライバーは、コントロールデバイスオブジェクト (CDO) での i/o 操作をサポートするためには必要ありません。 ただし、ほとんどのフィルターでは、次の種類の i/o 要求をフィルターの CDO に送信できます。

-   [**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create) (ターゲットデバイスオブジェクトへのハンドルを開き、そのハンドルをユーザーアプリケーションに渡す)

-   [**IRP\_MJ\_CLEANUP**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-cleanup) (ターゲットデバイスオブジェクトへのユーザーモードアプリケーションのハンドルを閉じるため)

-   [**IRP\_MJ\_close**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-close) (ターゲットデバイスオブジェクトに対して開いている最後のハンドルを閉じるため)

-   [**Irp\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control)、 [**irp\_MJ\_ファイル\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)、または**fasystem.servicemodel Odevicecontrol** (プライベート ioctl または FSCTLs をフィルタードライバーに送信する)

ただし、ファイルシステムフィルタードライバーによって作成される他のすべてのデバイスオブジェクトとは異なり、CDO はドライバースタックにアタッチされません。 フィルタードライバーの CDO の上または下にデバイスオブジェクトがアタッチされていません。 そのため、受信した i/o 要求については、CDO は、それが唯一の目的の受信者であると想定することができます。 これは、デバイスオブジェクトのフィルター処理やファイルシステムの CDOs には当てはまりません。 したがって、CDO は、受信したすべての IRP を最終的に完了させる必要があります。 高速な i/o 要求の場合は、 **TRUE**または**FALSE**を返す必要があります。

 

 




