---
title: フィルター エンジンへのコールアウトの登録
description: フィルター エンジンへのコールアウトの登録
ms.assetid: a5bade33-e3d1-4e1d-8503-51485097046e
keywords:
- Windows フィルタリングプラットフォームのコールアウトドライバーの WDK、初期化
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、初期化
- コールアウトドライバーの初期化 WDK Windows フィルタリングプラットフォーム
- コールアウトの登録 WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34f70e1e059a685845fbcbd394cd55a808cd9927
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842080"
---
# <a name="registering-callouts-with-the-filter-engine"></a>フィルター エンジンへのコールアウトの登録


コールアウトドライバーは、デバイスオブジェクトを作成した後、そのコールアウトをフィルターエンジンに登録できます。 コールアウトドライバーは、フィルターエンジンが現在実行されていない場合でも、いつでもフィルターエンジンにコールアウトを登録できます。 コールアウトドライバーは、コールアウトをフィルターエンジンに登録するために、 [**FwpsCalloutRegister0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister0)関数を呼び出します。 次に、例を示します。

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

[**FwpsCalloutRegister0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister0)関数の呼び出しが成功した場合、最後のパラメーターが指す変数は、コールアウトのランタイム識別子を格納します。 この実行時識別子は、コールアウトキーに指定された GUID に対応します。

1つのコールアウトドライバーでは、複数のコールアウトを実装できます。 コールアウトドライバーが複数のコールアウトを実装している場合は、フィルターエンジンで各コールアウトを登録するためにサポートされている各コールアウトに対して[**FwpsCalloutRegister0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister0)関数が1回呼び出されます。

## <a name="related-topics"></a>関連トピック


[Classid (場合)](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

 

 






