---
title: IRP_MN_QUERY_DEVICE_RELATIONS
description: PnP マネージャーでは、デバイス間の特定の関係を判断するには、この要求を送信します。
ms.date: 08/12/2017
ms.assetid: 32437c5a-ad92-433c-8255-83775751a44d
keywords:
- IRP_MN_QUERY_DEVICE_RELATIONS カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 6e655cbf8e96102d7a3b388eb7c0990ab0863d41
ms.sourcegitcommit: 46654c090f937923d9712de114fdebe7deffeaaf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427694"
---
# <a name="irpmnquerydevicerelations"></a>IRP\_MN\_クエリ\_デバイス\_リレーション


PnP マネージャーでは、デバイス間の特定の関係を判断するには、この要求を送信します。 次の種類のドライバーでは、この要求を処理します。

-   バス ドライバーを処理する必要があります**BusRelations**アダプターまたはコント ローラー (バス FDO) を要求します。 フィルター ドライバーが処理**BusRelations**要求。

-   バス ドライバーを処理する必要があります**TargetDeviceRelation**子デバイス (子 Pdo) を要求します。

-   関数とフィルター ドライバーが処理**RemovalRelations**と**PowerRelations**要求。

-   バス ドライバーが処理**EjectionRelations**子デバイス (子 Pdo) を要求します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、指定したデバイスに関係を持つデバイスに関する情報を収集するには、この IRP を送信します。

PnP マネージャー クエリ、デバイスの**BusRelations** (子デバイス)、デバイスが列挙され、デバイスの中に、それ以外の時間がアクティブで、ドライバーを呼び出す場合など、 [ **IoInvalidateDeviceRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)ルーチンを子デバイスが到着したまたはゲームを終了したことを示します。

PnP マネージャー クエリ、デバイスの**RemovalRelations**前に、デバイスのドライバーを削除します。 PnP マネージャーをクエリ**RemovalRelations**と**EjectionRelations**デバイスを取り出す前にします。

PnP マネージャー クエリ、デバイスの**TargetDeviceRelation**の PnP 通知ドライバーまたはユーザー モード アプリケーションを登録するときに、 **EventCategoryTargetDeviceChange**デバイスにします。 特定のファイル オブジェクトに関連付けられているデバイスの PnP マネージャー クエリです。 **IRP\_MN\_クエリ\_デバイス\_リレーション**は有効なファイル オブジェクトのパラメーターを持つ PnP IRP ののみです。 ドライバーのデバイス スタックを照会できます**TargetDeviceRelation**します。 ドライバーが送信するときに、ファイル オブジェクトを指定する必要はありません、 **TargetDeviceRelation**クエリ。

PnP マネージャー クエリ、デバイスの**PowerRelations** 、デバイスのドライバーを呼び出すと**IoInvalidateDeviceRelations**ことを示す一連のデバイスがこのデバイスには、暗黙的な電源管理の関係が変更されました。 **PowerRelations**要求には、Windows 7 以降ではサポートされています。

**BusRelations**、 **RemovalRelations**、 **EjectionRelations**、および**PowerRelations** PnP マネージャー送信要求します。**IRP\_MN\_クエリ\_デバイス\_リレーション**IRQL = パッシブ\_システム スレッドのコンテキスト内のレベル。

**TargetDeviceRelation**要求、PnP マネージャー IRQL でこの IRP の送信 = パッシブ\_任意のスレッド コンテキストのレベル。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.QueryDeviceRelations.Type**のメンバー、 [ **IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)構造体のリレーションの種類を指定します。照会中します。 指定できる値は**BusRelations**、 **EjectionRelations**、 **RemovalRelations**、 **TargetDeviceRelation**、および**PowerRelations**します。

**FileObject** 、現在のメンバー **IO\_スタック\_場所**場合のみ有効なファイル オブジェクトへのポインターを構造体**Parameters.QueryDeviceRelations.Type**は**TargetDeviceRelation**します。

## <a name="output-parameters"></a>出力パラメーター


状態の I/O ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功や状態などのエラー状態に\_不十分\_リソース。

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information** 、PDEVICE に\_リレーションシップの要求された情報を指すリレーションのポインター。 **デバイス\_リレーション**構造は次のように定義されます。

```cpp
typedef struct _DEVICE_RELATIONS {
  ULONG  Count;
  PDEVICE_OBJECT  Objects[1];  // variable length
} DEVICE_RELATIONS, *PDEVICE_RELATIONS;
```

<a name="operation"></a>操作
---------

