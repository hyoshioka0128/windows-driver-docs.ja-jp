---
title: IRP_MN_QUERY_ID
description: バスドライバーは、子デバイス (子 PDOs) の BusQueryDeviceID の要求を処理する必要があります。 バスドライバーは、その子デバイスの Busquerydevices Id、Busquery/Ids、BusQueryInstanceID の要求を処理できます。
ms.date: 08/12/2017
ms.assetid: 3135cb30-a696-4201-8dfc-cdc1a29fe52b
keywords:
- IRP_MN_QUERY_ID カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 9caa4d0e24eca9d73f3058b366e945c1799877e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828023"
---
# <a name="irp_mn_query_id"></a>IRP\_\_クエリ\_ID


バスドライバーは、子デバイス (子 PDOs) の**Busquerydeviceid**の要求を処理する必要があります。 バスドライバーは、その子デバイスの**Busquerydevices id**、 **Busquery/Ids**、 **busqueryinstanceid**の要求を処理できます。

Windows 7 以降では、バスドライバーは、子 PDOs の BusQueryContainerID の要求も処理する必要があります。

これらの識別子 (IDs) の詳細については、「[デバイス Id 文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)」を参照してください。

**メモ**  関数ドライバーとフィルタードライバーがこの IRP を処理しないことに注意してください。

 

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、デバイスが列挙されたときにこの IRP を送信します。 ドライバーは、そのデバイスの1つのインスタンス ID を取得するために、この IRP を送信する場合があります。

PnP マネージャーとドライバーは、任意のスレッドコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_STACK\_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の**Parameters. idtype**メンバーは、要求された ID の種類を指定します。 指定できる値は、BusQueryDeviceID、Busquerydeviceid Id、Busquerydeviceid Ids、Busquerydeviceid、Busquerydeviceid です。 次の ID の種類は予約されています: Busqueryデバイス Erialnumber。

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS または適切なエラー状態に設定します。

成功すると、ドライバーは、要求された情報を指す WCHAR ポインターに**Irp&gt;IoStatus. 情報**を設定します。 エラーが発生した場合、ドライバーは**Irp&gt;IoStatus. 情報**をゼロに設定します。

<a name="operation"></a>操作
---------

ドライバーがこの IRP への応答として ID を返す場合、その ID を格納するために、ページプールから WCHAR 構造体を割り当てます。 不要になったときに、PnP マネージャーによって構造が解放されます。

ドライバーは、次のいずれかを返します。

-   BusQueryDeviceID、Busquerydeviceid、または Busquerydeviceid 要求への応答としての REG\_SZ 文字列。

-   Busqueryの Id または Busqueryて Ids 要求への応答として、REG\_複数\_SZ 文字列。

ドライバーが無効な文字を含む ID を返す場合、システムはバグチェックを行います。 次の値を持つ文字は、この IRP の ID では無効です。

-   0x20 (' ') 以下

-   0x7F より大きい

-   0x2C (', ') と等しい

ドライバーは、Id に対して次の長さの制限に準拠している必要があります。

-   この IRP でドライバーが返す各ハードウェア ID または互換性 ID は、最大\_デバイス\_ID\_LEN 文字未満である必要があります。 現在、この定数には、sdk\\inc.\\cfgmgr32 で定義されている値200があります。

-   この IRP でドライバーから返されるコンテナー ID は、グローバル一意識別子 (GUID) として書式設定されている必要があります。また、null 終端文字を含む最大\_GUID\_文字列\_LEN 文字である必要があります。

-   バスドライバーが子デバイスのグローバルに一意のインスタンス Id を提供する場合 (つまり、ドライバーは[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)を設定し**ます)。** デバイスの UniqueID。デバイス id とインスタンス ID の組み合わせは、(最大\_デバイス\_ID\_LEN-1) 文字未満である必要があります。 オペレーティングシステムでは、パスの区切り記号に追加の文字が必要です。

