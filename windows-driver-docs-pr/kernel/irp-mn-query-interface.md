---
title: IRP_MN_QUERY_INTERFACE
description: IRP_MN_QUERY_INTERFACE 要求を使用すると、ドライバーは、直接呼び出しインターフェイスを他のドライバーにエクスポートできます。インターフェイスをエクスポートするバスドライバーは、子デバイス (子 PDOs) に対してこの要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: ae1dab46-c387-4e5f-9368-451e625ddbc1
keywords:
- IRP_MN_QUERY_INTERFACE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: f686fc93b945d5dfe3c7a633cef77a4ade731d77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838573"
---
# <a name="irp_mn_query_interface"></a>IRP\_\_クエリ\_インターフェイス


**IRP\_\_クエリ\_インターフェイス**要求を使用すると、ドライバーは直接呼び出しインターフェイスを他のドライバーにエクスポートできます。

インターフェイスをエクスポートするバスドライバーは、子デバイス (子 PDOs) に対してこの要求を処理する必要があります。 関数とフィルターは、必要に応じてこの要求を処理できます。

このコンテキストの "インターフェイス" は、1つ以上のルーチンと、場合によっては、ドライバーまたはドライバーのセットによってエクスポートされるデータで構成されます。 インターフェイスには、その内容とその型を識別する GUID を記述した構造体があります。

たとえば、pcmcia バスドライバーは、pcmcia メモリカードの書き込み禁止状態の取得などの操作のルーチンを含む、GUID\_PCMCIA\_インターフェイス\_標準のインターフェイスをエクスポートします。 このようなメモリカードの関数ドライバーは、 **IRP\_\_クエリ\_インターフェイス**要求を親の pcmcia バスドライバーに送信して、pcmcia インターフェイスルーチンへのポインターを取得できます。

このセクションでは、一般的なメカニズムとしてのクエリインターフェイスの IRP について説明します。 インターフェイスを公開するドライバーは、特定のインターフェイスに関する追加情報を提供する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

ドライバーまたはシステムコンポーネントは、デバイスのドライバーによってエクスポートされたインターフェイスに関する情報を取得するために、この IRP を送信します。

ドライバーまたはシステムコンポーネントは、任意のスレッドコンテキストで、IRQL = パッシブ\_レベルでこの IRP を送信します。

ドライバーは、デバイスに対してドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンが呼び出された後、いつでもこの IRP を受信できます。 この IRP が送信されるときに、デバイスが起動しない場合があります (つまり、ドライバーが正常に\_完了したことを前提として、デバイスに対する[ **\_デバイスの要求\_開始**](irp-mn-start-device.md)することはできません)。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_スタック\_の位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の**パラメーターの QueryInterface**メンバー自体が構造体であり、要求されているインターフェイスが記述されています。 構造体には、次の情報が含まれています。

```cpp
CONST GUID *InterfaceType;
USHORT Size;
USHORT Version;
PINTERFACE Interface;
PVOID InterfaceSpecificData
```

構造体のメンバーは、次のように定義されます。

<a href="" id="interfacetype"></a>**InterfaceType**  
は、要求されているインターフェイスを識別する GUID を指します。 Guid は、GUID\_バス\_インターフェイス\_標準、カスタムインターフェイスなどのシステム定義のインターフェイスに対して使用できます。 システム定義のインターフェイスの Guid は、Wdmguid .h に記載されています。 カスタムインターフェイスの Guid は、Uuidgen.exe を使用して生成する必要があります。

<a href="" id="size"></a>**幅**  
要求されるインターフェイスのサイズを指定します。 この IRP を処理するドライバーは、**サイズ**バイトを超える[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)構造を返すことはできません。

<a href="" id="version"></a>**バージョン**  
要求されるインターフェイスのバージョンを指定します。

ドライバーが複数のバージョンのインターフェイスをサポートしている場合、ドライバーは、要求されたバージョンを超えない限り、サポートされている最も近いバージョンを返します。 IRP を送信したコンポーネントは、返された**Interface. バージョン**フィールドを調べて、その値に基づいて何を行うかを決定する必要があります。

<a href="" id="interface"></a>**Efi**  
要求されたインターフェイスを返す構造体を指します。 この構造体には、最初のメンバーとして[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)構造が含まれている必要があります。 IRP を送信するコンポーネントは、ページングされたメモリからこの構造体を割り当てます。

インターフェイスをエクスポートするドライバーは、インターフェイス構造を含む新しい構造体型と、インターフェイスのルーチンやデータのメンバーを**定義します**。 (上記の**InterfaceType**メンバーで説明されているように、ドライバーはインターフェイスの GUID も定義します)。

インターフェイスをエクスポートするドライバーは、ルーチンを呼び出すことができる IRQL など、インターフェイス内の各ルーチンの実行環境を定義します。

<a href="" id="interfacespecificdata"></a>**InterfaceSpecificData**  
要求されているインターフェイスに関する追加情報を指定します。

一部のインターフェイスでは、IRP を送信するコンポーネントがこのフィールドに追加情報を指定します。 通常、このフィールドは**NULL**であり、要求されているインターフェイスを特定するには**InterfaceType**と**バージョン**が十分です。

## <a name="output-parameters"></a>出力パラメーター


成功した場合、ドライバーは、**パラメーター QueryInterface**構造体のメンバーを入力します。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS または適切なエラー状態に設定します。

