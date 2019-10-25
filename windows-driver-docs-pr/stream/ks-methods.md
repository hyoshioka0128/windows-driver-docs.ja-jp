---
title: KS のメソッド
description: KS のメソッド
ms.assetid: 1d7bd6f4-0aaf-4d77-8132-f551fd2ecbd2
keywords:
- カーネルストリーミング WDK、メソッド
- KS WDK、メソッド
- 方法 WDK カーネルストリーミング
- メソッドは WDK カーネルストリーミングを設定します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 011b0614ced6082fb29b33cf6311adb6816610c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842512"
---
# <a name="ks-methods"></a>KS のメソッド





メソッドセットは、カーネルストリーミングクライアントが KS オブジェクトで呼び出すことができる関連アクションのグループです。 たとえば、アロケーターオブジェクトは、メモリの割り当てと割り当て解除を行うメソッドを含むメソッドセットを提供できます。

ミニドライバーは、サポートする各メソッドセットの\_構造体を[**設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmethod_set)します。 さらに、KSK メソッド\_SET 構造体には、1つのメソッドを記述する[**Ksk メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmethod_item)構造体の配列が含まれています。 ミニドライバーは、 [*KSTRSUPPORTHANDLER*](https://docs.microsoft.com/previous-versions/ff567206(v=vs.85))メソッド\_項目構造体の**Methodhandler**および**SupportHandler**メンバーで、ドライバーによって提供される[*kstrmethodhandler*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkshandler)および処理ルーチンへのポインターを提供します。

クライアントは、 [**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)を呼び出すか、(Microsoft Windows SDK のドキュメントで説明されている) **DeviceIoControl**を呼び出すことによって非同期要求を送信し、 [**IOCTL\_KS\_メソッドを呼び出します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ni-ks-ioctl_ks_method).

ドライバーは、前の呼び出しの*Inbuffer*パラメーターに[**ksk メソッド**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))構造体を指定することによって、特定のメソッドを要求します。

AVStream のフィルターとピンは、ksk[**フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)構造体または kspin\_の**AutomationTable**メンバーに[**ksk オートメーション\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksautomation_table_)構造を指定することによってサポートされるメソッドを記述します。 [**記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体。 詳細については、「[オートメーションテーブルの定義](defining-automation-tables.md)」を参照してください。

 

 