-   バスドライバーが子デバイスに対してグローバルに一意のインスタンス id を指定していない場合、デバイス ID とインスタンス ID の組み合わせは、(最大\_デバイス\_ID\_LEN-28) 未満である必要があります。 この式の値は現在172です。

バスドライバーは、デバイスが列挙された直後に、子デバイスに対してこの IRP を処理するように準備する必要があります。

**BusQueryDeviceID と Busquerydeviceid の指定**

バスドライバーが BusQueryDeviceID に提供する値と Busquerydeviceid を使用すると、オペレーティングシステムは、コンピューター上の他のデバイスとデバイスを区別できます。 オペレーティングシステムは、Irp に返されたデバイス ID とインスタンス ID を使用します。この id は、irp **\_\_クエリ\_ID** IRP に返されます。また、\_irp に返される一意の ID フィールドには、そのデバイスのレジストリ情報を検索するための\_[**クエリ\_機能**](irp-mn-query-capabilities.md)irp があります。

**Busquerydeviceid**の場合、バスドライバーはデバイスの*デバイス ID*を提供します。 デバイス ID には、可能な場合は、列挙子の名前と製造元、デバイス、リビジョン、パッケージャー、およびパッケージ化された製品を識別する文字列を組み込んで、可能な限り具体的なデバイスの説明を含める必要があります。 たとえば、PCI バスドライバーは、PCI\\VEN\_xxxx & DEV\_xxxx & SUBSYS\_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx & REV\_xx という形式のデバイス Id で応答し、上記で説明した5つのすべての項目をエンコードします。 ただし、デバイス ID には、同一の2つのデバイスを区別するための十分な情報が含まれていてはなりません。 この情報は、インスタンス ID でエンコードする必要があります。

BusQueryInstanceID の場合、バスドライバーは、デバイスの*インスタンス ID*を含む文字列を提供する必要があります。 セットアップとバスドライバーは、コンピューター上の2つの同一のデバイスを区別するために、インスタンス ID とその他の情報を使用します。 インスタンス ID は、コンピューター全体で一意であるか、デバイスの親バス上で一意であるかのいずれかです。

インスタンス ID がバス上でのみ一意である場合、バスドライバーは BusQueryInstanceID にその文字列を指定しますが、IRP\_に応答し**て、デバイス**に対する[**クエリ\_機能**](irp-mn-query-capabilities.md)**の要求**\_クエリを実行します。 **UniqueID**が**FALSE**の場合、PnP マネージャーは、デバイスの親に関する情報を追加することによってインスタンス id を拡張します。これにより、コンピューター上で一意の id が作成されます。 この場合、バスドライバーは、デバイスのインスタンス Id をグローバルに一意にするための追加の手順を実行する必要はありません。適切な機能情報を返すだけで、オペレーティングシステムによって処理されます。

バスドライバーがシリアル番号などの各子デバイスに対してグローバル一意 ID を指定できる場合、バスドライバーは BusQueryInstanceID に対してこれらの文字列を指定し、各デバイスに対する[ **\_クエリ\_機能**](irp-mn-query-capabilities.md)要求に対する IRP\_の応答として、 **UniqueID**の値として**TRUE**を指定します。

**Busqueryハードウェア Id と Busqueryの Id の指定**

バスドライバーが Busquerydrivers Id と busqueryの Id に提供する値により、セットアップによって、バスの子デバイスに適したドライバーを見つけることができます。

バスドライバーは、デバイスを記述する Id の REG\_複数\_SZ リストを使用して、これらの要求に応答します。 リストを終了する2つの NULL 文字を含む Id のリストの最大文字数は、REGSTR\_VAL\_MAX\_HCID\_LEN です。

複数の*ハードウェア id*または互換性のある*id*を返す場合、バスドライバーは、デバイスに最適なドライバーの一致を選択しやすくするために、最も固有の順序で id を一覧表示する必要があります。 ハードウェア Id の一覧の最初のエントリは、デバイスの最も具体的な説明です。そのため、通常、デバイス ID と同じです。

