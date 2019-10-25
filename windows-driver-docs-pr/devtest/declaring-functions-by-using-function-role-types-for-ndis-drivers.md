---
title: NDIS ドライバーの関数役割型を使用した関数の宣言
description: NDIS ドライバーの関数役割型を使用した関数の宣言
ms.assetid: 232c4272-0bf0-4a4e-9560-3bceeca8a3e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e72f4f76c043180fd14416f1f3f2c0c8e27aad6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839567"
---
# <a name="declaring-functions-by-using-function-role-types-for-ndis-drivers"></a>NDIS ドライバーの関数役割型を使用した関数の宣言


SDV で NDIS ドライバーを分析できるようにするには、NDIS の関数ロール型宣言を使用して関数を宣言する必要があります。 関数ロールの種類は、Ndis. h で定義されています。

関数ロールの種類とそれに対応するイベントコールバック関数の一覧については、「 [Static Driver Verifier の NDIS 関数宣言](static-driver-verifier-ndis-function-declarations.md)」を参照してください。

NDIS ドライバーの各コールバック関数は、対応するロールの種類を指定して宣言する必要があります。

次のコード例は、 *Miniportpause*コールバック関数の関数ロール型宣言を示しています。 この例では、コールバック関数は*Myminiportpause*と呼ばれています。 関数ロールの種類は、ミニポート\_一時停止です。

```
MINIPORT_PAUSE myMiniportPause;
```

コールバック関数に関数プロトタイプ宣言がある場合は、関数プロトタイプを関数ロール型宣言に置き換える必要があります。

次の例は、ヘッダーファイル MP からの NDIS 関数宣言を示しています。これは、WDK の SDV fail\_drivers サブディレクトリにあります。 関連する関数は、Main で宣言されています。

\\ツール\\sdv\\サンプル\\失敗\_\\\\NDIS\_driver1。

```
/--------------------------------------
// Miniport routines in MAIN.C
//--------------------------------------

NDIS_STATUS
DriverEntry(
    IN  PDRIVER_OBJECT      DriverObject,
    IN  PUNICODE_STRING     RegistryPath
    );


MINIPORT_ALLOCATE_SHARED_MEM_COMPLETE MPAllocateComplete;

MINIPORT_HALT MPHalt;
MINIPORT_SET_OPTIONS MPSetOptions;
MINIPORT_INITIALIZE MPInitialize;
MINIPORT_PAUSE MPPause;
MINIPORT_RESTART MPRestart;
MINIPORT_OID_REQUEST MPOidRequest;
MINIPORT_INTERRUPT_DPC MPHandleInterrupt;
MINIPORT_ISR MPIsr;
MINIPORT_RESET MPReset;
MINIPORT_RETURN_NET_BUFFER_LISTS MPReturnNetBufferLists;
MINIPORT_CANCEL_OID_REQUEST MPCancelOidRequest;
MINIPORT_SHUTDOWN MPShutdown;
MINIPORT_SEND_NET_BUFFER_LISTS MPSendNetBufferLists;
MINIPORT_CANCEL_SEND MPCancelSendNetBufferLists;
MINIPORT_DEVICE_PNP_EVENT_NOTIFY MPPnPEventNotify;
MINIPORT_UNLOAD MPUnload;
MINIPORT_CHECK_FOR_HANG MPCheckForHang;
MINIPORT_ENABLE_INTERRUPT MpEnableInterrupt;
MINIPORT_DISABLE_INTERRUPT MpDisableInterrupt;
MINIPORT_SYNCHRONIZE_INTERRUPT MPSynchronizeInterrupt;
MINIPORT_PROCESS_SG_LIST MPProcessSGList;
NDIS_TIMER_FUNCTION MpDemonstrationTimer;
NDIS_IO_WORKITEM MPQueuedWorkItem;
```

### <a name="span-idfunction_parameters_and_function_role_typesspanspan-idfunction_parameters_and_function_role_typesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>関数のパラメーターと関数のロール型

C プログラミング言語で必要とされるように、関数定義で使用するパラメーター型は、関数プロトタイプのパラメーター型 (この場合は関数ロール型) と一致する必要があります。 SDV は分析のために関数シグネチャに依存しており、署名が一致しない関数は無視されます。

たとえば、ミニポート\_ISR 関数の役割の種類を使用して、 [*Miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)関数を宣言する必要があります。

```
MINIPORT_ISR myMPIsr;
```

割り込みルーチン ( *Mympisr*) を実装する場合、パラメーターの型は、ミニポート\_ISR、つまり、NDIS\_HANDLE、pboolean、および (構文については「 [*miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)関数」を参照) によって使用される型と一致する必要があります。

```
BOOLEAN 
myMPIsr(
    __in  NDIS_HANDLE      MiniportInterruptContext,
    __out PBOOLEAN        QueueMiniportInterruptDpcHandler,
    __out PULONG          TargetProcessors
    ) {
}
```

## <a name="span-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspanspan-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span>ドライバーのコード分析を実行して関数の宣言を検証する


ソースコードが準備されているかどうかを判断するために、[ドライバーのコード分析](code-analysis-for-drivers.md)を実行します。 ドライバーのコード分析では、関数ロールの種類の宣言をチェックします。また、関数定義のパラメーターが関数ロール型のパラメーターと一致しない場合に、失敗した可能性がある関数宣言を識別したり、警告を表示したりすることができます。

 

 





