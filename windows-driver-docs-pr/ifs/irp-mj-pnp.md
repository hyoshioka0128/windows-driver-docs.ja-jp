---
title: IRP_MJ_PNP
description: IRP\_MJ\_PNP
ms.assetid: aec2f309-02a1-460a-b674-33ad18286347
keywords:
- IRP_MJ_PNP インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_PNP
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ecc03dacfa436a958c8eeda4e360a64cfef8d97
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553561"
---
# <a name="irpmjpnp"></a>IRP\_MJ\_PNP


## <a name="when-sent"></a>送信時


プラグ アンド プレイ Manager 送信 IRP\_MJ\_PNP 要求、システムでプラグ アンド プレイのアクティビティが発生するたびにします。 その他のオペレーティング システムのコンポーネントとその他のカーネル モード ドライバーでは、送信することも特定の IRP\_MJ\_マイナー関数コードによって、PNP 要求。

ドライバーのプラグ アンド プレイ IRP の処理要件の詳細については、次を参照してください。[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)します。

IRP の参照情報について\_MJ\_PNP マイナー関数のコードは、「[プラグ アンド プレイ マイナー Irp](https://msdn.microsoft.com/library/windows/hardware/ff558807)します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システムには、必要な操作を決定するマイナー関数コードを確認する必要があります。 ファイル システムには、次のマイナー関数コードを処理する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_CANCEL_REMOVE_DEVICE</p></td>
<td align="left"><p>前のクエリの削除デバイス要求がキャンセルされたことを示します。 この要求は、ファイル システムのアラートを生成して、キャンセルに関連するクリーンアップを実行する必要がある場合に送信されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_REMOVE_DEVICE</p></td>
<td align="left"><p>デバイスが削除される直前にあることを示します。 PnP マネージャーにデバイスのファイル システムをマウントすると、ファイル システムおよびすべてのファイル システム フィルターにこの要求を送信します。 デバイスに開いているハンドルがある場合は、ファイル システムでは通常、クエリの削除要求が失敗します。 通常のファイル システムを将来を防ぐために、ボリュームのロックそうでない場合は、次の位置から要求を作成します。 マウントされたファイル システムがクエリの削除要求をサポートしていない場合、PnP マネージャー デバイスのクエリの削除要求は失敗します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_REMOVE_DEVICE</p></td>
<td align="left"><p>デバイスが削除される直前にあることを示します。 PnP マネージャーにデバイスのファイル システムをマウントすると、ファイル システムおよびすべてのファイル システム フィルターにこの IRP を送信します。 ファイル システムは、完了ルーチンをファイル システムからマウント解除、ボリュームの設定、デバイスの記憶域ドライバーをこの IRP をすぐに渡す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_START_DEVICE</p></td>
<td align="left"><p>デバイスが開始されていることを示します。 ファイル システムでは、デバイスの記憶域ドライバーをこの IRP を渡す必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_SURPRISE_REMOVAL</p></td>
<td align="left"><p>デバイスが削除されたことを示します。 PnP マネージャーにデバイスのファイル システムをマウントすると、ファイル システムおよびすべてのファイル システム フィルターにこの IRP を送信します。 ファイル システムは、完了ルーチンをファイル システムからマウント解除、ボリュームの設定、デバイスの記憶域ドライバーをこの IRP をすぐに渡す必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


ファイル システム フィルター ドライバーは、次のガイドラインに従って PnP Irp を処理する必要があります。

-   ボリュームは、ユーザーが正常に削除される直前には、PnP マネージャーに送信 IRP\_MN\_クエリ\_削除\_デバイス要求。 この IRP を受信するには、フィルターはボリューム上のすべての開いているハンドルを閉じるし、スタック上に次の下位ドライバー IRP を渡す必要があります。 これは、非常に重要です。 ドライバーは、すべての開いているハンドルを閉じる失敗した場合、これにより、ボリュームをマウント解除するから取り出されて順番物理デバイスを実行できなくなります。

    &gt; \[!注\] &gt; IRP を受信する\_MN\_クエリ\_削除\_FAT ファイル システムがすぐにそれを安全に削除できるすべてのボリュームをマウント解除、デバイスを要求します。 したがって、FAT ボリュームに接続されている任意のフィルターは、そのフィルター デバイス オブジェクトは、フィルターの完了ルーチンを呼び出す前に解放されますと予想されます。 NTFS ファイル システムはこれを実行しません。 したがって、NTFS ボリュームに接続されているフィルターは、こと、デバイス オブジェクトを引き続きに添付されます、ボリューム フィルターの完了のルーチンが呼び出されたときに期待できます。

     

-   IRP がなかった Irp\_MN\_クエリ\_削除\_デバイスの要求が IRP の前に\_MN\_キャンセル\_削除\_デバイスまたは IRP\_MN\_削除\_装置を削除する要求を受信またはデバイスの要求を受信した、安全に (記憶域デバイスのスタックによって失敗する) をスタックに渡されたしたりキャンセルと削除されるまで、キューに保持されます。

-   フィルターは IRP を受信した場合\_MN\_キャンセル\_削除\_IRP への応答内のボリュームのすべての開いているハンドルが既に終了した後のデバイス要求\_MN\_クエリ\_削除\_デバイス要求と、ハンドルを開くことができます。 ただし、フィルターのみで実行できるこのその完了ルーチンでは、スタックの下にあるドライバーが IRP が正常に完了した後。

-   フィルターが IRP を受信すると\_MN\_削除\_、通常は必要はありませんがされてを押しながら Irp をキューに IRP を受信するための IRP の処理を実行するデバイスで要求\_MN\_クエリ\_削除\_デバイス要求。 Irp キューで、保持している場合、フィルターがボリュームのすべての Irp をデキューする必要がありますと&lt;は&gt;失敗&lt;/i&gt;スタック上に次の下位ドライバー IRP を渡す前にすることです。

-   IRP を受信する\_MN\_突然\_削除要求と、フィルターは、次を行う必要があります。

    -   未解決の参照がなくなるまで、ファイル システムがスタックをクリーンアップできませんので、ボリュームにすべての開いているハンドルを閉じます。

    -   フィルターに、キューに Irp が保持している場合か、それらが失敗することもできます下位のスタック (記憶域デバイスのスタックによって失敗する) を渡します。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のプラグ アンド プレイの要求の処理中の IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
このポインターにする必要があります**NULL** PnP Irp の。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_PNP します。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
次のいずれかです。

-   IRP\_MN\_CANCEL\_REMOVE\_DEVICE
-   IRP\_MN\_クエリ\_削除\_デバイス
-   IRP\_MN\_削除\_デバイス
-   IRP\_MN\_開始\_デバイス
-   IRP\_MN\_SURPRISE\_REMOVAL

## <a name="see-also"></a>関連項目


[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_PNP (WDK カーネル リファレンス)**](https://msdn.microsoft.com/library/windows/hardware/ff550772)

[**IRP\_MN\_CANCEL\_REMOVE\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff550823)

[**IRP\_MN\_クエリ\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551705)

[**IRP\_MN\_REMOVE\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551738)

[**IRP\_MN\_START\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551749)

[**IRP\_MN\_SURPRISE\_REMOVAL**](https://msdn.microsoft.com/library/windows/hardware/ff551760)

 

 






