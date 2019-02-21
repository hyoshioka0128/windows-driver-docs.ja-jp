---
title: フィルター エンジンとコールアウトを登録します。
description: フィルター エンジンとコールアウトを登録します。
ms.assetid: a5bade33-e3d1-4e1d-8503-51485097046e
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、初期化しています
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームの初期化
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームの初期化
- コールアウト WDK Windows フィルタ リング プラットフォームの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb8d789bb064798dff30d65a0be8da8385f35d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552369"
---
# <a name="registering-callouts-with-the-filter-engine"></a>フィルター エンジンとコールアウトを登録します。


コールアウト ドライバーには、デバイス オブジェクトが作成、フィルター エンジンがそのコールアウトし登録できます。 コールアウト ドライバーを登録できます、コールアウト、フィルター エンジン、いつでも場合でも、フィルター エンジンが現在実行されていません。 コールアウト ドライバーの呼び出しに、フィルター エンジンを吹き出しを登録する、 [ **FwpsCalloutRegister0** ](https://msdn.microsoft.com/library/windows/hardware/ff551140)関数。 次に、例を示します。

```C++
// Prototypes for the callout's callout functions
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    IN OUT FWPS_CLASSIFY_OUT0  *classifyOut
    );

NTSTATUS NTAPI
 NotifyFn(
 IN FWPS_CALLOUT_NOTIFY_TYPE notifyType,
    IN const GUID  *filterKey,
    IN const FWPS_FILTER0  *filter
    );

VOID NTAPI
 FlowDeleteFn(
    IN UINT16  layerId,
    IN UINT32  calloutId,
    IN UINT64  flowContext
    );

// Callout registration structure
const FWPS_CALLOUT0 Callout =
{
 { ... }, // GUID key identifying the callout
  0,       // Callout-specific flags (none set here)
 ClassifyFn,
 NotifyFn,
 FlowDeleteFn
};

// Variable for the run-time callout identifier
UINT32 CalloutId;

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  PDEVICE_OBJECT deviceObject;
  NTSTATUS status;

  ...

 status =
 FwpsCalloutRegister0(
 deviceObject,
      &Callout,
      &CalloutId
      );

  ...

 return status;
}
```

場合に呼び出し、 [ **FwpsCalloutRegister0** ](https://msdn.microsoft.com/library/windows/hardware/ff551140)関数が成功すると、最後のパラメーターが指す変数にはコールアウトのランタイム識別子が含まれています。 このランタイム識別子は、引き出しキーに対して指定された GUID に対応します。

1 つのコールアウト ドライバーでは、1 つ以上のコールアウトを実装できます。 呼び出すコールアウト ドライバーでは、1 つ以上のコールアウトを実装する場合、 [ **FwpsCalloutRegister0** ](https://msdn.microsoft.com/library/windows/hardware/ff551140)関数をフィルター エンジンの各吹き出しを登録することをサポートする各コールアウトの 1 回です。

## <a name="related-topics"></a>関連トピック


[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)

 

 






