---
title: KMDF ドライバーの関数役割型を使用した関数の宣言
description: KMDF ドライバーの関数役割型を使用した関数の宣言
ms.assetid: 73a408ba-0219-4fde-8dad-ca330e4e67c3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9024cd3b17c4b2aa5f43326268468183d248c0b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341168"
---
# <a name="declaring-functions-by-using-function-role-types-for-kmdf-drivers"></a>KMDF ドライバーの関数役割型を使用した関数の宣言


KMDF ドライバーを分析する SDV を有効にするには、kmdf 役割タイプの関数の宣言を使用して、関数を宣言する必要があります。 関数のロールの種類は、Wdf.h と Wdf.h に含まれているその他の KMDF ヘッダー ファイル内に定義されます。 関数のロールの種類とその対応するイベントのコールバック関数の一覧で、次を参照してください。[静的ドライバー検証ツール KMDF 関数宣言](static-driver-verifier-kmdf-function-declarations.md)します。

KMDF ドライバー内の各イベントのコールバック関数は、対応するロールの種類を指定して宣言する必要があります。

たとえば、次のコード例の関数の役割の型宣言を示しています。、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 この例では、コールバック関数が呼び出されます*myDriver\_EvtDriverDeviceAdd*します。 関数のロールの種類は EVT\_WDF\_ドライバー\_デバイス\_を追加します。

```
EVT_WDF_DRIVER_DEVICE_ADD myDriver_EvtDriverDeviceAdd;
```

コールバック関数に関数のプロトタイプ宣言がある場合とロールの種類の関数の宣言、関数プロトタイプを置き換える必要があります。

次のリストは、ヘッダー ファイルの失敗から\_Driver6.h します。 関連する関数は、FailDriver6.c で宣言されます。

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

後に、ドライバーは、コールバック関数がロールの種類の宣言を使用して宣言している、[ドライバーをスキャン](scanning-the-driver.md)します。 ドライバーをスキャンするには、エントリ ポイントが正しく識別されているかを判断することを確認することができます、Sdv map.h ファイルが生成されます。

### <a name="span-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspanspan-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span> Code Analysis for Drivers は、関数宣言を確認するを実行しています。

ソース コードを準備するかどうかを判断するために、実行[Code Analysis for Drivers](code-analysis-for-drivers.md)します。 関数の役割の型宣言に対するドライバーのチェックのコード分析とされなかった可能性が関数宣言を特定するのに役立ちますまたは関数のロールの種類の関数定義のパラメーターが一致しない場合に警告を表示します。

### <a name="span-idfunctionparametersandfunctionroletypesspanspan-idfunctionparametersandfunctionroletypesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>関数パラメーターと関数のロールの種類

C プログラミング言語で必要に応じて関数定義で使用するパラメーターの型は、関数プロトタイプのパラメーターの型と一致する必要があります。 またはこの場合、関数のロールを入力します。 SDV は、分析関数のシグネチャに依存し、一致しないシグネチャを持つ関数を無視します。

たとえば、宣言する必要があります、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693) 、EVT を使用してルーチン\_WDF\_ドライバー\_デバイス\_関数ロールの種類を追加します。

```
EVT_WDF_DRIVER_DEVICE_ADD myEvtDriverDeviceAdd;
```

関数を実装する場合*myEvtDriverDeviceAdd*、EVT によって使用されるパラメーターの型が一致する必要があります\_WDF\_ドライバー\_デバイス\_WDFDRIVER と PWDFDEVICE namely を追加\_INIT (を参照してください[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)構文の日常的な)。

```
NTSTATUS
 myEvtDriverDeviceAdd (
  WDFDRIVER Driver,
 PWDFDEVICE_INIT DeviceInit
 )
{
}
```

 

 





