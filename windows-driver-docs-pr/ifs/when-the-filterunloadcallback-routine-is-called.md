---
title: FilterUnloadCallback ルーチンの呼び出し時期
description: FilterUnloadCallback ルーチンの呼び出し時期
ms.assetid: 22a3a73e-28be-4483-a7a6-73525e74503d
keywords:
- FilterUnloadCallback
- 任意のアンロード WDK ファイル システム ミニフィルター
- 必須のアンロード WDK ファイル システム ミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 486e4fdc67301b528378a1bc63a573d3e2a21101
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385307"
---
# <a name="when-the-filterunloadcallback-routine-is-called"></a>FilterUnloadCallback ルーチンの呼び出し時期


## <span id="ddk_when_the_filterunloadcallback_routine_is_called_if"></span><span id="DDK_WHEN_THE_FILTERUNLOADCALLBACK_ROUTINE_IS_CALLED_IF"></span>


フィルター マネージャー呼び出しミニフィルター ドライバーの[ **FilterUnloadCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンは次の方法のいずれかでミニフィルター ドライバーをアンロードする前に。

-   *非必須アンロード*します。 この種類のアンロードは、ユーザー モード アプリケーションが呼び出されたときに発生します[ **FilterUnload** ](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)またはカーネル モード ドライバーが呼び出されて[ **FltUnloadFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltunloadfilter)。 入力するときにも発生**fltmc unload**コマンド プロンプトでします。

-   *必須のアンロード*します。 この種類のアンロードは、」と入力してサービスの停止要求を発行するときに発生します。 **sc stop**または**net stop**コマンド プロンプトでします。 (の詳細については、 **sc stop**と**net stop**コマンド、クリックして**ヘルプし、サポート**[スタート] メニュー)。ユーザー モード アプリケーションが Microsoft Win32 を呼び出すときにも発生**ControlService**関数をサービス\_コントロール\_として停止制御コード、 *dwControl*パラメーター。 (サービスの Win32 関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください)。

任意のアンロードの場合、ミニフィルター ドライバーの*FilterUnloadCallback*ルーチンは、状態など、エラーまたは警告 NTSTATUS 値を返します\_FLT\_は\_いない\_デタッチ、フィルター マネージャーはミニフィルター ドライバーをアンロードしません。

フィルター マネージャーがミニフィルター ドライバーの後に、ミニフィルター ドライバーをアンロード、必須のアンロードの*FilterUnloadCallback*ルーチンが呼び出された場合でも、 *FilterUnloadCallback*ルーチンを返します、。状態など、エラーまたは警告の NTSTATUS 値\_FLT\_は\_いない\_デタッチします。

ミニフィルター ドライバーはミニフィルター ドライバーの必須のアンロードを無効にする、FLTFL を設定\_登録\_は\_いない\_サポート\_サービス\_で停止フラグ**フラグ**のメンバー、 [ **FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_registration)ミニフィルター ドライバーは、パラメーターとして渡される構造[ **FltRegisterFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)でその**DriverEntry**ルーチン。 このフラグが設定されている場合、フィルター マネージャーは通常任意のアンロード要求を処理します。 ただし、必須のアンロード要求は失敗します。 フィルター マネージャーには、ミニフィルター ドライバーは呼び出しません*FilterUnloadCallback*アンロードが失敗した要求のルーチンです。

ミニフィルター ドライバーの場合に注意してください**DriverEntry**ルーチンは、警告またはエラー NTSTATUS の値を返します、 *FilterUnloadCallback*ルーチンは呼び出されませんフィルター マネージャーが、ミニフィルターを単にアンロード。ドライバー。

*FilterUnloadCallback*ルーチンは、システムのシャット ダウン時に呼び出されません。 シャット ダウン処理を実行する必要があるミニフィルター ドライバーは IRP の preoperation コールバック ルーチンを登録する必要があります\_MJ\_シャット ダウン操作。

 

 




