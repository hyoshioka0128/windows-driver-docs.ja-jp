---
Description: クライアント コンテキストのサポート
title: クライアント コンテキストのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b227917f936a9f0a0136e786b06b4bd91ea39c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380853"
---
# <a name="supporting-client-contexts"></a>クライアント コンテキストのサポート


Windows ポータブル デバイス (WPD) ドライバーは、アプリケーション、および物理デバイス間の通信チャネルを提供します。 複数の WPD アプリケーションをいつでも実行できます。 ドライバーは、コンピューター上の別のクライアントからの要求を処理し、キューに置かれた要求に基づいてクライアントを識別する必要があります。 つまり、ドライバーには、接続ごとに、クライアントのデータを格納および要求時にデータを取得する、効率的かつ簡単な方法が必要があります。

ユーザー モード ドライバー Frameork (UMDF) は、コンテキストの領域を使用してこの機能をサポートしています。 汎用メカニズム、ドライバーがクライアント データを保存します。 WPD ドライバーには、データ構造体またはクライアントのデータを保持、framework オブジェクトのコンテキストの領域にデータ構造を割り当てる、後で、コンテキストを取得するオブジェクトを割り当てる必要があります。

適切な接続の WDF framework オブジェクトを使用するには、WDF ファイル オブジェクトを示します。

## <a name="span-idassigningthecontextspanspan-idassigningthecontextspanspan-idassigningthecontextspanassigning-the-context"></a><span id="Assigning_the_Context"></span><span id="assigning_the_context"></span><span id="ASSIGNING_THE_CONTEXT"></span>コンテキストの割り当てください。


ドライバーは、クライアント コンピューターへの接続を開いたときに、コンテキストを割り当てます。

WPD アプリケーションを呼び出すと、 **IPortableDevice::Open**または**IPortableDeviceService::Open** Win32 を使用して、メソッド、WPD API の作成、ドライバーを識別するハンドル**CreateFile**メソッド。 ドライバーにある、ユーザー モード ドライバー Frameork (UMDF) を初期化します、 **IWDFFile**オブジェクトし、ドライバーに、作成要求と共に転送**IQueueCallbackCreate::OnCreateFile**メソッド。 **IWDFFile**オブジェクトは、この場合、Win32 を表します**処理**ドライバーにこのクライアントからの後続の通信に使用されます。

例を見つけることができます、 **CreateFile** WpdWudfSampleDriver のコールバックの実装**CQueue::OnCreateFile**メソッド。 ドライバー固有の ContextMap COM オブジェクトは、(アプリケーション名、バージョン、実行中の列挙型とリソースのコンテキストおよびなど) のクライアント データの格納に使用されます。 オブジェクトの COM の使用を UMDF; がコンテキスト データを要求しないよう注意してください。UMDF としてコンテキスト データを表示する、 **PVOID**します。 コンテキスト データを格納する COM オブジェクトを使用する場合、ドライバーはその COM オブジェクトの参照カウントを維持し、適切なクリーンアップの方法でリソースを解放することを確認する必要があります。

ドライバー コンテキスト データを保存するには、新しい ContextMap オブジェクトを初期化しますを呼び出すと、 **IWDFObject::AssignContext**のメソッド、 **IWDFFile** UMDF によって渡されたオブジェクト。 このメソッドのパラメーターはへのポインター、 **IObjectCleanup**オブジェクトと新しく作成された ContextMap します。 **IObjectCleanup**オブジェクトにはコンテキストのクリーンアップ コードが含まれています。 新しく作成されたマップに格納されているデータが含まれています。 ドライバーの呼び出し、 **IObjectCleanup::OnCleanup**メソッド CloseHandle 中に、ファイル オブジェクトが破棄されるときにします。

さらに、1 つのみのコンテキストの場合は、ファイル オブジェクト (または任意の UMDF フレームワーク オブジェクト) に割り当てられていることができます。 後続の呼び出し、 **AssignContext**メソッドが失敗する場合は、コンテキストが既に割り当てられています。 追加またはクライアントに固有のデータの削除を動的に、ドライバーは、データを管理し、ファイル オブジェクトのコンテキストとそのオブジェクトへのポインターを割り当てるマッピング オブジェクトを実装できます。 例については、WpdWudfSampleDriver の ContextMap オブジェクトを参照してください。

## <a name="span-idretrievingandsavingcontextdataspanspan-idretrievingandsavingcontextdataspanspan-idretrievingandsavingcontextdataspanretrieving-and-saving-context-data"></a><span id="Retrieving_and_Saving_Context_Data"></span><span id="retrieving_and_saving_context_data"></span><span id="RETRIEVING_AND_SAVING_CONTEXT_DATA"></span>取得とコンテキスト データを保存


WPD ドライバーからコンテキストの取得要求中に、クライアントのデータにアクセスするには指定された**IWDFFile**オブジェクト。

検索順序は、次の手順で実施されます。

1.  ドライバーの呼び出し、 **IWDFIoRequest::GetFileObject**メソッドを取得する、 **IWDFFile**オブジェクト。
2.  ドライバーの呼び出し、 **IWDFObject::RetrieveContext**メソッドを**IWDFFile**コンテキスト領域にアクセスするオブジェクト。 コンテキストの領域がで作成された ContextMap オブジェクトへのポインターをサンプル ドライバーで**CQueue::OnCreateFile**アプリケーションが呼び出されたときに**IPortableDevice::Open**します。
3.  ドライバーは、データを追加または WPD コマンドを処理するときに、ContextMap オブジェクトからデータを直接削除します。 呼び出すことによって、アプリケーションが接続するたびに**IPortableDevice::Open**が、独自**IWDFFile**と ContextMap オブジェクト。

WpdWudfSampleDriver コンテキスト マップを取得し、クライアントの情報を追加する方法の例については、コードを参照してください。 次の表は、WpdWudfSampleDriver でコードを検索する場所について説明します。

| 例                                                                                                                  | ドライバーのサンプル内の場所           |
|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| WDF の要求に対するファイル オブジェクトからコンテキスト マップを取得しています。                                                     | **CQueue::OnDeviceIoControl**       |
| WPD を処理するときに、クライアントの情報をコンテキスト マップに追加する\_コマンド\_共通\_保存\_クライアント\_情報コマンド。 | **WpdBaseDriver::OnSaveClientInfo** |

 

## <a name="span-idreleasingthecontextspanspan-idreleasingthecontextspanspan-idreleasingthecontextspanreleasing-the-context"></a><span id="Releasing_the_Context"></span><span id="releasing_the_context"></span><span id="RELEASING_THE_CONTEXT"></span>コンテキストを解放します。


クライアント アプリケーションを呼び出すと、 **IPortableDevice::Close**メソッド、WPD API を呼び出します**CloseHandle**開いている接続に関連付けられている Win32 ハンドル。 UMDF を破棄する前に、 **IWDFFile**への応答オブジェクト、 **CloseHandle**、ファイル オブジェクトの呼び出し**IObjectCleanup::OnCleanup**に渡されるドライバー メソッド**AssignContext**中に**OnCreateFile**します。

実装例、 **IQueueCleanup**コールバックは、WpdWudfSampleDriver ドライバーの**CQueue::OnCleanup**メソッド。 このメソッドは、IWDFObject オブジェクトに格納されている ContextMap を取得します (ここでは、インスタンスから IWDFFile の**OnCreateFile**) し、ContextMap を保持するオブジェクトを含む、割り当てられたメモリを解放します。 メモリ リークを避けるためには、オブジェクトが適切にクリーンアップする、および (該当する) 場合は、参照カウントをデクリメントことを確認します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