ドライバーは、これに対する応答で関係を返す場合、 **IRP\_MN\_クエリ\_デバイス\_リレーション**、ドライバーを割り当てます、**デバイス\_リレーション**からページングされたメモリの数、およびデバイス オブジェクト ポインターの適切な数を含む構造体。 PnP マネージャーは、不要になったときに、構造体を解放します。 ドライバーが置き換えられた場合、**デバイス\_リレーション**割り当てられているその他のドライバーを構造体をドライバーは、以前の構造体を解放する必要があります。

ドライバーは、この IRP でレポートされる任意のデバイスの PDO を参照する必要があります ([**ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject))。 PnP マネージャーは、該当する場合に参照を削除します。

関数またはフィルター ドライバーは、後にいつでもこの IRP のデバイスを処理するために準備する必要があります、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)デバイスのルーチンが完了しました。 クエリを処理するために、バス ドライバーを準備する必要があります**BusRelations**デバイスが列挙された後すぐにします。

処理の一般的な規則について[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)を参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)します。

次のサブセクションでは、さまざまなクエリを処理するための特定のアクションについて説明します。

**BusRelations 要求**

コント ローラーのアダプター バス リレーション (子デバイス) の PnP マネージャー クエリ、バス ドライバー返す必要がありますのポインターのリストの任意のデバイスの Pdo を物理的にするときは、バスに提示します。 バス ドライバーでは、起動されたかどうかに関係なく、すべてのデバイスを報告します。 バス ドライバーは、そのバス デバイスの電源を投入する子が存在するかを判断する必要があります。

**警告**  デバイス オブジェクトは、引数としての PDO を PnP マネージャーで、[デバイス] ノードが作成されるまで任意のルーチンに渡されることはできません (*devnode*) そのオブジェクト。 (システムはバグに確認の場合は、ドライバーがデバイス オブジェクトを渡すと、 [ **0 xca のバグ チェック。PNP\_検出\_FATAL\_エラー**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xca--pnp-detected-fatal-error))。PnP マネージャーへの応答で devnode を作成し、 **IRP\_MN\_クエリ\_デバイス\_リレーション**要求。 ドライバーを受信したときに PDO の devnode が作成されていると想定できる、 [ **IRP\_MN\_クエリ\_リソース\_要件**](irp-mn-query-resource-requirements.md)要求。

 

この IRP に応答するバス ドライバーとは、関数のドライバー、バス アダプタまたはコント ローラーを親バス ドライバーではなく bus アダプターまたはコント ローラーに接続しているのです。 バスではないデバイスの機能のドライバーでは、このクエリは処理されません。 このようなドライバーは、[次へ] の下のドライバーに IRP を渡すだけです。 (詳しくは、次の図を参照してください)。通常、フィルター ドライバーでは、このクエリは処理されません。

Windows Vista およびそれ以降のオペレーティング システムでは、ことをお勧めドライバー保留常に、 **IRP\_MN\_クエリ\_デバイス\_リレーション**IRP 後でその処理を完了します。 この順序により、バスのリレーションのクエリを非同期に処理するシステムです。 (Windows Vista より前に、のオペレーティング システム、ドライバーは安全に状態を返す\_ディスパッチ ルーチンが PnP マネージャーからの保留が他の操作とバスの関係のクエリと重複しない)。

次の図は、ドライバーがバス リレーションのクエリを処理する方法を示します。

![ドライバーのバスは、関連付けクエリの処理を示す図](images/qdrstaks.png)

PnP マネージャーが送信の図に示す例で、 **IRP\_MN\_クエリ\_デバイス\_リレーション**の**BusRelations**のドライバーをUSB ハブのデバイスです。 PnP マネージャーでは、ハブのデバイスの子の一覧を要求しています。

1.  すべての PnP Irp としてに、PnP マネージャーは、デバイスのデバイス スタックの最上位のドライバーを使用して、IRP を送信します。

2.  オプションのフィルター ドライバー スタックの最上位のドライバーがあります。 フィルター ドライバーは通常、この IRP; を処理しません下位のスタック IRP が渡されます。 フィルター ドライバーが、この IRP では、ドライバー、バス上の列挙可能でないデバイスを公開している場合などの処理。

