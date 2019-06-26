---
title: フィルター エンジンへのコールアウトの登録
description: フィルター エンジンへのコールアウトの登録
ms.assetid: a5bade33-e3d1-4e1d-8503-51485097046e
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、初期化しています
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームの初期化
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームの初期化
- コールアウト WDK Windows フィルタ リング プラットフォームの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08f01e15ef409c71704bbbd9b5d37d07fae01828
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374762"
---
# <a name="registering-callouts-with-the-filter-engine"></a>フィルター エンジンへのコールアウトの登録


コールアウト ドライバーには、デバイス オブジェクトが作成、フィルター エンジンがそのコールアウトし登録できます。 コールアウト ドライバーを登録できます、コールアウト、フィルター エンジン、いつでも場合でも、フィルター エンジンが現在実行されていません。 コールアウト ドライバーの呼び出しに、フィルター エンジンを吹き出しを登録する、 [ **FwpsCalloutRegister0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpscalloutregister0)関数。 例:

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

場合に呼び出し、 [ **FwpsCalloutRegister0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpscalloutregister0)関数が成功すると、最後のパラメーターが指す変数にはコールアウトのランタイム識別子が含まれています。 このランタイム識別子は、引き出しキーに対して指定された GUID に対応します。

1 つのコールアウト ドライバーでは、1 つ以上のコールアウトを実装できます。 呼び出すコールアウト ドライバーでは、1 つ以上のコールアウトを実装する場合、 [ **FwpsCalloutRegister0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpscalloutregister0)関数をフィルター エンジンの各吹き出しを登録することをサポートする各コールアウトの 1 回です。

## <a name="related-topics"></a>関連トピック


[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

 

 






