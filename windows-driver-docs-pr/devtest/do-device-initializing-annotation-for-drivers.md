---
title: ドライバーの DO_DEVICE_INITIALIZING 注釈
description: 使用すると、注釈付きの関数は、デバイス オブジェクトの Flags フィールドに DO_DEVICE_INITIALIZING ビットをオフにする必要かどうかを指定します。
ms.assetid: EFC5F0A3-7B20-49A5-9D50-1737DF76DC9E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca73e667c23f41ee2d7f89b9d651514b861e142c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577855"
---
# <a name="dodeviceinitializing-annotation-for-drivers"></a>\_デバイス\_ドライバーの初期化の注釈


使用、\_カーネル\_オフ\_は\_init\_注釈付きの関数は、オフに必要かどうかを指定する注釈\_デバイス\_のビットを初期化しています、デバイス オブジェクトのフィールドのフラグを設定します。

この注釈では、次の構文があります。

```
_Kernel_clear_do_init_(yes|no)
```

注釈がある関数を呼び出す\_カーネル\_オフ\_は\_init\_(yes) から、操作をオフにすることは、呼び出し元の関数を除外\_デバイス\_ビットを初期化します。

注釈ほぼ常に使用してください、条件付きのコンテキストで関数が成功した場合、返されるときに関数の型定義に注釈が適用されていない場合。 たとえば、ドライバーは、次の関数型定義で\_追加\_デバイス関数クラスでは、注釈を指定、関数が、IRQL を上げることができないし、関数、操作をオフにする必要のある\_デバイス\_ビットを初期化しています。

```
typedef
_IRQL_always_function_max_(PASSIVE_LEVEL)
_IRQL_requires_same_
_Kernel_clear_do_init_(yes)
__drv_functionClass(DRIVER_ADD_DEVICE)
NTSTATUS
DRIVER_ADD_DEVICE (
    _In_ struct _DRIVER_OBJECT *DriverObject,
    _In_ struct _DEVICE_OBJECT *PhysicalDeviceObject
    );
typedef DRIVER_ADD_DEVICE *PDRIVER_ADD_DEVICE;
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Windows ドライバーの SAL 2.0 注釈](sal-2-annotations-for-windows-drivers.md)