3.  USB ハブのバス ドライバーは IRP を処理します。

    USB ハブ バス ドライバー:

    -   既にない任意の子デバイス用の PDO を作成します。

    -   バス上に存在しないすべてのデバイスの非アクティブの PDO をマークします。 バス ドライバーの Pdo を削除するタイミングの詳細については「このような PDOs.For は削除されません[デバイスを削除する](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)します。

    -   バス上に存在するすべての子デバイスを報告します。

        子デバイスごとに、バス ドライバーは、PDO を参照し、デバイスで PDO にポインターを与えます\_リレーション構造体。

        この例である 2 つの Pdo: ジョイスティック デバイスとキーボード デバイスのいずれかのいずれか。

        バス ドライバーが別のドライバーが既にデバイスを作成するかどうかを確認する必要があります\_この IRP の関係の構造体。 場合は、バス ドライバーは、既存の情報を追加する必要があります。

        ドライバーがデバイスでゼロにカウントを設定、バス上に存在する子デバイスがない場合は、\_リレーションの構造体、成功を返します。

    -   状態の I/O ブロックで適切な値を設定し、[次へ] の下位のドライバーを IRP を渡します。 アダプターまたはコント ローラーのバス ドライバーは IRP を完了できません。

4.  省略可能な下位のフィルター、存在する場合、通常は処理されませんこの IRP。 このようなフィルター ドライバーは IRP が下位のスタックを渡します。 低いフィルター ドライバーは、この IRP を処理する場合は、PDO(s) 子デバイスの一覧に追加できますが、他のドライバーによって作成された任意の Pdo を削除する必要があります。

