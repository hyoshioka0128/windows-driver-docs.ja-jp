---
title: KS のメソッド
description: KS のメソッド
ms.assetid: 1d7bd6f4-0aaf-4d77-8132-f551fd2ecbd2
keywords:
- カーネルの WDK、メソッドのストリーミング
- KS WDK、メソッド
- ストリーミング メソッド WDK カーネル
- メソッドは、WDK のストリームを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b78f53f79834bf8f01d5e0b847fbd260d69bfd8c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382513"
---
# <a name="ks-methods"></a>KS のメソッド





メソッドのセットは、ストリーミング クライアントのカーネルは、KS オブジェクトで呼び出すことができる関連するアクションのグループです。 たとえば、アロケーター オブジェクトには、設定の割り当てし、メモリの割り当てを解除するメソッドを格納しているメソッドを提供できます。

ミニドライバーの提供、 [ **KSMETHOD\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmethod_set)サポートする各メソッド設定の構造体します。 さらに、KSMETHOD\_セット構造体には配列が含まれています[ **KSMETHOD\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmethod_item) 1 つのメソッドを記述する構造体。 ドライバーによって提供されるへのポインターを提供する、ミニドライバー [ *KStrMethodHandler* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkshandler)と[ *KStrSupportHandler* ](https://docs.microsoft.com/previous-versions/ff567206(v=vs.85))処理ルーチンで**MethodHandler**と**SupportHandler** 、KSMETHOD のメンバー\_項目の構造体。

クライアントが呼び出すことによって同期メソッドの要求を行う[ **KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)、または呼び出すことによって、非同期要求**DeviceIoControl** (で説明されている、Microsoft Windows SDK のドキュメント) で[ **IOCTL\_KS\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ni-ks-ioctl_ks_method)します。

ドライバーが提供することで、特定のメソッドを要求する[ **KSMETHOD** ](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))構造体、 *InBuffer*上の呼び出しのパラメーター。

AVStream フィルターとピンが提供することによってサポートされる方法を説明します、 [ **KSAUTOMATION\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksautomation_table_)構造体、 **AutomationTable**のメンバーいずれかを[ **KSFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)構造または[ **KSPIN\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。 詳細については、次を参照してください。 [Automation テーブルを定義する](defining-automation-tables.md)します。

 

 




