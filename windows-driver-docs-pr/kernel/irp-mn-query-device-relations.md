---
title: IRP_MN_QUERY_DEVICE_RELATIONS
description: PnP マネージャーは、この要求を送信して、デバイス間の特定の関係を判断します。
ms.date: 08/12/2017
ms.assetid: 32437c5a-ad92-433c-8255-83775751a44d
keywords:
- IRP_MN_QUERY_DEVICE_RELATIONS カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 55884e623edc843a066488d474c8140effdeae4c
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922585"
---
# <a name="irp_mn_query_device_relations"></a>IRP\_の\_全\_クエリ\_のデバイスの関係


PnP マネージャーは、この要求を送信して、デバイス間の特定の関係を判断します。 この要求を処理するドライバーの種類は次のとおりです。

-   バスドライバーは、アダプターまたはコントローラー (bus FDO) の**Busrelations**要求を処理する必要があります。 フィルタードライバーは、 **Busrelations**要求を処理する場合があります。

-   バスドライバーは、子デバイス (子 PDOs) の**TargetDeviceRelation**要求を処理する必要があります。

-   関数ドライバーとフィルタードライバーは、 **RemovalRelations**および**powerrelations**要求を処理する場合があります。

-   バスドライバーは、子デバイス (子 PDOs) の**EjectionRelations**要求を処理する場合があります。

## <a name="value"></a>値

0x07

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、指定されたデバイスとの関係を持つデバイスに関する情報を収集するために、この IRP を送信します。

PnP マネージャーは、デバイスが列挙されたとき、デバイスがアクティブになっている間に、デバイスの**Busrelations** (子デバイス) に対してクエリを実行します。たとえば、ドライバーが[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)ルーチンを呼び出して子デバイスが到着したかどうかを示している場合などです。

PnP マネージャーは、デバイスのドライバーを削除する前に、デバイスの**RemovalRelations**を照会します。 PnP マネージャーは、デバイスを取り出す前に**RemovalRelations**と**EjectionRelations**を照会します。

PnP マネージャーは、ドライバーまたはユーザーモードアプリケーションがデバイス上の**Eventカテゴリ Targetdevicechange**の PnP 通知を登録するときに、デバイスの**TargetDeviceRelation**を照会します。 PnP マネージャーは、特定のファイルオブジェクトに関連付けられているデバイスを照会します。 Irp は、有効なファイルオブジェクトパラメーターを持つ唯一の PnP IRP です。 **\_\_\_\_** ドライバーは、 **TargetDeviceRelation**のデバイススタックを照会できます。 ドライバーは、 **TargetDeviceRelation**クエリを送信するときにファイルオブジェクトを提供する必要はありません。

PnP マネージャーは、デバイスのドライバーが**IoInvalidateDeviceRelations**を呼び出して、このデバイスが暗黙的な電源管理関係を持つデバイスのセットが変更されたことを示す場合に、デバイスの**powerrelations**を照会します。 **Powerrelations**要求は Windows 7 以降でサポートされています。

**Busrelations**、 **RemovalRelations**、 **EjectionRelations**、および**powerrelations**要求の場合、PnP マネージャーは、システムスレッドのコンテキストで、IRQL =\_パッシブレベルで IRP **\_を使用した\_\_クエリデバイス\_の関係**を送信します。

**TargetDeviceRelation**要求の場合、PnP マネージャーは、任意のスレッドコンテキストで\_この IRP を IRQL = パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造の**QueryDeviceRelations**メンバーは、クエリ対象のリレーションシップの種類を指定します。 指定できる値は、 **Busrelations**、 **EjectionRelations**、 **RemovalRelations**、 **TargetDeviceRelation**、および**powerrelations**です。

現在の**\_IO スタック\_の場所**構造体の**FileObject**メンバーは、 **QueryDeviceRelations**が**TargetDeviceRelation**の場合にのみ、有効なファイルオブジェクトを指しています。

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp-&gt;iostatus. status**を status\_に設定します。または、不足\_\_しているリソースの状態などのエラー状態に設定します。

成功すると、ドライバーは、要求された関係情報を指す PDEVICE\_リレーションポインターに**Irp-&gt;iostatus**を設定します。 **デバイス\_のリレーション**構造は、次のように定義されています。

```cpp
typedef struct _DEVICE_RELATIONS {
  ULONG  Count;
  PDEVICE_OBJECT  Objects[1];  // variable length
} DEVICE_RELATIONS, *PDEVICE_RELATIONS;
```

