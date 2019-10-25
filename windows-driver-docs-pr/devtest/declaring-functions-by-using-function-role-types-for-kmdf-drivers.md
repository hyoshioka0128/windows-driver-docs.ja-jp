---
title: KMDF ドライバーの関数役割型を使用した関数の宣言
description: KMDF ドライバーの関数役割型を使用した関数の宣言
ms.assetid: 73a408ba-0219-4fde-8dad-ca330e4e67c3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3d91b8b9b079b11090601fdc92024a23a35720b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840283"
---
# <a name="declaring-functions-by-using-function-role-types-for-kmdf-drivers"></a>KMDF ドライバーの関数役割型を使用した関数の宣言


SDV で KMDF ドライバーを分析できるようにするには、KMDF の関数ロール型宣言を使用して関数を宣言する必要があります。 関数ロールの型は、Wdf と、Wdf に含まれる他の KMDF ヘッダーファイルで定義されています。 関数ロールの種類とそれに対応するイベントコールバック関数の一覧については、「 [Static Driver Verifier KMDF 関数の宣言](static-driver-verifier-kmdf-function-declarations.md)」を参照してください。

KMDF ドライバーの各イベントコールバック関数は、対応するロールの種類を指定して宣言する必要があります。

たとえば、次のコード例は、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数の関数ロール型宣言を示しています。 この例では、コールバック関数は、 *Mydriver\_EvtDriverDeviceAdd*と呼ばれています。 機能ロールの種類は .EVT\_WDF\_ドライバー\_デバイス\_追加です。

```
EVT_WDF_DRIVER_DEVICE_ADD myDriver_EvtDriverDeviceAdd;
```

コールバック関数に関数プロトタイプ宣言がある場合は、関数プロトタイプを関数ロール型宣言に置き換える必要があります。

次の一覧は、ヘッダーファイルの Driver6 が\_失敗したことを示しています。 関連する関数は、FailDriver6 で宣言されています。

```
/*++

Copyright (C) Microsoft.  All rights reserved.
Module Name:
    fail_driver6.h
Environment:
    Kernel mode
--*/

#include <NTDDK.h>  
#include <wdf.h>

#include "fail_library6.h"

DRIVER_INITIALIZE DriverEntry;
EVT_WDF_DRIVER_DEVICE_ADD EvtDriverDeviceAdd;
EVT_WDF_IO_QUEUE_IO_READ EvtIoRead;
EVT_WDF_IO_QUEUE_IO_WRITE EvtIoWrite;
EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL EvtIoDeviceControl;
EVT_WDF_DEVICE_CONTEXT_CLEANUP DeviceContextCleanUp;
EVT_WDF_DEVICE_CONTEXT_DESTROY DeviceContextDestroy;
EVT_WDF_IO_QUEUE_CONTEXT_CLEANUP_CALLBACK QueueCleanup;
EVT_WDF_IO_QUEUE_CONTEXT_DESTROY_CALLBACK QueueDestroy;
EVT_WDF_FILE_CONTEXT_CLEANUP_CALLBACK FileContextCleanup;
EVT_WDF_FILE_CONTEXT_DESTROY_CALLBACK FileContextDestroy;
```

ロールの種類の宣言を使用してドライバーコールバック関数を宣言した後、[ドライバーをスキャン](scanning-the-driver.md)できます。 ドライバーをスキャンすると、Sdv .h ファイルが生成されます。このファイルを調べて、エントリポイントが正しく識別されたかどうかを確認できます。

### <a name="span-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspanspan-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span>ドライバーのコード分析を実行して関数の宣言を検証する

ソースコードが準備されているかどうかを判断するために、[ドライバーのコード分析](code-analysis-for-drivers.md)を実行します。 ドライバーのコード分析では、関数ロールの種類の宣言をチェックします。また、関数定義のパラメーターが関数ロール型のパラメーターと一致しない場合に、失敗した可能性がある関数宣言を識別したり、警告を表示したりすることができます。

### <a name="span-idfunction_parameters_and_function_role_typesspanspan-idfunction_parameters_and_function_role_typesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>関数のパラメーターと関数のロール型

C プログラミング言語で必要とされるように、関数定義で使用するパラメーター型は、関数プロトタイプのパラメーター型 (この場合は関数ロール型) と一致する必要があります。 SDV は分析のために関数シグネチャに依存しており、署名が一致しない関数は無視されます。

たとえば、\_WDF\_ドライバー\_デバイス\_追加機能のロールの種類を使用して、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)ルーチンを宣言する必要があります。

```
EVT_WDF_DRIVER_DEVICE_ADD myEvtDriverDeviceAdd;
```

関数*Myevtdriverdeviceadd*を実装する場合、パラメーターの型は、.EVT\_WDF\_DRIVER\_デバイス\_ADD、WDFDRIVER および PWDFDEVICE\_INIT ( [*evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)を参照) で使用されているものと一致する必要があります。構文のルーチン。

```
NTSTATUS
 myEvtDriverDeviceAdd (
  WDFDRIVER Driver,
 PWDFDEVICE_INIT DeviceInit
 )
{
}
```

 

 





