---
title: FilterUnloadCallback ルーチンの呼び出し時期
description: FilterUnloadCallback ルーチンの呼び出し時期
ms.assetid: 22a3a73e-28be-4483-a7a6-73525e74503d
keywords:
- FilterUnloadCallback
- 必須ではないアンロード WDK ファイルシステムミニフィルター
- 必須のアンロード WDK ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c575349d7cfca834401df1cc0abab7a8d0f97e62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840932"
---
# <a name="when-the-filterunloadcallback-routine-is-called"></a>FilterUnloadCallback ルーチンの呼び出し時期


## <span id="ddk_when_the_filterunloadcallback_routine_is_called_if"></span><span id="DDK_WHEN_THE_FILTERUNLOADCALLBACK_ROUTINE_IS_CALLED_IF"></span>


フィルタマネージャは、次のいずれかの方法でミニフィルタドライバをアンロードする前に、ミニフィルタドライバの[**FilterUnloadCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンを呼び出します。

-   *必須ではないアンロード*。 この種類のアンロードは、ユーザーモードアプリケーションが[**Filterunload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)を呼び出した場合、またはカーネルモードドライバーが[**Fltunloadfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunloadfilter)を呼び出した場合に発生します。 また、コマンドプロンプトで「 **fltmc unload** 」と入力した場合にも発生します。

-   *必須のアンロード*。 この種類のアンロードは、コマンドプロンプトで「 **sc stop** 」または「 **net stop** 」と入力して、サービス停止要求を発行したときに発生します。 ( **Sc stop**コマンドと**net stop**コマンドの詳細については、スタート メニューの **ヘルプとサポート** をクリックしてください)。また、ユーザーモードアプリケーションが Microsoft Win32 **Controlservice**関数を呼び出して、サービス\_制御\_、 *dwcontrol*パラメーターとしてコントロールコードを停止した場合にも発生します。 (Win32 サービス関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください)。

必須ではないアンロードの場合、ミニフィルタードライバーの*FilterUnloadCallback*ルーチンによってエラーまたは警告の NTSTATUS 値が返された場合 (STATUS\_FLT\_DO\_\_、DETACH など)、フィルターマネージャーはミニフィルターをアンロードしません。driver.

必須のアンロードの場合、フィルタマネージャは、ミニフィルタドライバの*FilterUnloadCallback*ルーチンが呼び出された後にミニフィルタドライバをアンロードします。たとえば、 *FilterUnloadCallback*ルーチンがエラーまたは警告の NTSTATUS 値を返した場合でも、ステータス\_FLT\_DO\_\_デタッチされません。

ミニフィルタードライバーの必須のアンロードを無効にするには、ミニフィルタードライバーによって、FLT の**Flags**メンバーで\_SERVICE\_STOP フラグが\_サポートされていない\_、FLTFL\_登録\_設定され[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)フィルタドライバーが**driverentry**ルーチン内の[**fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)にパラメーターとして渡す登録構造。 このフラグが設定されている場合、フィルターマネージャーは通常、必須ではないアンロード要求を処理します。 ただし、必須のアンロード要求は失敗します。 フィルターマネージャーは、失敗したアンロード要求に対してミニフィルタードライバーの*FilterUnloadCallback*ルーチンを呼び出しません。

ミニフィルタードライバーの**Driverentry**ルーチンから警告またはエラーの NTSTATUS 値が返された場合、 *FilterUnloadCallback*ルーチンは呼び出されないことに注意してください。フィルタマネージャーは、ミニフィルタードライバーを単にアンロードします。

*FilterUnloadCallback*ルーチンは、システムのシャットダウン時に呼び出されません。 シャットダウン処理を実行する必要があるミニフィルタードライバーは、IRP\_MJ\_のシャットダウン操作に対して preoperation コールバックルーチンを登録する必要があります。

 

 