セットアップでは、一致候補について、INF ファイルに示されている Id に対して Id がチェックされます。 セットアップでは、最初にハードウェア Id の一覧、次に互換性のある Id の一覧がスキャンされます。 以前のエントリは、デバイスのより具体的な説明として扱われ、後でデバイスに対してより一般的な (つまり、最適ではない) 一致として処理されます。 ハードウェア Id の一覧に一致する項目が見つからない場合は、互換性のある Id の一覧に移動する前に、インストールメディアの入力を求めるメッセージが表示されることがあります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**BusQueryContainerIDs の指定**

Windows 7 以降では、バスドライバーは、デバイスの[コンテナー ID](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)を含む BusQueryContainerID の文字列を提供する必要があります。 コンテナー ID を使用すると、オペレーティングシステムは1つのリムーバブル物理デバイスからすべての機能デバイスをグループ化できます。 たとえば、リムーバブルの多機能デバイスのすべての機能デバイスは、同じコンテナー ID を持ちます。 複数のコンテナー内の複数のディスクにまたがり、どのコンテナーにも属していないボリュームデバイスなど、特殊なケースでのレポートコンテナー Id の詳細については、「[コンテナー id の概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-container-ids)」を参照してください。

リムーバブル物理デバイスは子デバイスとして定義されます。これは、バスドライバーが、 [**IRP\_\_クエリ\_機能**](irp-mn-query-capabilities.md)の要求に応じて、**リムーバブル**機能を**TRUE**として指定します。 **リムーバブル**値の詳細については、「[**デバイス\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)」を参照してください。

バスドライバーは、デバイスが提供するバス固有の一意の ID に基づいて、コンテナー ID を作成します。 詳細については、「[コンテナー id の生成方法](https://docs.microsoft.com/windows-hardware/drivers/install/how-container-ids-are-generated)」を参照してください。

ドライバーは、IRP 要求を失敗させ、Iostatus を設定する必要があり**ます。** 次のいずれかに該当する場合、状態は [状態] に\_\_サポートされません。

-   デバイスは、バスドライバーがコンテナー ID を生成するために使用できるバス固有の一意の ID をサポートしていません。

-   バスドライバーでは、デバイスに対する[ **\_クエリ\_機能**](irp-mn-query-capabilities.md)の要求に対して、IRP\_に応答して、既に**FALSE**の**リムーバブル**機能が指定されていました。

**この IRP を送信しています**

通常、この IRP を送信するのは PnP マネージャーだけです。

デバイスのハードウェア Id または互換性のある Id を取得するには、この IRP を送信する代わりに[**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出します。

ドライバーは、そのデバイスの1つのインスタンス ID を取得するために、この IRP を送信する場合があります。 たとえば、機能が独立して動作しない多機能 PnP ISA デバイスがあるとします。 PnP マネージャーでは、機能が個別のデバイスとして列挙されますが、このようなデバイスのドライバーは、1つまたは複数の機能を関連付けるために必要になる場合があります。 PnP ISA は一意のインスタンス ID を保証するため、このような多機能なデバイスのドライバーは、インスタンス Id を使用して、同じデバイス上に存在する機能を見つけることができます。 このようなデバイスのドライバーも、デバイスが PnP ISA デバイスであることを確認するために、 [**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出してデバイスの列挙子名を取得する必要があります。

Irp の送信の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。 次の手順は、この IRP に特に適用されます。

-   IRP の次の i/o スタックの場所の値を設定します: set **MajorFunction**を[**irp\_MJ\_PNP**](irp-mj-pnp.md)に設定し、 **minorfunction**を "IRP\_\_QUERY\_ID" に設定し、QueryId を**busqueryinstanceid**に設定します **。**

-   **Iostatus を設定します。** 状態\_サポートされていません\_。

ドライバーは、クエリ ID IRP を送信するだけでなく、デバイスの**Deviceproperty列挙 Atorname**を取得するために[**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出す必要があります。

IRP が完了し、ドライバーが ID で終了すると、ドライバーは、クエリ IRP を処理したドライバーによって返された ID 構造を解放する必要があります。

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
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[デバイス識別文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)

[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

 




