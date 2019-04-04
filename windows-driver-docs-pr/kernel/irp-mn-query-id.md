---
title: IRP_MN_QUERY_ID
description: バス ドライバーは、その子デバイス (子 Pdo)、BusQueryDeviceID の要求を処理する必要があります。 バス ドライバーは、その子デバイス BusQueryHardwareIDs、BusQueryCompatibleIDs、および BusQueryInstanceID 要求を処理できます。
ms.date: 08/12/2017
ms.assetid: 3135cb30-a696-4201-8dfc-cdc1a29fe52b
keywords:
- IRP_MN_QUERY_ID カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: a219da899a672f471652e3f6a215b18c8369db10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529862"
---
# <a name="irpmnqueryid"></a>IRP\_MN\_QUERY\_ID


バス ドライバーに対する要求を処理する必要があります**BusQueryDeviceID**の子デバイス (子 Pdo)。 バス ドライバーの要求を処理できる**BusQueryHardwareIDs**、 **BusQueryCompatibleIDs**と**BusQueryInstanceID**子デバイス用です。

Windows 7 以降、バス ドライバーする必要がありますもの要求を処理 BusQueryContainerID その子の Pdo をします。

これらの識別子 (Id) の詳細については、[識別文字列](https://msdn.microsoft.com/library/windows/hardware/ff541224)を参照してください。

**注**  関数およびフィルター ドライバーでこの IRP を処理しません。

 

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーは、デバイスが列挙されたときに、この IRP を送信します。 ドライバーでは、そのデバイスの 1 つのインスタンス ID を取得するには、この IRP を送信します。

PnP マネージャーとドライバーは、この IRP を送信 IRQL パッシブで\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.QueryId.IdType**のメンバー、 [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659) ID(s) 要求の種類を指定します。 使用可能な値には、BusQueryDeviceID、BusQueryHardwareIDs、BusQueryCompatibleIDs、BusQueryInstanceID、および BusQueryContainerID が含まれます。 次の ID の種類は予約されています。BusQueryDeviceSerialNumber します。

## <a name="output-parameters"></a>出力パラメーター


状態の I/O ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態にします。

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information**に要求された情報を指す WCHAR ポインター。 ドライバーの設定エラーが発生した**Irp -&gt;IoStatus.Information**をゼロにします。

<a name="operation"></a>操作
---------

ドライバーで ID(s) この IRP への応答を返す場合は、ページ プールを含む、ID(s) から WCHAR 構造体を割り当てます。 PnP マネージャーは、不要になったときに、構造体を解放します。

ドライバーは、次のいずれかを返します。

-   21\_BusQueryDeviceID、BusQueryInstanceID への応答で SZ 文字列または BusQueryContainerID 要求。

-   21\_マルチ\_SZ 文字列 BusQueryHardwareIDs または BusQueryCompatibleIDs 要求に応答します。

ドライバーが無効な文字の ID を返す場合、システム チェックのバグは。 次の値を持つ文字では、この IRP の ID に正しくありません。

-   0x20 小さい (' ')

-   0x7F よりも大きい

-   0x2C と等しく (',')

ドライバーは、Id には、次の長さ制限に従う必要があります。

-   各ハードウェア ID または互換性 ID をドライバーの返すこの IRP では最大未満である必要があります\_デバイス\_ID\_LEN 文字。 この定数は、sdk で定義されている現在 200 の値を持つ\\inc\\cfgmgr32.h します。

-   この IRP のドライバーが返すコンテナー ID がグローバルに一意の識別子 (GUID) としてフォーマットする必要があり、最大にする必要があります\_GUID\_文字列\_LEN 文字は、null 終端文字が含まれています。

-   その子デバイスにグローバルに一意のインスタンス Id を提供するバス ドライバー場合、(ドライバーの設定は、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)**します。UniqueID** 、デバイスの場合)、デバイス ID とインスタンス ID の組み合わせである必要がありますしより小さい (最大\_デバイス\_ID\_LEN - 1) 文字。 オペレーティング システムでは、パスの区切り文字の追加の文字が必要です。