<a name="operation"></a>Operation
---------

この**IRP\_による\_クエリ\_デバイス\_の関係**に応じて、ドライバーが関係を返す場合、ドライバーは、カウントと適切な数のデバイスオブジェクトポインターを含むページメモリからデバイス**\_のリレーション**構造を割り当てます。 不要になったときに、PnP マネージャーによって構造が解放されます。 別のドライバーによって割り当てられた**デバイス\_の関係**構造をドライバーが置き換える場合、ドライバーは前の構造を解放する必要があります。

ドライバーは、この IRP ([**Obreferenceobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)) で報告されるすべてのデバイスの PDO を参照する必要があります。 必要に応じて、PnP マネージャーによって参照が削除されます。

関数またはフィルタードライバーは、デバイスの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンが完了した後であればいつでも、デバイスに対してこの IRP を処理できるように準備する必要があります。 バスドライバーは、デバイスが列挙された直後の**Busrelations**のクエリを処理できるように準備する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)の処理に関する一般的な規則については、[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)を参照してください。

次のサブセクションでは、さまざまなクエリを処理するための特定のアクションについて説明します。

**BusRelations 要求**

PnP マネージャーがアダプターまたはコントローラーのバス関係 (子デバイス) に対してクエリを行う場合、バスドライバーは、バス上に物理的に存在するすべてのデバイスの PDOs へのポインターの一覧を返す必要があります。 バスドライバーは、開始されているかどうかに関係なく、すべてのデバイスを報告します。 バスドライバーは、バスデバイスの電源を入れて、どの子が存在するかを判断することが必要になる場合があります。

**警告**  デバイスオブジェクトは、PnP マネージャーによってそのオブジェクトのデバイスノード (*devnode*) が作成されるまで、PDO を引数として受け取るルーチンに渡すことはできません。 (ドライバーがデバイスオブジェクトを渡す場合、システムはバグチェックを使用します。 [**0xCA: PNP\_が\_致命的\_なエラーを検出**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xca--pnp-detected-fatal-error)したことを確認します)。PnP マネージャーは、 **IRP\_devnode\_\_QUERY デバイス\_のリレーション**要求に応答して、その応答としてを作成します。 ドライバーは、 [**IRP\_\_devnode\_QUERY リソース\_要件**](irp-mn-query-resource-requirements.md)要求を受信すると、PDO のが作成されているものとしても安全です。

 

この IRP に応答するバスドライバーは、アダプターまたはコントローラーが接続されているバスの親バスドライバーではなく、バスアダプターまたはコントローラーの関数ドライバーです。 非バスデバイスの関数ドライバーは、このクエリを処理しません。 このようなドライバーは、IRP を次の下位のドライバーに渡すだけです。 (次の図を参照してください)。フィルタードライバーは、通常、このクエリを処理しません。

Windows Vista 以降のオペレーティングシステムでは、ドライバーは常に**irp\_の包括的な\_クエリ\_デバイス\_の関係**の irp を保留し、後で処理を完了することをお勧めします。 この順序を使用すると、システムはバス関係クエリを非同期的に処理できます。 (Windows Vista より前のオペレーティングシステムでは、ドライバーは\_ディスパッチルーチンから保留状態を安全に返すことができますが、PnP マネージャーは、他の操作とバス関係クエリと重複しません)。

次の図は、ドライバーがバスリレーションのクエリを処理する方法を示しています。

![バスリレーションのクエリを処理するドライバーを示す図](images/qdrstaks.png)

図に示されている例では、PnP マネージャーは、 **Busrelations**に対する**IRP\_の全\_クエリ\_デバイス\_の関係**を、USB ハブデバイスのドライバーに送信します。 PnP マネージャーは、ハブデバイスの子の一覧を要求しています。

1.  すべての PnP Irp と同様に、PnP マネージャーは、デバイスのデバイススタックの最上位のドライバーに IRP を送信します。

2.  オプションのフィルタードライバーは、スタック内の最上位のドライバーである可能性があります。 フィルタードライバーは通常、この IRP を処理しません。IRP をスタックに渡します。 フィルタードライバーは、この IRP を処理することがあります。たとえば、ドライバーが、バス上で非列挙型のデバイスを公開する場合などです。