成功した場合、バスドライバーは**Irp&gt;IoStatus. 情報**をゼロに設定します。

関数またはフィルタードライバーがこの IRP を処理しない場合は、 [**Ioskipfinalentifinallocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、次のドライバーに irp を渡します。 このようなドライバーでは、 **irp&gt;IoStatus. Status**を変更しないでください。 irp を完了することはできません。

バスドライバーが要求されたインターフェイスをエクスポートせず、子 PDO に対してこの IRP を処理しない場合、バスドライバーは**irp&gt;IoStatus**をそのままにして irp を完了します。

<a name="operation"></a>操作
---------

ドライバーは、ドライバーがサポートするインターフェイスをパラメーターが指定すると、この IRP を処理します。

ドライバーがサポートしていないインターフェイスを IRP が要求した場合、ドライバーはこの IRP をキューに置いてはなりません。 ドライバーは、 [**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の構造で**パラメーター**を確認する必要があります。 インターフェイスがドライバーでサポートされていない場合は、ドライバーが IRP をブロックせずに、デバイススタック内の次の下位のドライバーに渡す必要があります。

各インターフェイスは**InterfaceReference**および**interfacedereference 参照**ルーチンを提供する必要があり、インターフェイスをエクスポートするドライバーは、これらのルーチンのアドレスを[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)構造体に渡す必要があります。 ドライバーが IRP に応答してインターフェイスを返す前に、 **InterfaceReference**ルーチンを呼び出すことによって、インターフェイスの参照カウントをインクリメントする必要があります。 インターフェイスを要求したドライバーがそれを使用して終了した場合、そのドライバーは、インターフェイスの**Interfacedereference**参照ルーチンを呼び出すことによって、参照カウントをデクリメントする必要があります。

IRP (driver *x*) を送信するドライバーが後で別のドライバー (ドライバー *y*) にインターフェイスを渡す場合、ドライバー *x*はインターフェイスの参照カウントをインクリメントする必要があり、ドライバー *y*はそれをデクリメントする必要があります。

この IRP を処理するドライバーは、要求されたインターフェイスを取得するために、IRP を別のデバイススタックに渡すことを避ける必要があります。 このような設計では、管理が困難なデバイススタック間の依存関係が作成されます。 たとえば、2番目のデバイススタックで表されるデバイスは、最初のスタック内の適切なドライバーがインターフェイスを逆参照するまで削除できません。

インターフェイスは、バス固有またはバスに依存しない場合があります。 バス固有のインターフェイスは、これらのバスのヘッダーファイルで定義されています。 システムは、標準バスインターフェイスをエクスポートするために、バスに依存しないインターフェイスである[**bus\_interface\_standard**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)を定義します。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

この IRP は、デバイスの多層カーネルモードドライバー間でルーチンエントリポイントを渡すために特に使用されます。 この IRP によって公開されているインターフェイスを*デバイスインターフェイス*と混同しないでください。 デバイスインターフェイスは、主にユーザーモードコンポーネントまたはその他のカーネルコンポーネントによって使用されるデバイスへのパスを公開するために使用されます。 デバイスインターフェイスの詳細については、「[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)」を参照してください。

**この IRP を送信しています**

Irp の送信の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。 次の手順は、この IRP に特に適用されます。

-   ページプールから[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)構造を割り当て、0に初期化します。 インターフェイスが、インターフェイスコントラクトに基づいて IRQL &gt;= ディスパッチ\_レベルで呼び出される場合、呼び出し元は、非ページプールから割り当てられたメモリにコンテンツをコピーできます。

-   IRP の次の i/o スタックの場所の値を設定します: set **MajorFunction**を[**irp\_MJ\_PNP**](irp-mj-pnp.md)に設定し、 **minorfunction**を " **irp\_\_\_** " に設定して、適切な値**を設定します。パラメーター。 QueryInterface**。

-   **Iostatus を初期化します。** 状態は状態に\_\_サポートされていません。

-   不要になったときに、IRP と**インターフェイス**構造の割り当てを解除します。

-   インターフェイスの仕様で説明されているように、インターフェイスルーチンとコンテキストパラメーターを使用します。

-   インターフェイスが不要になったときに、 [*Interfacedereference*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pinterface_dereference)参照ルーチンを使用して参照カウントをデクリメントします。 インターフェイスを逆参照した後は、インターフェイスルーチンを呼び出さないでください。

通常、ドライバーは、ドライバーが接続されているデバイススタックの一番上にこの IRP を送信します。 ドライバーがこの IRP を別のデバイススタックに送信する場合、他のデバイスが、ドライバーがサービスを提供しているデバイスの先祖でない場合は、他のデバイスでターゲットデバイスの通知に対してドライバーを登録する必要があります。 このようなドライバーは、Eventcategory **Targetdevicechange**の*eventcategory*を使用して[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出します。 ドライバーは、種類が GUID\_ターゲット\_デバイス\_クエリ\_削除の通知を受信すると、ドライバーはインターフェイスを逆参照する必要があります。 ドライバーは、その後の GUID\_ターゲット\_デバイスが受信した場合に、そのインターフェイスの再クエリを実行して\_取り消された通知を削除\_ます。

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
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**バス\_インターフェイス\_STANDARD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)

[**EFI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)

[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

 

 