-   バス ドライバーがその子デバイスにグローバルに一意のインスタンス Id を指定しないかどうかは、デバイス ID とインスタンス ID の組み合わせである必要がありますより小さい (最大\_デバイス\_ID\_LEN - 28)。 この式の値が 172 では現在です。

デバイスが列挙された後すぐには、この IRP の子デバイスを処理するために、バス ドライバーを準備する必要があります。

**BusQueryDeviceID と BusQueryInstanceID を指定します。**

BusQueryDeviceID と BusQueryInstanceID バス ドライバーを提供する値は、コンピューター上の他のデバイスからデバイスを区別するために、オペレーティング システムを許可します。 オペレーティング システム、デバイス ID とで返されるインスタンス ID を使用して、 **IRP\_MN\_クエリ\_ID** IRP と一意の ID フィールドで返される、 [ **IRP\_MN\_クエリ\_機能**](irp-mn-query-capabilities.md) IRP をデバイスのレジストリ情報を特定します。

**BusQueryDeviceID**、バス ドライバーは、デバイスの*デバイス ID*します。 デバイス ID は、可能な場合は、製造元、デバイス、リビジョン、パッケー ジャー、およびパッケージの製品を識別する文字列、列挙子の名前を組み込むことのデバイスの可能な最も固有の説明を含める必要があります。 PCI バス ドライバーは PCI 形式のデバイス Id で応答など\\VEN\_xxxx & DEV\_xxxx & SUBSYS\_xxxxxxxx & REV\_xx、5 つすべて上記で説明した項目のエンコードします。 ただし、デバイス ID は、2 つの同一デバイスを区別するために十分な情報を含めることはできません。 インスタンス ID でこの情報をエンコードする必要があります。

バス ドライバー BusQueryInstanceID を含む文字列を指定する必要があります、*インスタンス ID*デバイス。 セットアップとバス ドライバーでは、他の情報と、インスタンス ID を使用して、コンピューター上の 2 つの同一デバイスを区別します。 インスタンス ID は、コンピューター全体の間で一意か、デバイスの親のバス上でのみ一意です。

インスタンス ID は、バス上で一意では、バス ドライバー BusQueryInstanceID をその文字列を指定しますがも指定します、 **UniqueID** @property **FALSE**への応答、 [ **IRP\_MN\_クエリ\_機能**](irp-mn-query-capabilities.md)デバイスの要求。 場合**UniqueID**は**FALSE**、PnP マネージャーについては、デバイスの親を追加することで、インスタンス ID を強化し、ため、ID 一意のコンピューターにします。 ここで、バス ドライバーでする必要がありますに、そのデバイスのインスタンス Id はグローバルに一意では追加の手順を実行しません。戻り値とオペレーティング システムの適切な機能については、処理がされます。

バス ドライバーが BusQueryInstanceID のこれらの文字列を指定し、指定バス ドライバーが、シリアル番号などの子デバイスごとにグローバルに一意の ID を指定する場合、 **UniqueID** @property **TRUE**で応答、 [ **IRP\_MN\_クエリ\_機能**](irp-mn-query-capabilities.md)デバイスごとに要求します。

**BusQueryHardwareIDs と BusQueryCompatibleIDs を指定します。**

値 BusQueryHardwareIDs のバス ドライバーを提供し、BusQueryCompatibleIDs はバスの子のデバイス用の適切なドライバーを検索する設定を許可します。

バス ドライバーに応答する、REG でこれらの要求の各\_マルチ\_SZ リスト Id、デバイスを記述するのです。 リストを終了する 2 つの NULL 文字を含む Id の一覧の文字の最大長は REGSTR\_VAL\_最大\_HCID\_LEN します。

1 つ以上返す場合*ハードウェア ID*および 1 つ以上の*互換性 ID*、バス ドライバーには、最も一般に最も固有の順序に最も一致するドライバーを選択するための Id が一覧表示デバイス ハードウェア Id の一覧の最初のエントリは、デバイスのほとんどに固有の説明と、そのため、通常は同じデバイス ID には