3.  この IRP は、USB hub バスドライバーによって処理されます。

    USB ハブバスドライバー:

    -   まだ存在しないすべての子デバイスの PDO を作成します。

    -   バス上に存在しなくなったすべてのデバイスについて、PDO を非アクティブとしてマークします。 バスドライバーは、このような Dos を削除しません。 PDOs を削除するタイミングの詳細については、「[デバイスの](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)削除」を参照してください。

    -   バス上に存在するすべての子デバイスを報告します。

        各子デバイスに対して、バスドライバーは PDO を参照し、デバイス\_のリレーション構造に pdo へのポインターを書き込みます。

        この例では2つの PDOs があります。1つはジョイスティックデバイス用で、もう1つはキーボードデバイス用です。

        バスドライバーは、別のドライバーによって、この\_IRP のデバイスリレーション構造が既に作成されているかどうかを確認する必要があります。 その場合、バスドライバーは既存の情報にを追加する必要があります。

        バス上に子デバイスが存在しない場合、ドライバーはデバイス\_の関係構造でカウントを0に設定し、成功を返します。

    -   は、i/o 状態ブロックに適切な値を設定し、IRP を次の下位のドライバーに渡します。 アダプターまたはコントローラーのバスドライバーが IRP を完了していません。

4.  省略可能な下位フィルター (存在する場合) は、通常、この IRP を処理しません。 このようなフィルタードライバーは、IRP をスタックに渡します。 下位フィルタードライバーがこの IRP を処理する場合は、子デバイスの一覧に PDO を追加できますが、他のドライバーによって作成された PDOs を削除することはできません。

