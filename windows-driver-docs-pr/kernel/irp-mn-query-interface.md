---
title: IRP_MN_QUERY_INTERFACE
description: IRP_MN_QUERY_INTERFACE 要求には、他のドライバーを直接呼び出しインターフェイスをエクスポートするためのドライバーができるようにします。バス ドライバー インターフェイスをエクスポートするには、その子デバイス (子 Pdo) は、この要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: ae1dab46-c387-4e5f-9368-451e625ddbc1
keywords:
- IRP_MN_QUERY_INTERFACE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: d33afe8a8fc3e6f0030ade6ccc8fc60eb1c06955
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532270"
---
# <a name="irpmnqueryinterface"></a>IRP\_MN\_クエリ\_インターフェイス


**IRP\_MN\_クエリ\_インターフェイス**要求が他のドライバーを直接呼び出しインターフェイスをエクスポートするためのドライバーを使用します。

バス ドライバー インターフェイスをエクスポートするには、その子デバイス (子 Pdo) は、この要求を処理する必要があります。 関数とフィルターは、この要求を処理することができます必要に応じて。

このコンテキストで「インターフェイス」では、1 つまたは複数のルーチンと、場合によっては、ドライバーまたは一連のドライバーによってエクスポートされたデータで構成されます。 インターフェイスは、その内容とその型を識別する GUID を表す構造体を持ちます。

たとえば、PCMCIA バス ドライバーが GUID 型のインターフェイスをエクスポートします\_PCMCIA\_インターフェイス\_PCMCIA のメモリ カードの書き込み禁止条件の取得などの演算のルーチンを含む標準。 このようなメモリ カードの関数のドライバーを送信する、 **IRP\_MN\_クエリ\_インターフェイス**PCMCIA インターフェイスのルーチンへのポインターを取得する親 PCMCIA バス ドライバーに要求します。

このセクションでは、汎用的なメカニズムとしてクエリ インターフェイス IRP がについて説明します。 ドライバー インターフェイスを公開するには、その特定のインターフェイスに関する追加情報を提供する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

ドライバーまたはシステム コンポーネントは、デバイスのドライバーによってエクスポートされたインターフェイスに関する情報を取得するには、この IRP を送信します。

ドライバーまたはシステム コンポーネントでは、この IRP を送信 IRQL でパッシブ =\_任意のスレッド コンテキストでします。

ドライバーがドライバーの後にいつでもこの IRP を受信できる[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)デバイスのルーチンが呼び出されました。 デバイスの場合がありますまたはこの IRP が送信されるときに起動しない可能性があります (ドライバーが正常に完了したことを想定できません、 [ **IRP\_MN\_開始\_デバイス**](irp-mn-start-device.md)デバイスの要求)。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.QueryInterface**のメンバー、 [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)構造自体が構造体、について説明しますが、要求されているインターフェイス。 構造体には、次の情報が含まれています。

```cpp
CONST GUID *InterfaceType;
USHORT Size;
USHORT Version;
PINTERFACE Interface;
PVOID InterfaceSpecificData
```

構造体のメンバーの定義は次のとおりです。

<a href="" id="interfacetype"></a>**InterfaceType**  
要求されているインターフェイスを識別する GUID を指します。 GUID などのシステム定義のインターフェイスの GUID を指定できます\_BUS\_インターフェイス\_STANDARD、またはカスタム インターフェイスです。 システム定義のインターフェイスの Guid は、Wdmguid.h で一覧表示されます。 Uuidgen では、カスタム インターフェイスの Guid を生成する必要があります。

<a href="" id="size"></a>**サイズ**  
要求されているインターフェイスのサイズを指定します。 この IRP を処理するドライバーに返す必要がありますいないを[**インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff547825)構造よりも大きい**サイズ**バイト。

<a href="" id="version"></a>**バージョン**  
要求されているインターフェイスのバージョンを指定します。

ドライバーは、インターフェイスの 1 つ以上のバージョンをサポートする場合、ドライバーは、要求されたバージョンを超えずに最も近いサポートされているバージョンを返します。 IRP を送信するコンポーネントは、返された調べる必要があります**Interface.Version**フィールドし、その値に基づいて処理を決定します。

<a href="" id="interface"></a>**インターフェイス**  
要求されたインターフェイスが返される構造体をポイントします。 この構造体を含める必要があります、 [**インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff547825)その最初のメンバーとして構造体。 IRP を送信するコンポーネントは、ページングされたメモリからこの構造体を割り当てます。

新しい構造型含むインターフェイスをエクスポートするドライバーの定義、**インターフェイス**構造、およびルーチンまたはインターフェイス内のデータ メンバー。 (ドライバーは、インターフェイスの GUID も定義」の説明に従って、 **InterfaceType**メンバー、上記)。

インターフェイスをエクスポートするドライバーでは、位置、ルーチンを呼び出すことができます、IRQL を含め、インターフェイスなどの各ルーチンの実行環境を定義します。

<a href="" id="interfacespecificdata"></a>**InterfaceSpecificData**  
要求されているインターフェイスに関する追加情報を指定します。

いくつかのインターフェイスでは、IRP を送信するコンポーネントは、このフィールドの追加情報を指定します。 このフィールドは、通常、 **NULL**と**InterfaceType**と**バージョン**で要求されているインターフェイスを識別するために十分です。

## <a name="output-parameters"></a>出力パラメーター


成功した場合、ドライバーがのメンバーで塗りつぶす、 **Parameters.QueryInterface.Interface**構造体。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態にします。

成功した場合、バス ドライバーの設定**Irp -&gt;IoStatus.Information**をゼロにします。

