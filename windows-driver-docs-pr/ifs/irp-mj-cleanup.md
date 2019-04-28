---
title: IRP_MJ_CLEANUP
description: IRP\_MJ\_CLEANUP
ms.assetid: e4593d99-a721-4ab1-82a5-b32b9c312b25
keywords:
- IRP_MJ_CLEANUP インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_CLEANUP
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3cfcac0ecd2fedb768c79e997c2d4e06fa4b0f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379712"
---
# <a name="irpmjcleanup"></a>IRP\_MJ\_CLEANUP


## <a name="when-sent"></a>送信時


IRP の受領書\_MJ\_クリーンアップ要求では、ファイル オブジェクトのハンドルの参照カウントがゼロに達したことを示します。 (つまり、ファイル オブジェクトへのすべてのハンドルが閉じられました。)多くの場合、ユーザー モード アプリケーションには、Microsoft Win32 が呼び出されたときに送信される**CloseHandle**関数 (カーネル モード ドライバーが呼び出されたときまたは[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)) 最後のファイル オブジェクトへの未処理のハンドル。

あるファイル オブジェクトへのすべてのハンドルが閉じられたときにこれは必ずしもファイル オブジェクトが不要になった使用されていることに注意してください。 重要です。 キャッシュ マネージャーや、メモリ マネージャーなどのシステム コンポーネントには、ファイル オブジェクトへの未解決の参照を保持可能性があります。 これらのコンポーネントの読み取りや IRP 後も、ファイルから作成できますも\_MJ\_クリーンアップ要求を受信します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ターゲット デバイス オブジェクトが、ファイル システムの制御デバイス オブジェクトの場合、ファイル システム ドライバーは IRP を完了する必要があります。

それ以外の場合、ファイル システム ドライバーは、クリーンアップ要求を処理する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


ターゲット デバイス オブジェクトが、フィルター ドライバーの制御デバイス オブジェクトの場合は、フィルター ドライバーは IRP を完了する必要があります。

それ以外の場合、フィルター ドライバーは、必要な処理を実行した後は、スタック上に次の下位ドライバー IRP を渡す必要があります。

ファイル システム フィルター ドライバー開発者が注意を[ **IoCreateStreamFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff548296) IRP が\_MJ\_クリーンアップ要求のファイル システム ドライバー スタックへの送信、ボリューム。 ファイル システム多くの場合、オブジェクトを作成ストリーム ファイル IRP 以外の操作の副作用としてため\_MJ\_作成、ストリームのファイル オブジェクトの作成を確実に検出するために、フィルター ドライバーに対することは困難です。 フィルター ドライバーは IRP を受信することしたがって\_MJ\_クリーンアップと IRP\_MJ\_閉じるが以前の見えないファイル オブジェクトを要求します。

フィルター ドライバー開発者も注意してくださいとは異なり[ **IoCreateStreamFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548296)、 [ **IoCreateStreamFileObjectLite** ](https://msdn.microsoft.com/library/windows/hardware/ff548306)しませんIRP が発生する\_MJ\_クリーンアップ要求をファイル システム ドライバー スタックに送信します。 このため、のでファイル システム多くの場合、ストリームのファイル オブジェクトの IRP 以外の操作の副作用として\_MJ\_作成、ストリームのファイル オブジェクトの作成を確実に検出するために、フィルター ドライバーに対することは困難です。 フィルター ドライバーは IRP を受信することしたがって\_MJ\_閉じるが以前の見えないファイル オブジェクトを要求します。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のクリーンアップ要求の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--flags"></a>*Irp-&gt;フラグ*  
この要求に対して、次のフラグが設定されます。

IRP\_閉じる\_操作

IRP\_同期\_API

<a href="" id="irp--iostatus"></a>*Irp -&gt;IoStatus*へのポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)に関する最終的な完了の状態および情報を受け取る、要求された操作。

<a href="" id="irpsp--fileobject"></a>*IrpSp -&gt;FileObject*に関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_クリーンアップ使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp -&gt;MajorFunction* IRP を指定します\_MJ\_クリーンアップします。

## <a name="see-also"></a>関連項目


[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoCreateStreamFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548296)

[**IoCreateStreamFileObjectLite**](https://msdn.microsoft.com/library/windows/hardware/ff548306)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_クリーンアップ (WDK カーネル リファレンス)**](https://msdn.microsoft.com/library/windows/hardware/ff550718)

[**IRP\_MJ\_CLOSE**](irp-mj-close.md)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

[**ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)

 

 






