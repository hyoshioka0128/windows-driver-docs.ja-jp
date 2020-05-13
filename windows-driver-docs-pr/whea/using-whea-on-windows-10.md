---
title: Windows 10 での WHEA の使用
description: Windows 10 で WHEA エラーを報告する方法について説明します。
ms.assetid: ace3230c-3e41-4290-a1fe-74a6cfc1eb0b
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、Windows 10 の変更
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: a06916d6ee58ed91191ab566d9a079e472d08cbc
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270413"
---
# <a name="using-whea-on-windows-10"></a>Windows 10 での WHEA の使用

Windows 10 バージョン2004では、Windows ハードウェアエラーアーキテクチャ (WHEA) に新しいインターフェイス (v2) が追加されています。  このページでは、エラーソースとして登録し、エラーを報告する方法について説明します。

## <a name="adding-an-error-source"></a>エラーソースの追加

WHEA v2 を使用してエラーソースとして WHEA に登録するには、ドライバーは次の操作を行う必要があります。

1. [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)構造体をインスタンス化してデバイスドライバーの構成を指定し、 [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver)および[*WHEA_ERROR_SOURCE_UNINITIALIZE_DEVICE_DRIVER*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_uninitialize_device_driver)イベントコールバック関数へのポインターを提供します。
2. 構成構造を指定して[**WheaAddErrorSourceDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheaadderrorsourcedevicedriver)を呼び出します。  通常、ドライバーは*Driverentry*からこのルーチンを呼び出します。

    後でエラーソースを削除するには、 [**WheaRemoveErrorSourceDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)を呼び出します。

3. WHEA は、エラーソースがエラーを報告する準備ができたときに、ドライバーの[*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver)イベントコールバック関数を呼び出します。 ドライバーは、コールバックのパラメーターとして*Errorsourceid*を受け取ります。

## <a name="reporting-an-error"></a>エラーの報告

エラーを報告するには、次の手順を順番に実行します。

1. [**WheaCreateHwErrorReportDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheacreatehwerrorreportdevicedriver)を呼び出します。 *errorsourceid*と、必要に応じてドライバーの*DeviceObject*を提供します。  ルーチンは、進行中のエラーへのハンドルを返します。

2. エラーにデータを追加するには、エラーハンドルを指定して[**WheaAddHwErrorReportSectionDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheaaddhwerrorreportsectiondevicedriver)を呼び出します。  この関数は、エラーレポートに1つのセクションを追加し、ドライバーによって提供されるデータバッファーを構成します。  ドライバーは、 [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)で指定されているように、 **Maxsectionsperreport** times までこのルーチンを呼び出すことができます。

    必要に応じて、ドライバーは[**WheaHwErrorReportSetSeverityDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportsetseveritydevicedriver)を呼び出して、パケットとセクションのエラーの重要度を設定できます。 [**WHEA_ERROR_RECORD_SECTION_DESCRIPTOR**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record_section_descriptor)構造体の FRUText フィールドを更新するためのヘルパー関数である「 [**WheaHwErrorReportSetSectionNameDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportsetsectionnamedevicedriver)」も参照してください。

3. エラーデータをバッファーセットにコピーします。

4. もう一度[**WheaHwErrorReportSubmitDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportsubmitdevicedriver)を呼び出して、エラーハンドルを提供します。 この呼び出しの後、バッファーセット内のバッファーは使用できなくなり、ハンドルは無効になります。

5. エラーが発生した場合、またはエラーが無効になった場合、ドライバーは必要に応じて[**WheaHwErrorReportAbandonDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportabandondevicedriver)を呼び出すことができます。 この場合、WHEA にはレポートが送信されません。

ドライバーは、 [**WheaCreateHwErrorReportDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheacreatehwerrorreportdevicedriver)によって作成されたすべてのハンドルで、 [**WheaHwErrorReportSubmitDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportsubmitdevicedriver)または[**WheaHwErrorReportAbandonDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportabandondevicedriver)のいずれかを呼び出す必要があります。 それ以外の場合、 [**WheaRemoveErrorSourceDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)は STATUS_RESOURCE_IN_USE を返す可能性があります。
