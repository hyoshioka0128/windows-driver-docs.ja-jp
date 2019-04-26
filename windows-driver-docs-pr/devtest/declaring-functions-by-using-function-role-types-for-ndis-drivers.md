---
title: NDIS ドライバーの関数役割型を使用した関数の宣言
description: NDIS ドライバーの関数役割型を使用した関数の宣言
ms.assetid: 232c4272-0bf0-4a4e-9560-3bceeca8a3e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6467f919247aa8b34e9df5b81eaf001e2965f6b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341156"
---
# <a name="declaring-functions-by-using-function-role-types-for-ndis-drivers"></a>NDIS ドライバーの関数役割型を使用した関数の宣言


SDV NDIS ドライバーの分析を有効にするには、NDIS の関数の役割の型宣言を使用して関数を宣言する必要があります。 関数のロールの種類は、Ndis.h で定義されます。

関数のロールの種類とその対応するイベントのコールバック関数の一覧で、次を参照してください。、[静的ドライバー検証ツールの NDIS 関数宣言](static-driver-verifier-ndis-function-declarations.md)します。

対応するロールの種類を指定することで、NDIS ドライバー内の各コールバック関数を宣言する必要があります。

次のコード例の関数の役割の型宣言を示しています、 *MiniportPause*コールバック関数。 この例では、コールバック関数が呼び出されます*myMiniportPause*します。 関数のロールの種類はミニポート\_一時停止します。

```
MINIPORT_PAUSE myMiniportPause;
```

コールバック関数に関数のプロトタイプ宣言がある場合とロールの種類の関数の宣言、関数プロトタイプを置き換える必要があります。

次の例は、ヘッダー ファイル、SDV にある、MP.h から NDIS 関数の宣言が失敗する\_WDK のドライバーのサブディレクトリ。 Main.c で、関連する関数が宣言されます。

\\ツール\\sdv\\サンプル\\失敗\_ドライバー\\NDIS\\失敗\_driver1 します。

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

### <a name="span-idfunctionparametersandfunctionroletypesspanspan-idfunctionparametersandfunctionroletypesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>関数パラメーターと関数のロールの種類

C プログラミング言語で必要に応じて関数定義で使用するパラメーターの型は、関数プロトタイプのパラメーターの型と一致する必要があります。 またはこの場合、関数のロールを入力します。 SDV は、分析関数のシグネチャに依存し、一致しないシグネチャを持つ関数を無視します。

たとえば、宣言する必要があります、 [ *MiniportInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559395)ミニポートを使用して機能\_ISR 関数ロールの種類。

```
MINIPORT_ISR myMPIsr;
```

割り込みのルーチンを実装するときに*myMPIsr*、ミニポートによって使用されるパラメーターの型が一致する必要があります\_ISR、具体的には、NDIS\_ハンドル、PBOOLEAN、および PULONG (を参照してください、 [ *MiniportInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559395)構文の関数)。

```
BOOLEAN 
myMPIsr(
    __in  NDIS_HANDLE      MiniportInterruptContext,
    __out PBOOLEAN        QueueMiniportInterruptDpcHandler,
    __out PULONG          TargetProcessors
    ) {
}
```

## <a name="span-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspanspan-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span> Code Analysis for Drivers は、関数宣言を確認するを実行しています。


ソース コードを準備するかどうかを判断するために、実行[Code Analysis for Drivers](code-analysis-for-drivers.md)します。 関数の役割の型宣言に対するドライバーのチェックのコード分析とされなかった可能性が関数宣言を特定するのに役立ちますまたは関数のロールの種類の関数定義のパラメーターが一致しない場合に警告を表示します。

 

 