5.  親バスドライバーは、デバイススタック内の唯一のドライバーでない限り、この IRP を処理しません (デバイスは raw モードです)。 すべての PnP Irp と同様、親バスドライバーは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を使用して IRP を完了します。

    デバイススタックに1つまたは複数のバスフィルタードライバーがある場合、このようなドライバーは、バスドライバーに対して、または IRP によってデバイススタックをバックアップするように、IRP を処理することがあります ( [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンがある場合)。 PnP IRP 規則に従って、このようなドライバーでは、スタックの下位にある IRP に PDOs を追加したり、IRP の方法 ( *Iocompletion*ルーチン) で関係一覧を変更したりすることができます。

**EjectionRelations 要求**

ドライバーは、指定されたデバイスの取り出し時にシステムから物理的に削除される可能性があるすべてのデバイスの PDOs へのポインターを返します。 デバイスの子の PDOs を報告しないでください。PnP マネージャは常に、親デバイスの前に子デバイスを削除するように要求します。

PnP マネージャーは、追放されたデバイスに対して[**irp\_\_**](irp-mn-eject.md)の出力の irp を送信します。 このようなデバイスのドライバーも、削除 IRP を受け取ります。 デバイスの取り出しの関係は、irp によって[**\_\_\_削除**](irp-mn-remove-device.md)されたデバイスの irp を受信します ( **irp\_\_** を通した排出の irp ではありません)。

親バスドライバーだけが、その子デバイスの1つの**EjectionRelations**クエリに応答できます。 関数ドライバーとフィルタードライバーは、デバイススタック内の次に小さいドライバーに渡す必要があります。 バスドライバーがアダプターまたはコントローラーの関数ドライバーとしてこの IRP を受信した場合、バスドライバーは関数ドライバーのタスクを実行しているため、IRP を次の下位のドライバーに渡す必要があります。

**PowerRelations 要求**

Windows 7 以降では、 **Powerrelations**クエリを使用すると、ドライバーは、PnP 列挙をサポートする親バスとバス上の列挙子デバイスとの間の従来の関係とは別に、電源管理の関係を指定できます。 たとえば、バスドライバーがバス上の子デバイスを列挙できない場合、またはデバイスが複数のバスの子デバイスである場合、 **powerrelations**クエリでは、その子デバイスとバスまたはバスとの電源の関係を記述できます。

PnP マネージャーは、デバイスのドライバーが[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)ルーチンを呼び出し、 **Powerrelations**の*型*パラメーター値を指定すると、デバイスの**powerrelations**クエリを発行します。

このクエリに対する応答として、ターゲットデバイスのドライバー (つまり、クエリの対象であるデバイス) には、ターゲットデバイスの電源をオンにする前に、電源マネージャーによって電源をオンにする必要があるその他のデバイスの PDOs へのポインターを含む**デバイス\_リレーション**構造が用意されています。 逆に、これらの他のデバイスは、ターゲットデバイスがオフになった後にのみオフにする必要があります。 Power manager は、クエリの情報を使用して、これらのデバイスが正しい順序でオンまたはオフになっていることを保証します。

この順序保証は、グローバルシステムスリープ状態遷移にのみ適用されます。これには、S1、S2、S3 (*スリープ*)、S4 (*休止*)、および S5 (*シャットダウン*) システム電源の状態への移行が含まれます。 **Powerrelations**の順序保証は、システムが S0 (実行中) システム状態のままになっている間に、システムが S0 (*実行中*) システム状態のままである間は、Dx[デバイスの電源](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-the-directed-power-management-framework)状態遷移には適用されません。

ターゲットデバイスが特別なファイル (ページングファイル、休止ファイル、クラッシュダンプファイルなど) のデバイスパスにある場合、ターゲットデバイスのドライバーは、 **Inpath**が**TRUE**の場合、irp [**\_が発生した\_デバイス\_使用状況\_の通知**](irp-mn-device-usage-notification.md)irp を処理するときに追加の手順を実行する必要があります。 このドライバーは、 **Powerrelations**クエリに対して pdos が提供されているデバイスが、特別なファイルのデバイスパスにあることもサポートしている必要があります。 このサポートを確認するには、ターゲットデバイスのドライバーが、まず、各デバイスに**irp\_\_UsageNotification device\_USAGE\_NOTIFICATION** irp を送信する必要があります。また、この irp はターゲットデバイスと同じ**UsageNotification.Type**を指定する必要があります。 この IRP を受信したすべてのデバイスが正常な状態コードを使用して IRP を完了した場合にのみ、ターゲットデバイスのドライバーが**irp\_\_complete\_device USAGE\_NOTIFICATION** irp を正常に完了させることができます。 それ以外の場合、このドライバーはエラー状態コードを使用してこの IRP を完了する必要があります。

この同じドライバーが、 **inpath**が**FALSE**に設定されている irp **\_状態\_のデバイス\_使用状況\_通知**の irp を処理する場合、ドライバーは、 **Inpath**が**TRUE**の場合と同じ依存デバイスのセットに対して、irp **\_が使用されている\_デバイス\_使用状況\_の通知**を送信する必要があります。 ただし、 **Inpath**が**FALSE**の場合、ドライバーはこの IRP を失敗状態コードで完了させないようにする必要があります。

**Powerrelations クエリに**応答するドライバーは、 **Powerrelations**クエリに pdos が提供されているすべてのデバイスで、ターゲットデバイスの変更通知を登録する必要があります。 これらの通知に登録するために、ドライバーは[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)ルーチンを呼び出し、 *Eventcategory* **targetdevicechange**の eventcategory パラメーター値を指定できます。

**RemovalRelations 要求**

ドライバーは、指定されたデバイスのドライバーが削除されたときにドライバーを削除する必要があるすべてのデバイスの PDOs へのポインターを返します。 デバイスの子の PDOs を報告しないでください。PnP マネージャーは、デバイスを削除する前に子デバイスの削除を既に要求しています。

削除関係が削除される順序は定義されていません。

デバイススタック内のすべてのドライバーは、この種類の関係クエリを処理できます。 関数またはフィルタードライバーは、IRP を次の下位のドライバーに渡す前に処理します。 バスドライバーが IRP を処理し、それを完了します。

**TargetDeviceRelation 要求**

**TargetDeviceRelation**クエリを使用すると、pnp マネージャーは、ハードウェアを制御する pnp デバイススタック内の PDO の pnp 以外のデバイススタックを照会できます。

一般に、irp が特定のデバイススタックの一番下に到達するまで、 **irp\_\_\_\_** がいっぱいになったことをデバイスに送信するデバイスの関係が、ドライバーによって転送されます。 PnP 以外のスタックの一番下にあるドライバーは、IRP を関連する PnP スタックに転送または再発行します。 たとえば、PnP マネージャーは、ファイルシステムスタックの一番上にあるデバイスオブジェクト (pnp 以外のスタック) に**TargetDeviceRelation**クエリを送信する場合があります。 ファイルシステムスタック内の各デバイスオブジェクトは、クエリがスタックの一番下にあるデバイスオブジェクトに到達するまで、その下のデバイスオブジェクトにクエリを渡します。 スタック内の最も低いデバイスオブジェクトは、 **TargetDeviceRelation**クエリを PnP ストレージボリュームスタックの一番上にあるデバイスオブジェクトに転送または再発行します。その後、クエリはストレージボリュームスタックの一番下にある PDO に渡されます。

次の一覧は、PnP デバイススタックの一番下にある PDO へのポインターを安全に取得できる状況をまとめたものです。

-   PnP のデバイスオブジェクト

    PnP デバイススタック内のデバイスオブジェクトは、デバイスの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンが呼び出されたときにスタックの PDO を学習します。 [削除ロックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用して、ポインターを使用すると、受信した[**\_IRP\_\_**](irp-mn-remove-device.md)によってデバイスメッセージが正常に同期される場合、ドライバーは PDO へのポインターを安全にキャッシュできます。

-   スタックの一番下ではなく、非 PnP スタック内のデバイスオブジェクト

    PnP 以外のスタックの一番下にないデバイスオブジェクトの場合、ドライバーは**TargetDeviceRelation**クエリを送信して、対応する pnp デバイススタックの一番下にある PDO へのポインターを取得できます。

-   デバイスのファイルオブジェクト

    デバイスのファイルオブジェクトを指定すると、ドライバーは[**IoGetRelatedDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetrelateddeviceobject)を呼び出してデバイスオブジェクトを取得し、前のリスト項目の指示に従うことができます。

-   デバイスオブジェクトへのハンドル

    デバイスオブジェクトへのハンドルを指定すると、ドライバーは[**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)を呼び出してデバイスのファイルオブジェクトを取得し、前のリスト項目の指示に従うことができます。

親バスドライバーは、その子デバイスの**TargetDeviceRelation**リレーションクエリを処理する必要があります。 バスドライバーは、 [**Obreferenceobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)を使用して子デバイスの pdo を参照し、 **\_デバイスのリレーション**構造内の pdo へのポインターを返します。 このリレーションシップ型の構造体には PDO ポインターが1つだけあります。 PnP マネージャーは、ドライバーまたはアプリケーションがデバイス上で通知を受け取るために登録を解除するときに、PDO への参照を削除します。

**TargetDeviceRelation**クエリに応答するのは、親バスドライバーだけです。 関数ドライバーとフィルタードライバーは、デバイススタック内の次に小さいドライバーに渡す必要があります。 バスドライバーがアダプターまたはコントローラーの関数ドライバーとしてこの IRP を受信した場合、バスドライバーは関数ドライバーのタスクを実行しているため、IRP を次の下位のドライバーに渡す必要があります。

ドライバーが PDO ベースのスタックにない場合、ドライバーは、ドライバーが i/o を実行するファイルハンドルに関連付けられているデバイスオブジェクトに、新しいターゲットデバイス関係クエリ IRP を送信します。

**この IRP を送信しています**

ドライバーは、IRP**リレーション**を要求するために、IRP **\_の全\_クエリ\_デバイス\_の関係**を送信することはできません。 ドライバーは、この IRP を**RemovalRelations**または**EjectionRelations**に送信することを制限されていませんが、ドライバーがこれを行うとは限りません。

ドライバーは、 **TargetDeviceRelation**のデバイススタックを照会できます。 Irp の送信の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。 次の手順は、この IRP に特に適用されます。

-   次の i/o スタックの場所にある IRP: set **MajorFunction**を[**irp\_MJ\_PNP**](irp-mj-pnp.md)に設定し、 **Minorfunction**を**irp\_\_\_\_** に設定し、 **QueryDeviceRelations**を**TargetDeviceRelation**に設定し、 **IRP-&gt;FileObject**を有効なファイルオブジェクトに設定します。

-   **Iostatus を初期化します。** 状態はサポートされて\_いません\_。

ドライバーがこの IRP を送信して、ドライバーが受信した**TargetDeviceRelation**に対する irp **\_の\_完全\_な\_クエリデバイスの関係**に応じて pdo を報告する場合、ドライバーは pdo を報告し、irp の完了時に返されたリレーション構造を解放します。 ドライバーが別の理由でこの IRP を開始した場合、IRP が完了すると、ドライバーはリレーション構造を解放し、不要になったときに PDO を逆参照します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)

[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)

[**IoGetRelatedDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetrelateddeviceobject)

[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)

[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_\_デバイス\_使用量\_の通知**](irp-mn-device-usage-notification.md)

[**IRP\_の\_全取り出し**](irp-mn-eject.md)

[**IRP\_の\_全\_クエリ\_のリソース要件**](irp-mn-query-resource-requirements.md)

[**IRP\_の\_すべて\_のデバイスの削除**](irp-mn-remove-device.md)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**Obreferenceobject へ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)

[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)

 

 




