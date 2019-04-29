---
title: フレームワーク ファイル オブジェクト
description: フレームワーク ファイル オブジェクト
ms.assetid: 93ec5dd7-8ef0-4cea-9253-ea5d7869d4b8
keywords:
- I/O 要求の WDK KMDF、ファイル オブジェクト
- ファイル オブジェクト WDK KMDF
- 要求の WDK KMDF、ファイル オブジェクトの処理
- フレームワークは、WDK KMDF、ファイル オブジェクトをオブジェクトします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2b08ac687648f3747082f6f6d47a89ab26f3637
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391347"
---
# <a name="framework-file-objects"></a>フレームワーク ファイル オブジェクト





アプリケーションまたはドライバーは、デバイスへのアクセスを試みると、通常、作成するか、ファイルを開くオペレーティング システム ファイルの作成に要求を送信ドライバー スタック。 アプリケーションまたはドライバーがデバイスを使用して完了したら、システムはファイルのクリーンアップを送信し、ドライバー スタックへの要求を閉じます。 [要求の種類は](https://msdn.microsoft.com/library/windows/hardware/ff552503)これら 3 つの要求は**WdfRequestTypeCreate**、 **WdfRequestTypeCleanup**、および**WdfRequestTypeClose**、それぞれします。

通常、ドライバーが呼び出されていない限り[ **WdfDeviceInitSetExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff546097)ドライバーは、特定のファイルを実行する必要があります、またはその他のアクセスに特化した操作の受信時にファイルの作成、クリーンアップ、および閉じるファイルを複数開くことができる同時にまたは複数のアプリケーションでは、デバイスを同時にアクセスするために要求します。 ドライバーする必要がありますのでの追跡ファイルまたはアプリケーションに関連付けられている I/O 要求。

フレームワーク定義*framework ファイル オブジェクト*、表しますアプリケーションまたはファイル、ディレクトリ、ボリュームなどのデバイスにアクセスするためのドライバーの手段メール スロットは、名前付きパイプ、またはデバイス全体。 ファイル名は、ファイル オブジェクトを関連付けることができますが、ファイル名の意味は、ドライバー固有です。 ファイル名の詳細については、次を参照してください。[デバイス Namespace のアクセスを制御する](https://msdn.microsoft.com/library/windows/hardware/ff542068)します。

呼び出す必要がありますが、ドライバーは、ファイル操作を処理する必要がある場合、 [ **WdfDeviceInitSetFileObjectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff546107)内からその[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 **WdfDeviceInitSetFileObjectConfig**メソッドは受信、 [ **WDF\_FILEOBJECT\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551319)入力として構造体します。 ドライバーでは、この構造を使用して、登録、 [ *EvtDeviceFileCreate*](https://msdn.microsoft.com/library/windows/hardware/ff540868)、 [ *EvtFileCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff541700)、および[ *EvtFileClose* ](https://msdn.microsoft.com/library/windows/hardware/ff541702)コールバック関数と、必要に応じて、フレームワークを作成する必要があるかどうかを示すフレームワーク ファイル オブジェクトごとにドライバー ファイルの作成要求を受信します。

ファイル操作を処理するほとんどのドライバーが framework ファイル オブジェクトのファイルに固有の情報を格納[コンテキスト領域](framework-object-context-space.md)します。 ドライバーでファイルの操作を処理している場合、ファイル オブジェクトのコンテキストの領域に情報を格納する必要はありません、フレームワークがフレームワークに、ドライバーのファイル オブジェクトを作成する必要はありません。

### <a name="creating-or-opening-a-file"></a>作成またはファイルを開く

フレームワークは、関数のドライバーのファイルの作成要求を受け取ること。

1.  されていない限り、ドライバー以前 framework ファイル オブジェクトを使用する必要はありません、ファイルを表すフレームワーク ファイル オブジェクトを作成します。

2.  ドライバーの呼び出す[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)ドライバーには、コールバック関数が登録されている場合、コールバック関数。

[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)コールバック関数を通常[情報を取得する](#obtaining-file-information)その名前とファイル オブジェクト フラグなどのファイルについて。 ドライバーは、通常、この情報をフレームワークのファイル オブジェクトのコンテキストの領域に格納します。

指定する代わりに、 [ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)コールバック関数では、ドライバーが呼び出せる[ **WdfDeviceConfigureRequestDispatching** ](https://msdn.microsoft.com/library/windows/hardware/ff545920)を受信する I/O キューを設定するのには、すべてのファイルの作成要求 (**WdfRequestTypeCreate**要求の種類)。 ドライバーはキューのファイルの作成要求を受信後[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)要求ハンドラー。 (場合に、I/O キューがファイルの作成要求を受信できません、 **DefaultQueue**のキューのメンバー [ **WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)構造に設定されている**TRUE**)。

ドライバーが提供されていない場合、 [ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)コールバック関数と処理するために、I/O キューを設定しないは**WdfRequestTypeCreate**の I/O 要求の場合は、型指定された、フレームワーク:

-   状態のステータス値を持つドライバーのすべてのファイルの作成要求が完了すると\_成功した場合、ドライバーには関数の場合。

-   場合は、ドライバーは、フィルター ドライバーは、次の下位のドライバーにすべてのファイルの作成要求を転送します。

(この動作を変更する方法については、次を参照してください、 **AutoForwardCleanupClose**のメンバー、 [ **WDF\_FILEOBJECT\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551319)構造です。)。

**注**  関数には、ドライバーがいずれかを提供しない場合[デバイス インターフェイス](using-device-interfaces.md)こと、ドライバーのデバイスへのアクセスを使用するアプリケーション、ドライバーが提供する必要があります、 [ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)はすべて完了コールバック関数では、どの NT のステータス値を持つ作成要求を提出\_成功 (*状態*) と等しい**FALSE**. それ以外の場合、悪意のあるアプリケーションは、デバイスの物理デバイス オブジェクト (PDO) の名前を使用して、デバイスにアクセスしよう可能性があります。 (すべての Pdo が[名](controlling-device-access-in-kmdf-drivers.md#naming-device-objects-only-when-necessary))。

 

場合、ドライバー[転送](forwarding-i-o-requests.md)I/O のターゲットに作成要求、ドライバーはその必要が[完了](completing-i-o-requests.md)I/O からドライバーがエラー状態の値を受信されていない場合に、エラー状態が、要求が値ターゲット。 それ以外の場合、作成要求が失敗し、ファイルが開くように動作を試みること、下位のドライバーは通知されません。

ドライバーは、I/O のターゲットに作成要求を転送する場合、ドライバーは設定できません、 [ **WDF\_要求\_送信\_オプション\_送信\_AND\_破棄** ](https://msdn.microsoft.com/library/windows/hardware/ff552493)フレームワークが、framework のファイル オブジェクトの作成要求を作成した場合にフラグを設定します。 そのため、ドライバーは、WDF を設定できません\_要求\_送信\_オプション\_送信\_AND\_破棄フラグ作成の要求も設定しない限り、 [ **WdfFileObjectNotRequired** ](https://msdn.microsoft.com/library/windows/hardware/ff551315)フラグ。

ドライバーはエラー状態で作成要求が完了すると、フレームワーク フレームワーク ファイル オブジェクトを削除しますが、ドライバーは呼び出しません[ *EvtFileCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff541700)または[ *EvtFileClose* ](https://msdn.microsoft.com/library/windows/hardware/ff541702)コールバック関数。 そのため、ドライバー ファイル オブジェクトのコンテキストの領域外のオブジェクトに固有の余分なメモリを割り当てる場合は、提供する、 [ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)または[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)コールバック関数を割り当てられたメモリを削除します。

Windows Vista 以降、ファイルの作成要求ができる[キャンセル](canceling-i-o-requests.md)します。 以前のバージョンの Windows オペレーティング システムでは、ファイルの作成要求をキャンセルできません。

システムには、ユーザー アプリケーションから取得された各作成の要求のファイル オブジェクトを Windows Driver Model (WDM) を常に作成します。 ドライバーは、作成要求を送信する場合は、要求の WDM ファイル オブジェクトを作成、可能性がありますできません。 通常、WDM ファイル オブジェクトが存在しない場合、フレームワークはフレームワーク ファイル オブジェクトを作成できません。 ただし、ドライバーが呼び出された場合[ **WdfDeviceInitSetExclusive** ](https://msdn.microsoft.com/library/windows/hardware/ff546097)ドライバーを設定した場合と[ **WdfFileObjectWdfCannotUseFsContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff551315)で、 **FileObjectClass**のメンバー、 [ **WDF\_FILEOBJECT\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff551319)構造、フレームワークによって作成します。フレームワークのファイル オブジェクト場合でも、WDM ファイル オブジェクトが存在しません。

### <a href="" id="obtaining-file-information"></a> ファイル情報を取得します。

ドライバーの[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)コールバック関数は、1 つまたは複数のアプリケーションまたはデバイスへのドライバーのアクセスに関する情報を取得する次のオブジェクトのメソッドを呼び出すことができます。

<a href="" id="---------wdffileobjectgetfilename--------"></a>[**WdfFileObjectGetFileName**](https://msdn.microsoft.com/library/windows/hardware/ff547310)  
フレームワークのファイル オブジェクト内に含まれているファイル名を返します。

<a href="" id="---------wdffileobjectgetflags--------"></a>[**WdfFileObjectGetFlags**](https://msdn.microsoft.com/library/windows/hardware/ff547316)  
フレームワークのファイル オブジェクト内に含まれるフラグを返します。

<a href="" id="---------wdffileobjectwdmgetfileobject--------"></a>[**WdfFileObjectWdmGetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff547324)  
フレームワークのファイル オブジェクトに関連付けられている WDM ファイル オブジェクトを返します。

<a href="" id="---------wdfrequestgetparameters--------"></a>[**WdfRequestGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549969)  
フレームワークの要求オブジェクトに関連付けられているパラメーターを取得します。 場合、[要求の種類](https://msdn.microsoft.com/library/windows/hardware/ff552503)は**WdfRequestTypeCreate**、 **Parameters.Create**のメンバー、 [ **WDF\_要求\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff552472)構造体には、ファイルの作成要求に関する情報が含まれています。

通常、ドライバーは、フレームワーク ファイル オブジェクトのコンテキストの領域でファイル情報を格納します。 ドライバーを呼び出すことができます、ドライバーは、の I/O キュー、1 つの場合、I/O 要求を取得するときに[ **WdfRequestGetFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff549963)要求に関連付けられている framework ファイル オブジェクトを識別するハンドルを取得します。 ドライバーは、フレームワーク ファイル オブジェクトのコンテキストの領域に保存しておいたファイル情報を取得できます。

ドライバーは、呼び出すことによって、特定のファイルに関連付けられている要求のキューを I/O を検索できます[ **WdfIoQueueRetrieveRequestByFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548470)します。

ドライバー、WDM へのポインターがある場合[**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)構造体、ドライバーが呼び出せる[ **WdfDeviceGetFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff546007)WDM デバイス オブジェクトに関連付けられている framework ファイル オブジェクトを識別するハンドルを取得します。

### <a name="closing-a-file"></a>ファイルを閉じる

アプリケーションまたは別のドライバー ファイルを閉じると、フレームワークは、クリーンアップ要求と、ドライバーの終了要求を受信します。 フレームワーク:

1.  ドライバーの呼び出す[ *EvtFileCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff541700)と[ *EvtFileClose* ](https://msdn.microsoft.com/library/windows/hardware/ff541702)ドライバーがこれらのコールバックを登録した場合、コールバック関数関数。

2.  ファイルを表すフレームワーク ファイル オブジェクトを削除します。

ドライバーの[ *EvtFileCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff541700)と[ *EvtFileClose* ](https://msdn.microsoft.com/library/windows/hardware/ff541702)コールバック関数が framework ファイル オブジェクトへのハンドルを受信します。 ドライバーを呼び出すことができます[ **WdfFileObjectGetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff547302) framework デバイス オブジェクトが framework ファイルのオブジェクトに関連付けられたを確認します。

 

 