セットアップは、一致候補の INF ファイルに表示される Id に対して Id を確認します。 セットアップでは、ハードウェア Id の一覧、互換性のある Id の一覧で、最初にスキャンします。 以前のエントリは、デバイス、およびデバイスの一般的な (およびそのため、小さいに最適な) の一致として以降のエントリのより具体的な説明として扱われます。 ハードウェア Id の一覧に一致するものがない場合、セットアップは、互換性 Id の一覧に進む前にインストール メディアのユーザーを要求する可能性があります。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**BusQueryContainerIDs を指定します。**

Windows 7 以降、バス ドライバーが文字列を指定を含む BusQueryContainerID の[コンテナー ID](https://msdn.microsoft.com/library/windows/hardware/ff540024)デバイス。 コンテナー ID には、単一の物理リムーバブル デバイスの機能すべてのデバイスをグループ化するオペレーティング システムができるようにします。 たとえば、リムーバブル多機能デバイスからすべての機能のデバイスにある同じコンテナー ID 複数のコンテナー内の複数のディスクにまたがる可能性がありますが、任意のコンテナーに属さないボリューム デバイスなどの特殊なケースでコンテナー Id をレポートの詳細については、[コンテナー Id の概要](https://msdn.microsoft.com/library/windows/hardware/ff549447)を参照してください。

物理リムーバブル デバイスが、バス ドライバーを指定する子デバイスとして定義されている、**リムーバブル**の機能**TRUE**への応答、 [ **IRP\_MN\_クエリ\_機能**](irp-mn-query-capabilities.md)要求。 詳細については、**リムーバブル**値を参照してください[**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)します。

バス ドライバーでは、デバイスは、バスに固有の一意の ID に基づくコンテナー ID を作成します。 詳細については、[どのコンテナー Id が生成される](https://msdn.microsoft.com/library/windows/hardware/ff546193)を参照してください。

ドライバーは IRP の要求は失敗し、設定する必要があります**IoStatus.Status**ステータス\_いない\_次のいずれかに当てはまる場合にサポートされます。

-   デバイスは、バス ドライバーを使用してコンテナー ID を生成するバスに固有の一意の ID をサポートしていません。

-   以前指定したバス ドライバー、**リムーバブル**の機能**FALSE**への応答、 [ **IRP\_MN\_クエリ\_機能**](irp-mn-query-capabilities.md)デバイスの要求。

**この IRP を送信します。**

通常、PnP マネージャーだけでは、この IRP を送信します。

デバイスのハードウェア Id または互換性 Id を取得する[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)この IRP を送信する代わりにします。

ドライバーでは、そのデバイスの 1 つのインスタンス ID を取得するには、この IRP を送信します。 たとえば、関数は独立して動作しない PnP ISA 多機能デバイスを検討してください。 PnP マネージャーが別のデバイスとして関数を列挙しますが、このようなデバイスのドライバーは、関数の 1 つ以上を関連付ける必要があります。 PnP ISA は一意のインスタンス ID を保証するためのような多機能デバイス ドライバーは、同じデバイス上に常駐する関数を検索するのにインスタンス Id を使用できます。 このようなデバイスのドライバー呼び出すことでデバイスの列挙子の名前を取得する必要がありますも[ **IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)デバイスが、ISA の PnP デバイスであることを確認します。

参照してください[Irp の処理](https://msdn.microsoft.com/library/windows/hardware/ff546847)Irp を送信する方法について。 この IRP に具体的には、次の手順が適用されます。

-   IRP の I/O スタック内の次の場所の値を設定します設定**MajorFunction**に[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)設定 **。MinorFunction** IRP を\_MN\_クエリ\_ID、およびセット**Parameters.QueryId.IdType**に**BusQueryInstanceID**します。

-   設定**IoStatus.Status**ステータス\_いない\_サポートされています。

クエリ ID IRP を送信するだけでなく、ドライバーを呼び出す必要があります[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)を取得する、 **DevicePropertyEnumeratorName**デバイス。

IRP が完了するし、id、ドライバーが完了したら、ドライバーは IRP のクエリを処理するドライバーによって返される ID の構造体を解放する必要があります。

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


[デバイスの識別文字列](https://msdn.microsoft.com/library/windows/hardware/ff541224)

[**IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)

 

 




