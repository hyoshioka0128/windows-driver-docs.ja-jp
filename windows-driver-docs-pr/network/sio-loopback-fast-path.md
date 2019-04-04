---
title: SIO_LOOPBACK_FAST_PATH 制御コード
description: SIO_LOOPBACK_FAST_PATH ソケット I/O 制御コードにより、TCP ソケットのループバック インターフェイスで高速の操作を構成する WSK アプリケーション。
ms.assetid: 5A5AD945-9EFD-4157-AFA4-F9C3995B7C43
ms.date: 08/08/2017
keywords: -Windows Vista 以降のドライバーをネットワーク SIO_LOOPBACK_FAST_PATH 制御コード
ms.localizationpriority: medium
ms.openlocfilehash: 202a5925817abb81d7ce4b3df8f1b399222a9c16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527897"
---
# <a name="sioloopbackfastpath-control-code"></a>SIO\_ループバック\_高速\_パス制御コード


**重要な**  、 **SIO\_ループバック\_高速\_パス**は非推奨し、コードで使用することは推奨されません。

 

**SIO\_ループバック\_高速\_パス**ソケット I/O 制御コードにより、TCP ソケットのループバック インターフェイスで高速の操作を構成する WSK アプリケーション。

WSK アプリケーションを呼び出すこの IOCTL を使用する、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p><strong>SIO_LOOPBACK_FAST_PATH</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>レベル</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>入力バッファーのバイト単位のサイズ。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>入力バッファーへのポインター。 このパラメーターにはへのポインターが含まれています、<strong>ブール</strong>高速なループバック操作のかどうか、ソケットを構成する必要がありますを示す値です。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p>Irp</p></td>
<td><p>IRP へのポインター。</p></td>
</tr>
</tbody>
</table>

 

アプリケーションで使用できます、 **SIO\_ループバック\_高速\_パス**IOCTL TCP ソケットでループバック操作のパフォーマンスを向上させるためにします。 この IOCTL では、TCP/IP スタックがこのソケットに対するループバック操作の特殊な高速なパスを使用することを要求します。 **SIO\_ループバック\_高速\_パス**IOCTL は TCP ソケットでのみ使用できます。 ループバック セッションの両方の側では、この IOCTL を使用する必要があります。 TCP ループバックの高速パスは、IPv4 または IPv6 のいずれかのループバック インターフェイスを使用してサポートされています。

接続要求を開始することを計画しているソケットは、接続要求を行う前にこの IOCTL を適用する必要があります。 接続要求をリッスンするソケットでは、接続を受け入れる前にこの IOCTL を適用する必要があります。

アプリケーションでは、高速なパスを使用するループバック インターフェイスで接続を確立すると、接続の有効期間のすべてのパケットは、高速パスを使用する必要があります。

適用する**SIO\_ループバック\_高速\_パス**は、ループバック以外に接続するソケットへのパスは影響しません。

この TCP ループバックの最適化は、従来のループバック ネットワーク レイヤーを通じてではなくトランスポート層 (TL) を通じてのフローのパケットで発生します。 この最適化では、ループバック パケットの待機時間が向上します。 アプリケーションがループバックの高速なパスを使用する設定、接続レベルのオプトインとすべてのパケットはループバック パスに従います。 ループバック通信での輻輳とパケットのドロップは必要ありません。 輻輳制御と TCP の信頼性の高い配信の概念が必要があります。 ただしこれはいないフロー制御の場合は true です。 フロー制御、なし、送信者が重荷となって受信バッファーに格納エラー TCP ループバックの動作につながります。 送信要求をキューに配置することで、TCP の最適化されたループバック パスでフロー制御が維持されます。 受信バッファーがいっぱいになった場合、TCP/IP スタックは、キューを処理すると、フロー制御を維持するまで、送信が完了しないことを保証します。

接続データの Windows フィルタ リング プラットフォーム (WFP) コールアウトが存在する場合、TCP 高速パス ループバック接続には、ループバックの最適化されていない低速パスを実行する必要があります。 したがって WFP フィルターはこの新しいループバックの高速パスを使用されないようにします。 システムであっても、低速パスを使用して WFP フィルターが有効にすると、 **SIO\_ループバック\_高速\_パス**IOCTL が設定されました。 これは、WFP の完全なセキュリティ機能をユーザー モード アプリケーションがあることに陥ります。

既定では、 **SIO\_ループバック\_高速\_パス**は無効です。

TCP/IP ソケット オプションのサブセットのみがサポートされているときに、 **SIO\_ループバック\_高速\_パス**IOCTL がソケットでループバックの高速パスを有効にするために使用します。 サポートされているオプションの一覧、次のとおりです。

-   IP\_TTL
-   IP\_ユニキャスト\_場合
-   IPV6\_ユニキャスト\_ホップ数
-   IPV6\_ユニキャスト\_場合
-   IPV6\_V6ONLY
-   [**したがって\_条件付き\_ACCEPT**](https://msdn.microsoft.com/library/windows/desktop/dd264794)
-   [したがって\_EXCLUSIVEADDRUSE](https://msdn.microsoft.com/library/windows/desktop/cc150667)
-   [**したがって\_ポート\_スケーラビリティ**](https://msdn.microsoft.com/library/windows/desktop/cc150670)
-   したがって\_RCVBUF
-   したがって\_REUSEADDR
-   TCP\_BSDURGENT

呼び出すときに、WSK アプリケーションは IRP の完了のルーチンへのポインターを指定する必要があります、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)の要求のこの型の関数。 WSK サブシステムが IRP を完了するまで、アプリケーションはバッファーを解放する必要があります。 IRP が完了すると、サブシステムは、完了ルーチンを呼び出します。 完了ルーチンで、アプリケーションが IRP の状態を確認し、いた以前の要求の割り当てられているすべてのリソースを解放する必要があります。

WSK IRP の処理の詳細については、[Winsock カーネル関数を使用して Irp](https://msdn.microsoft.com/library/windows/hardware/ff571006)を参照してください。

IRP を完了すると、サブシステムは設定*Irp -&gt;IoStatus.Status*に**状態\_成功**要求が成功した場合。 それ以外の場合、 *Irp -&gt;IoStatus.Status*に設定されます**状態\_無効な\_バッファー\_サイズ**または**状態\_いない\_サポートされている**呼び出しが成功しなかった場合。

## <a name="return-value"></a>戻り値


<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 8</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Mstcpip.h</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SIO\_ループバック\_高速\_パス (SDK)**](https://msdn.microsoft.com/library/windows/desktop/jj841212)

[Winsock カーネル関数での Irp の使用](https://msdn.microsoft.com/library/windows/hardware/ff571006)

 

 




