---
title: I/O 操作のパラメーターを変更します。
description: I/O 操作のパラメーターを変更します。
ms.assetid: 8e25842f-6f10-412f-8cb2-156bea7d7983
keywords:
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、パラメーターの変更
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、パラメーターの変更
- ファイル システム ミニフィルター ドライバー WDK、I/O のパラメーターの変更
- ミニフィルター ドライバー WDK、I/O のパラメーターの変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bba99331db7919c3b2c44ada8bbe286f8dfc0ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538019"
---
# <a name="modifying-the-parameters-for-an-io-operation"></a>I/O 操作のパラメーターを変更します。


## <span id="ddk_modifying_the_parameters_for_an_io_operation_if"></span><span id="DDK_MODIFYING_THE_PARAMETERS_FOR_AN_IO_OPERATION_IF"></span>


ミニフィルター ドライバーには、I/O 操作のパラメーターを変更できます。 たとえば、ミニフィルター ドライバーの[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)操作のターゲット インスタンスを変更することで、別のボリュームに、I/O 操作をリダイレクトできます。 新しいターゲット インスタンスは、別のボリュームに同じ高度に同じミニフィルター ドライバーのインスタンスである必要があります。

コールバック データ内に、I/O 操作のパラメーターがある ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造とパラメーターの I/O ブロック ([ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)) 操作の構造。 ミニフィルター ドライバーの[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)と[ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107)へのポインターを受信します内の操作のコールバックのデータ構造、*データ*入力パラメーター。 *Iopb*コールバックのデータ構造体のメンバーは、操作のパラメーターを含む I/O パラメーター ブロック構造へのポインター。

ミニフィルター ドライバーの preoperation コールバック ルーチンが、I/O 操作のパラメーターを変更、ミニフィルター ドライバーはミニフィルター ドライバーのインスタンスのスタックで以下のすべてのミニフィルター ドライバーはその preoperation で変更されたパラメーターを受信し、postoperation コールバック ルーチン。

現在ミニフィルター ドライバーの postoperation コールバック ルーチンまたはミニフィルター ドライバーはミニフィルター ドライバーのインスタンスのスタックで上記のすべてのミニフィルター ドライバーによって、変更後のパラメーターは受信されません。 すべての状況ではミニフィルター ドライバーの preoperation postoperation コールバック ルーチンは、指定した I/O 操作で同じ入力パラメーターの値を受け取るとします。

ように呼び出すことによって、I/O 操作のパラメーターを変更するには後から preoperation または postoperation コールバック ルーチンに示す必要があります[ **FltSetCallbackDataDirty**](https://msdn.microsoft.com/library/windows/hardware/ff544383)変更されている場合を除き、内容のコールバックのデータ構造体の**IoStatus**フィールド。 それ以外の場合、フィルター マネージャーでは、パラメーター値の変更には無視します。 **FltSetCallbackDataDirty**設定、FLTFL\_コールバック\_データ\_ダーティ I/O 操作のコールバックのデータ構造体のフラグ。 ミニフィルター ドライバーは、呼び出すことでこのフラグをテストできます[ **FltIsCallbackDataDirty** ](https://msdn.microsoft.com/library/windows/hardware/ff543311)または呼び出すことによってオフに[ **FltClearCallbackDataDirty** ](https://msdn.microsoft.com/library/windows/hardware/ff541853).

ミニフィルター ドライバーの preoperation コールバック ルーチンが、I/O 操作のパラメーターを変更、ミニフィルター ドライバーはミニフィルター ドライバーのインスタンスのスタックで以下のすべてのミニフィルター ドライバーでは、変更されたパラメーターが表示されます、*データ*と*FltObjects* preoperation と postoperation コールバック ルーチンへのパラメーターを入力します。 (ミニフィルター ドライバーからの内容を直接変更することはできません、 [ **FLT\_関連\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544816)が指す構造、 *FltObjects*パラメーター。 ただし、ミニフィルター ドライバーでは、ターゲット インスタンスまたは I/O 操作の対象のファイル オブジェクトを変更、フィルター マネージャーは 対応の値を変更**インスタンス**または**FileObject**のメンバー、FLT\_関連\_は下限に渡されたミニフィルター ドライバーを構造化オブジェクト)。

ミニフィルター ドライバーの preoperation コールバック ルーチンは、任意のパラメーターの変更は、ミニフィルター ドライバーの postoperation コールバック ルーチンによって受信されていない、preoperation コールバック ルーチンが変更されたパラメーターに関する情報を渡すことがミニフィルター ドライバーの postoperation コールバック ルーチン。 FLT を返すことによって、preoperation コールバック ルーチンが下位のスタックの I/O 操作を渡す場合\_PREOP\_成功\_WITH\_コールバックまたは FLT\_PREOP\_格納できる同期ミニフィルター ドライバー定義によってポイントされている構造に変更されたパラメーターの値については、 *CompletionContext*出力パラメーター。 フィルター マネージャーでは、この構造体ポインターを渡す、 *CompletionContext* postoperation コールバック ルーチンへの入力パラメーター。

I/O 操作のパラメーターの詳細については、次を参照してください[ **FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)と[ **FLT\_IO。\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)します。

 

 




