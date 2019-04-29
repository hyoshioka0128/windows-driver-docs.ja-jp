---
title: パラメーターの修正
description: パラメーターの修正
ms.assetid: 01accd7f-7aa6-4f83-b8b4-81c04cd48dac
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、パラメーターの変更
- スワップ バッファー WDK ファイル システム ミニフィルター
- バッファー WDK ファイル システム ミニフィルター
- メモリの記述子が WDK ファイル システム ミニフィルターを一覧表示します。
- MDLs WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47f4b3175b27ccc6a882bdd1a4548ec032cbaaa7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384276"
---
# <a name="modifying-parameters"></a>パラメーターの修正


ミニフィルター ドライバーには、ターゲットのインスタンス、ターゲット ファイルのオブジェクト、およびバッファーのアドレスやメモリ記述子のリスト (MDL) アドレスなど操作固有のパラメーターなど、I/O 操作に関連付けられている特定のパラメーターを変更できます。 ミニフィルター ドライバーでは、通常、I/O 要求の preoperation、コールバックのパラメーターを変更します。 ミニフィルター ドライバーでは、パラメーターを変更する場合は、呼び出す必要があります[ **FltSetCallbackDataDirty** ](https://msdn.microsoft.com/library/windows/hardware/ff544383)パラメーターが変更されたフィルター マネージャーに通知します。 その postoperation コールバックを利用できるように、その preoperation コールバックから渡されたコンテキストに変更を記録にする必要があります。

ミニフィルター ドライバーがその preoperation コールバックまたはその postoperation コールバックでは、操作が失敗した操作を完了するときに操作の I/O 状態を変更 (状態を変更するなど\_はエラー状態に成功した場合)。 呼び出す必要はありません[ **FltSetCallbackDataDirty** ](https://msdn.microsoft.com/library/windows/hardware/ff544383)ここでします。

パラメーターを変更する方法の詳細については、次を参照してください。 [I/O 操作のパラメーターを変更する](modifying-the-parameters-for-an-i-o-operation.md)します。

「スワップ バッファー」の I/O 要求のバッファー フィールドを独自のバッファーに置き換えることによりミニフィルター ドライバー。 このようなミニフィルター ドライバーとは、I/O 要求のフィールドの MDL バッファーとの同期を保つ責任を負います。フィルター マネージャーの設定、FLTFL\_コールバック\_データ\_システム\_バッファー\_フラグ、 [ **FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)バッファーは、システムのバッファーであるかどうかであるかどうかはそのため、ミニフィルター ドライバーする必要があります非ページ プールから置換バッファーを割り当てる MDL のフィールドに設定を示す構造**NULL**します。 それ以外の場合、バッファー ページか、または非ページ プールから割り当てることができます、ミニフィルター ドライバーが作成常に、し、MDL を設定する必要があります。 (高速の I/O 操作の場合は、新しいバッファーをページか、または非ページ プールから割り当てられることができ、MDL 必要があります**NULL**)。バッファーまたは、置き換える MDL ミニフィルター ドライバーを解放する必要があり、MDL のコールバックのデータ構造 (フィルター マネージャーは、MDL をミニフィルター ドライバーの代わりに解放されます) に正しく挿入を解放する必要があります。 ミニフィルター ドライバーを呼び出す必要があります、MDL バッファーを変更を行った後[ **FltSetCallbackDataDirty**](https://msdn.microsoft.com/library/windows/hardware/ff544383)します。

ミニフィルター ドライバーには、バッファーを交換がすべての操作に対して postoperation コールバックを登録する必要があります。 このコールバック ルーチン ミニフィルター ドライバーは、割り当てられているすべてのバッファーを解放する必要があります。 フィルター マネージャー ミニフィルター ドライバー呼び出さない限り、MDL が解放されます[ **FltRetainSwappedBufferMdlAddress**](https://msdn.microsoft.com/library/windows/hardware/ff544352)この例ではミニフィルター ドライバーは MDL の解放を担当します。 ミニフィルター ドライバーが呼び出せる[ **FltGetSwappedBufferMdlAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff543161) MDL バッファーを取得、その preoperation コールバックで設定します。

ミニフィルター ドライバーがアンロードされた場合のバッファーをスワップが操作中に、操作できません「を使い切ること」です。代わりに、操作をキャンセルし、フィルター マネージャーがミニフィルター ドライバーをアンロードする前に完了する操作を待機します。

バッファーをスワップしたミニフィルター ドライバーの例については、SwapBuffers サンプルを参照してください。

### <a name="span-idfiltermanagerroutinesformodifyingparametersspanspan-idfiltermanagerroutinesformodifyingparametersspanspan-idfiltermanagerroutinesformodifyingparametersspanfilter-manager-routines-for-modifying-parameters"></a><span id="Filter_Manager_Routines_for_Modifying_Parameters"></span><span id="filter_manager_routines_for_modifying_parameters"></span><span id="FILTER_MANAGER_ROUTINES_FOR_MODIFYING_PARAMETERS"></span>パラメーターを変更するためにマネージャーのルーチンをフィルター処理します。

フィルター マネージャーは、preoperation と postoperation コールバック ルーチン内で I/O 操作のパラメーターを変更するため、次のサポート ルーチンを提供します。

[**FltClearCallbackDataDirty**](https://msdn.microsoft.com/library/windows/hardware/ff541853)

[**FltIsCallbackDataDirty**](https://msdn.microsoft.com/library/windows/hardware/ff543311)

[**FltSetCallbackDataDirty**](https://msdn.microsoft.com/library/windows/hardware/ff544383)

次のルーチンは、バッファーをスワップするためのサポートを提供します。

[**FltGetSwappedBufferMdlAddress**](https://msdn.microsoft.com/library/windows/hardware/ff543161)

[**FltRetainSwappedBufferMdlAddress**](https://msdn.microsoft.com/library/windows/hardware/ff544352)

 

 




