---
title: FilterUnloadCallback ルーチンが呼び出された場合
description: FilterUnloadCallback ルーチンが呼び出された場合
ms.assetid: 22a3a73e-28be-4483-a7a6-73525e74503d
keywords:
- FilterUnloadCallback
- 任意のアンロード WDK ファイル システム ミニフィルター
- 必須のアンロード WDK ファイル システム ミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e94ef7593eb5bb12c84ab52d31a6a269120b4e8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550904"
---
# <a name="when-the-filterunloadcallback-routine-is-called"></a>FilterUnloadCallback ルーチンが呼び出された場合


## <span id="ddk_when_the_filterunloadcallback_routine_is_called_if"></span><span id="DDK_WHEN_THE_FILTERUNLOADCALLBACK_ROUTINE_IS_CALLED_IF"></span>


フィルター マネージャー呼び出しミニフィルター ドライバーの[ **FilterUnloadCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551085)ルーチンは次の方法のいずれかでミニフィルター ドライバーをアンロードする前に。

-   *非必須アンロード*します。 この種類のアンロードは、ユーザー モード アプリケーションが呼び出されたときに発生します[ **FilterUnload** ](https://msdn.microsoft.com/library/windows/hardware/ff541516)またはカーネル モード ドライバーが呼び出されて[ **FltUnloadFilter** 。](https://msdn.microsoft.com/library/windows/hardware/ff544602). 入力するときにも発生**fltmc unload**コマンド プロンプトでします。

-   *必須のアンロード*します。 この種類のアンロードは、」と入力してサービスの停止要求を発行するときに発生します。 **sc stop**または**net stop**コマンド プロンプトでします。 (の詳細については、 **sc stop**と**net stop**コマンド、クリックして**ヘルプし、サポート**[スタート] メニュー)。ユーザー モード アプリケーションが Microsoft Win32 を呼び出すときにも発生**ControlService**関数をサービス\_コントロール\_として停止制御コード、 *dwControl*パラメーター。 (サービスの Win32 関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください)。

任意のアンロードの場合、ミニフィルター ドライバーの*FilterUnloadCallback*ルーチンは、状態など、エラーまたは警告 NTSTATUS 値を返します\_FLT\_は\_いない\_デタッチ、フィルター マネージャーはミニフィルター ドライバーをアンロードしません。

フィルター マネージャーがミニフィルター ドライバーの後に、ミニフィルター ドライバーをアンロード、必須のアンロードの*FilterUnloadCallback*ルーチンが呼び出された場合でも、 *FilterUnloadCallback*ルーチンを返します、。状態など、エラーまたは警告の NTSTATUS 値\_FLT\_は\_いない\_デタッチします。

ミニフィルター ドライバーはミニフィルター ドライバーの必須のアンロードを無効にする、FLTFL を設定\_登録\_は\_いない\_サポート\_サービス\_で停止フラグ**フラグ**のメンバー、 [ **FLT\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544811)ミニフィルター ドライバーは、パラメーターとして渡される構造[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)でその**DriverEntry**ルーチン。 このフラグが設定されている場合、フィルター マネージャーは通常任意のアンロード要求を処理します。 ただし、必須のアンロード要求は失敗します。 フィルター マネージャーには、ミニフィルター ドライバーは呼び出しません*FilterUnloadCallback*アンロードが失敗した要求のルーチンです。

ミニフィルター ドライバーの場合に注意してください**DriverEntry**ルーチンは、警告またはエラー NTSTATUS の値を返します、 *FilterUnloadCallback*ルーチンは呼び出されませんフィルター マネージャーが、ミニフィルターを単にアンロード。ドライバー。

*FilterUnloadCallback*ルーチンは、システムのシャット ダウン時に呼び出されません。 シャット ダウン処理を実行する必要があるミニフィルター ドライバーは IRP の preoperation コールバック ルーチンを登録する必要があります\_MJ\_シャット ダウン操作。

 

 