呼び出す関数またはフィルター ドライバーがこの IRP を処理しない場合[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)し、[次へ] のドライバーに IRP を渡します。 このようなドライバーを変更する必要がありますいない**Irp -&gt;IoStatus.Status** IRP を完了する必要があります。

バス ドライバーでは、要求されたインターフェイスではエクスポートされませんし、そのため子 PDO のこの IRP を処理は、する場合は、バス ドライバーのまま**Irp -&gt;IoStatus.Status** IRP の完了であり。

<a name="operation"></a>操作
---------

ドライバーは、パラメーターは、インターフェイス、ドライバーのサポートを指定した場合、この IRP を処理します。

ドライバーは、IRP がドライバーがサポートされていないインターフェイスを要求した場合、この IRP をキューに配置しない必要があります。 ドライバーを確認する必要があります**Parameters.QueryInterface.InterfaceType**でその[ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)構造体。 インターフェイスでない場合、ドライバーを 1 つをサポートしています、ドライバーは、[次へ] の下ドライバー デバイス スタックに IRP をブロックすることがなく渡す必要があります。

各インターフェイスを提供する必要があります**InterfaceReference**と**InterfaceDereference**ルーチン、およびドライバー インターフェイスをエクスポートするでこれらのルーチンのアドレスを指定する必要があります、 [**インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff547825)構造体。 呼び出すことによって、インターフェイスの参照カウントを増やす必要があります、ドライバーは IRP への応答でインターフェイスを返します、前にその**InterfaceReference**ルーチン。 インターフェイスを要求したドライバーの使用が完了したら、そのドライバーが呼び出してインターフェイスの参照カウントをデクリメントする必要があります**InterfaceDereference**ルーチン。

ドライバーは IRP を送信する場合 (ドライバー *x*) 後で、インターフェイスを別のドライバーに渡します (ドライバー *y*) し、ドライバー *x*インターフェイスの参照カウントを増やす必要があり、ドライバー *y*デクリメントする必要があります。

この IRP を処理するドライバーは IRP を要求されたインターフェイスを取得するもう 1 つのデバイス スタックに渡すことを避ける必要があります。 このような設計では、管理が困難であるデバイス スタック間の依存関係を作成します。 たとえば、最初のスタックの適切なドライバーが、インターフェイスを逆参照されるまでは、2 つ目のデバイス スタックによって表されるデバイスを削除できません。

インターフェイスには、bus 固有またはバスに依存しないを指定できます。 バスに固有のインターフェイスは、それらのバスのヘッダー ファイルで定義されます。 システムは、バスに依存しないインターフェイスを定義[ **BUS\_インターフェイス\_標準**](https://msdn.microsoft.com/library/windows/hardware/ff540707)、標準バス インターフェイスをエクスポートします。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

複数層のカーネル モード デバイス ドライバーの間で日常的なエントリ ポイントを渡すためには、具体的には、この IRP が使用されます。 この IRP によって公開されるインターフェイスを混同しないでください*デバイス インターフェイス*します。 デバイスのインターフェイスは、ユーザー モード コンポーネントまたはその他のカーネル コンポーネントで使用するためのデバイスへのパスを公開するためには、主に使用されます。 デバイス インターフェイスの詳細については、次を参照してください。[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)します。

**この IRP を送信します。**

参照してください[Irp の処理](https://msdn.microsoft.com/library/windows/hardware/ff546847)Irp を送信する方法について。 この IRP に具体的には、次の手順が適用されます。

-   割り当て、 [**インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff547825)ページ プールから構造体し、ゼロに初期化します。 インターフェイスは IRQL で呼び出せる場合&gt;= ディスパッチ\_レベル、インターフェイス コントラクトに基づき、呼び出し元にコピーできます内容非ページ プールから割り当てられたメモリ。

-   IRP の I/O スタック内の次の場所の値を設定します設定**MajorFunction**に[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)設定 **。MinorFunction**に**IRP\_MN\_クエリ\_インターフェイス**、適切な値を設定および**Parameters.QueryInterface**します。

-   初期化**IoStatus.Status**ステータス\_いない\_サポートされています。

-   IRP の割り当てを解除し、**インターフェイス**不要になったときに構造体します。

-   インターフェイスの仕様」の説明に従って、インターフェイスのルーチンとコンテキスト パラメーターを使用します。

-   使用してその参照カウントをデクリメント、 [ *InterfaceDereference* ](https://msdn.microsoft.com/library/windows/hardware/ff547829)ルーチン インターフェイスが不要になったとき。 インターフェイスを逆参照した後は、インターフェイス ルーチンを呼び出さないでください。

ドライバーでは、この IRP がドライバーが接続されているデバイス スタックの一番上に通常送信します。 ドライバーは、この IRP を別のデバイス スタックに送信する場合、ドライバーを他のデバイス上のターゲット デバイスの通知の登録する必要がある場合は、その他のデバイスは、ドライバーが処理しているデバイスの先祖ではありません。 このようなドライバーを呼び出す[ **IoRegisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff549526)で、*によって*の**EventCategoryTargetDeviceChange**します。 ドライバーが GUID 型の通知を受信すると\_ターゲット\_デバイス\_クエリ\_REMOVE、ドライバー インターフェイス参照を解除する必要があります。 後続の GUID を受信した場合、ドライバーが、インターフェイスの requery できます\_ターゲット\_デバイス\_削除\_キャンセル通知します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**バス\_インターフェイス\_標準**](https://msdn.microsoft.com/library/windows/hardware/ff540707)

[**インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff547825)

[**IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)

 

 