5.  親のバス ドライバー (デバイスでは、raw モードで) デバイス スタックでのみ、ドライバーである場合を除き、この IRP を処理しません。 すべての PnP Irp の親のバス ドライバーは IRP が完了すると[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。

    このようなドライバーが IRP バス ドライバー下方向や IRP デバイス stack のバックアップ方法を処理デバイス スタックの 1 つまたは複数のバス フィルター ドライバーがある場合 (ある場合[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンの場合)。 このようなドライバー Pdo を下位のスタックの IRP に追加や、IRP スタックのバックアップ方法でリレーションシップの一覧を変更する PnP IRP の規則に従って (で*IoCompletion*ルーチン)。

**EjectionRelations 要求**

ドライバーは、指定されたデバイスを取り出すときに、システムから物理的に削除された可能性がありますすべてのデバイスの Pdo をポインターを返します。 デバイスの子の Pdo を報告しません。PnP マネージャーでは、親デバイスする前に、子のデバイスを削除することを常に要求します。

PnP マネージャーに送信、 [ **IRP\_MN\_取り出し**](irp-mn-eject.md) IRP が排出されるデバイスにします。 このようなデバイスのドライバーでは、削除 IRP も受け取ります。 デバイスの取り出しの関係が表示される、 [ **IRP\_MN\_削除\_デバイス**](irp-mn-remove-device.md) IRP (いない、 **IRP\_MN\_取り出す**IRP)。

親のバス ドライバーのみが応答できる、 **EjectionRelations**その子デバイスのいずれかのクエリ。 関数とフィルター ドライバーをデバイス スタックの次の下位のドライバーに渡す必要があります。 バス ドライバーでは、そのアダプターまたはコント ローラーの機能のドライバーとしてこの IRP を受信する場合、バス ドライバーは function ドライバーのタスクを実行してを次の下位のドライバーは IRP を渡す必要があります。

**PowerRelations 要求**

Windows 7 では、以降では、 **PowerRelations**クエリにより、PnP 列挙をサポートする親バスと、列挙子の間の従来のリレーションシップの外部で電源管理関係を指定するためのドライバーバス上のデバイス。 たとえば、バス ドライバー、バス上の子デバイスを列挙できませんでした。 場合、またはデバイスの場合は 1 つ以上のバスの子、 **PowerRelations**クエリは、バスのバスと子デバイスの電源の関係を記述できます。

PnP マネージャーの問題、 **PowerRelations** 、デバイスのドライバーを呼び出すと、デバイスのクエリ、 [ **IoInvalidateDeviceRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)ルーチンをを指定します*型*のパラメーター値**PowerRelations**します。

このクエリに応答して、ターゲット デバイス (クエリの対象となっているデバイス) のドライバーが提供する**デバイス\_リレーション**する必要があるその他のデバイスの Pdo へのポインターを含む構造体電源マネージャーで前に、ターゲット デバイスの電源をオンします。 逆に、ターゲット デバイスがオフにした後にのみこれらの他のデバイスをオフにする必要があります。 電源マネージャーは、これらのデバイスが有効になっているオンとオフを正しい順序で保証するために、クエリからの情報を使用します。

この順序は保証と、S1、S2、S3 の間の遷移を含むグローバル システム スリープ状態遷移にのみ適用されます (*スリープ*)、S4 (*休止*)、および S5 (*シャットダウン*)システム電源の状態。 **PowerRelations** Dx デバイスの電源の状態遷移には、システムが、S0 のままという保証は適用されませんを順序付け (*を実行している*) システムの場合を除く状態、[ダイレクト実行時の電源管理 (DFx)](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-the-directed-power-management-framework)遷移します。

ターゲット デバイスがデバイスの特別なファイルのパスにある場合 (など、ページング ファイル、休止状態ファイル、またはクラッシュ ダンプ ファイル)、処理する場合、ターゲット デバイスのドライバーは、追加の手順を実行する必要があります、 [ **IRP\_MN\_デバイス\_使用状況\_通知**](irp-mn-device-usage-notification.md)を IRP **InPath**は**TRUE**します。 このドライバーことを確認しますが Pdo は指定されたデバイス、 **PowerRelations**クエリは、特殊なファイルのデバイス パスになることもサポートできます。 このサポートを確認するには、ターゲット デバイスのドライバーを送信する必要があります最初、 **IRP\_MN\_デバイス\_使用状況\_通知**IRP をそれぞれのデバイス、およびこの IRP を指定する必要があります同じ**UsageNotification.Type**ターゲット デバイスとして。 この IRP を受信するすべてのデバイスが、成功状態コード IRP を完了する場合にのみ完全なターゲット デバイスのドライバーをことができますその**IRP\_MN\_デバイス\_使用状況\_通知**。IRP が正常にします。 それ以外の場合、このドライバーはエラー状態コードでは、この IRP を完了する必要があります。

この同じドライバーを処理すると、 **IRP\_MN\_デバイス\_使用状況\_通知**を IRP **InPath**は**FALSE**、ドライバーを送信する必要があります、 **IRP\_MN\_デバイス\_使用状況\_通知**IRP でどのしまったとしても依存しているデバイスの同じセットを**InPath**は**TRUE**します。 ただし、ドライバーにはエラー状態では、この IRP が完了する必要がありますしないときにコード**InPath**は**FALSE**します。

応答するドライバー、 **PowerRelations**クエリは、ターゲット デバイスの変更通知が Pdo は指定されたすべてのデバイスで登録する必要があります、 **PowerRelations**クエリ。 これらの通知に登録するドライバーを呼び出すことができます、 [ **IoRegisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)ルーチンを指定し、*によって*のパラメーター値**EventCategoryTargetDeviceChange**します。

**RemovalRelations 要求**

ドライバーは、指定したデバイスのドライバーが削除されたときに、ドライバーを削除する必要がすべてのデバイスの Pdo をポインターを返します。 デバイスの子の Pdo を報告しません。PnP マネージャーは、既にデバイスを削除する前に子デバイスの削除を要求します。

リレーションシップを削除する削除の順序は定義されません。

デバイス スタック内の任意のドライバーでは、この種類の関係のクエリを処理できます。 関数またはフィルター ドライバーは、[次へ] の下のドライバーに渡す前に、IRP を処理します。 バス ドライバーは IRP を処理し、それを完了します。

**TargetDeviceRelation 要求**

**TargetDeviceRelation**クエリにより、ハードウェアを制御する PnP デバイス スタックで PDO 非 PnP デバイス スタックを照会する PnP マネージャー。

ドライバーを一般に、転送、 **IRP\_MN\_クエリ\_デバイス\_リレーション**IRP IRP が特定のデバイス履歴の下端に達するまで、スタック ダウンします。 非 PnP スタックの下部にあるドライバーは、転送し、または関連する PnP スタックに IRP を再発行します。 たとえば、PnP マネージャーは送信、 **TargetDeviceRelation**非 PnP スタックは、ファイル システム スタックの上部にあるデバイス オブジェクトをクエリします。 ファイル システム スタック内の各デバイス オブジェクトが下にあるデバイス オブジェクトにファイルが、クエリ スタックの一番下にあるデバイス オブジェクトに到達するまでに、クエリを渡します。 スタックの一番下のデバイス オブジェクトは転送を再実行するか、 **TargetDeviceRelation** PnP 記憶域ボリュームのスタックの上部にあるデバイス オブジェクトをクエリし、クエリに渡される、記憶域の下部にある PDOボリュームのスタックです。

次の一覧を PnP デバイス スタックの下部にある PDO へのポインターを取得することが安全に状況をまとめたものです。

-   PnP デバイス オブジェクト

    PnP デバイス スタック内のデバイス オブジェクトがスタックの PDO を学習時に、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)デバイスのルーチンが呼び出されます。 ポインターの使用が適切に受信される同期されている場合、ドライバーは PDO へのポインターをキャッシュに安全にできます[ **IRP\_MN\_削除\_デバイス**](irp-mn-remove-device.md)メッセージ使用して、[削除ロック ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

-   スタックの一番下ではなく、非 PnP スタック内のデバイス オブジェクト

    ドライバーを送信するは、非 PnP スタックの一番下にないデバイス オブジェクトを**TargetDeviceRelation**を対応する PnP デバイス スタックの下部にある PDO へのポインターを取得するクエリ。

-   デバイスのファイル オブジェクト

    ドライバーを呼び出すことができます、ファイル オブジェクトを指定すると、デバイスの[ **IoGetRelatedDeviceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetrelateddeviceobject)をデバイス オブジェクトを取得し、上記のリスト アイテムでの指示に従います。

-   デバイス オブジェクトをハンドルします。

    ドライバーを呼び出すことができます、ハンドルを指定すると、デバイス オブジェクト、 [ **ObReferenceObjectByHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)をデバイスのファイル オブジェクトを取得し、上記のリスト アイテムでの指示に従います。

親のバス ドライバーを処理する必要があります、 **TargetDeviceRelation**リレーションがその子デバイスを照会します。 バス ドライバーの参照に子デバイスの PDO [ **ObReferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)で PDO へのポインターを返します、**デバイス\_リレーション**構造体。 このリレーションシップ型、構造体で 1 つだけの PDO ポインターがあります。 PnP マネージャーは、デバイスに通知をドライバーまたはアプリケーションの登録を解除するときに PDO への参照を削除します。

親のバス ドライバーのみに応答する、 **TargetDeviceRelation**クエリ。 関数とフィルター ドライバーをデバイス スタックの次の下位のドライバーに渡す必要があります。 バス ドライバーでは、そのアダプターまたはコント ローラーの機能のドライバーとしてこの IRP を受信する場合、バス ドライバーは function ドライバーのタスクを実行してを次の下位のドライバーは IRP を渡す必要があります。

ドライバーがない場合、ドライバー PDO ベースのスタックに送信します新しいターゲット デバイス関係は、ドライバーが I/O を実行して、ファイル ハンドルに関連付けられているデバイスのオブジェクトに IRP をクエリします。

**この IRP を送信します。**

ドライバーを送信する必要がありますいない**IRP\_MN\_クエリ\_デバイス\_リレーション**要求に**BusRelations**します。 ドライバーはこの IRP の送信が制限されません**RemovalRelations**または**EjectionRelations**が、これをドライバーでは、可能性はほとんどありません。

ドライバーのデバイス スタックを照会できます**TargetDeviceRelation**します。 参照してください[Irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)Irp を送信する方法について。 この IRP に具体的には、次の手順が適用されます。

-   IRP の I/O スタック内の次の場所の値を設定します設定**MajorFunction**に[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)設定 **。MinorFunction**に**IRP\_MN\_クエリ\_デバイス\_リレーション**設定**Parameters.QueryDeviceRelations.Type**に**TargetDeviceRelation**、設定と**Irp -&gt;FileObject**に有効なファイル オブジェクト。

-   初期化**IoStatus.Status**ステータス\_いない\_サポートされています。

ドライバーへの応答でのレポートに PDO を取得するには、この IRP を送信する場合、 **IRP\_MN\_クエリ\_デバイス\_リレーション**の**TargetDeviceRelation**受信されると、ドライバー、ドライバーは PDO を報告し、IRP の完了時に、返されたリレーション構造体を解放します。 ドライバーでは、別の理由でこの IRP が開始された場合、ドライバーは IRP が完了し、不要になったときに PDO を逆参照リレーション構造体を解放します。

<a name="requirements"></a>必要条件
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


[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)

[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)

[**IoGetRelatedDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetrelateddeviceobject)

[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)

[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MN\_デバイス\_使用状況\_通知**](irp-mn-device-usage-notification.md)

[**IRP\_MN\_EJECT**](irp-mn-eject.md)

[**IRP\_MN\_クエリ\_リソース\_要件**](irp-mn-query-resource-requirements.md)

[**IRP\_MN\_REMOVE\_DEVICE**](irp-mn-remove-device.md)

[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)

[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)

 

 




