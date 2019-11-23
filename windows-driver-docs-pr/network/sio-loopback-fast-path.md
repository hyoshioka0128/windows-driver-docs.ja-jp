---
title: SIO_LOOPBACK_FAST_PATH 制御コード
description: SIO_LOOPBACK_FAST_PATH ソケット i/o 制御コードを使用すると、WSK アプリケーションは、ループバックインターフェイスの操作を高速化するために TCP ソケットを構成できます。
ms.assetid: 5A5AD945-9EFD-4157-AFA4-F9C3995B7C43
ms.date: 08/08/2017
keywords: -Windows Vista 以降でコードネットワークドライバーを SIO_LOOPBACK_FAST_PATH 制御する
ms.localizationpriority: medium
ms.openlocfilehash: 4362a8a503cb4b8cd314c936e46421ee36fb51d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841912"
---
# <a name="sio_loopback_fast_path-control-code"></a>SIO\_ループバック\_高速\_パス制御コード


**重要**  **SIO\_ループバック\_高速\_パス**は非推奨とされており、コードで使用することは推奨されていません。

 

**SIO\_ループバック\_高速\_パス**ソケット i/o 制御コードを使用すると、wsk アプリケーションは、ループバックインターフェイスでの高速な操作のために TCP ソケットを構成できます。

この IOCTL を使用するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>入力バッファーのサイズ (バイト単位)。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>入力バッファーへのポインター。 このパラメーターには、高速ループバック操作用にソケットを構成する必要があるかどうかを示す<strong>ブール</strong>値へのポインターが含まれています。</p></td>
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

 

アプリケーションでは、TCP ソケットのループバック操作のパフォーマンスを向上させるために、 **SIO\_ループバック\_高速\_パス**IOCTL を使用できます。 この IOCTL は、TCP/IP スタックがこのソケットのループバック操作に特別な高速パスを使用することを要求します。 **SIO\_ループバック\_高速\_パス**IOCTL は、TCP ソケットでのみ使用できます。 この IOCTL は、ループバックセッションの両側で使用する必要があります。 TCP ループバックの高速パスは、IPv4 または IPv6 ループバックインターフェイスを使用してサポートされています。

接続要求を開始する予定のソケットは、接続要求を行う前にこの IOCTL を適用する必要があります。 接続要求をリッスンしているソケットは、接続を受け入れる前にこの IOCTL を適用する必要があります。

アプリケーションが高速パスを使用してループバックインターフェイスで接続を確立すると、接続の有効期間中のすべてのパケットが高速パスを使用する必要があります。

ループバックパス以外のパスに接続されるソケットに対して、 **SIO\_ループバック\_高速\_パス**を適用しても効果はありません。

この TCP ループバックの最適化では、ネットワーク層を介して従来のループバックではなくトランスポート層 (TL) を通過するパケットが生成されます。 この最適化により、ループバックパケットの待機時間が短縮されます。 アプリケーションがループバックの高速パスを使用するように接続レベルの設定を設定すると、すべてのパケットがループバックパスに従います。 ループバック通信の場合、輻輳とパケットの破棄は想定されていません。 TCP における輻輳制御と信頼性の高い配信の概念は不要になります。 ただし、これはフロー制御には当てはまりません。 フロー制御がない場合、送信側は受信バッファーを過負荷にすることがあり、TCP ループバック動作が異常になります。 TCP 最適化ループバックパスのフロー制御は、送信要求をキューに配置することによって維持されます。 受信バッファーがいっぱいになると、TCP/IP スタックは、キューが処理されるまで送信が完了しないことを保証し、フロー制御を維持します。

接続データに対して Windows Filtering Platform (WFP) コールアウトが存在する場合の TCP 高速パスループバック接続では、ループバックに対して最適化されていない低速パスを使用する必要があります。 そのため、この新しいループバックの高速パスは使用できません。 WFP フィルターが有効になっている場合、 **SIO\_ループバック\_高速\_パス**IOCTL が設定されていても、システムは低速パスを使用します。 これにより、ユーザーモードアプリケーションには、完全な WFP セキュリティ機能が ensues ます。

既定では、 **SIO\_ループバック\_高速\_パス**は無効になっています。

**SIO\_ループバック\_高速\_パス**IOCTL を使用してソケットのループバック高速パスを有効にすると、tcp/ip ソケットオプションのサブセットのみがサポートされます。 サポートされているオプションの一覧を次に示します。

-   IP\_TTL
-   IP\_ユニキャスト\_
-   IPV6\_ユニキャスト\_ホップ
-   IPV6\_ユニキャスト\_
-   IPV6\_V6ONLY
-   [ **\_条件付き\_受け入れ**](https://docs.microsoft.com/windows/desktop/WinSock/so-conditional-accept)
-   [EXCLUSIVEADDRUSE\_](https://docs.microsoft.com/windows/desktop/WinSock/so-exclusiveaddruse)
-   [ **\_ポート\_のスケーラビリティ**](https://docs.microsoft.com/windows/desktop/WinSock/so-port-scalability)
-   RCVBUF\_
-   REUSEADDR\_
-   TCP\_BSDURGENT

WSK アプリケーションは、この種類の要求に対して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出すときに、IRP と完了ルーチンへのポインターを指定する必要があります。 アプリケーションは、WSK サブシステムが IRP を完了するまでバッファーを解放しないようにする必要があります。 IRP が完了すると、サブシステムは完了ルーチンを呼び出します。 完了ルーチンでは、アプリケーションは IRP の状態を確認し、要求に対して以前に割り当てられたすべてのリソースを解放する必要があります。

WSK の IRP 処理の詳細については、「 [Winsock カーネル関数での irp の使用](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)」を参照してください。

IRP を完了すると、サブシステムは、要求が成功した場合に、 *irp&gt;iostatus. status*を**status\_SUCCESS**に設定します。 それ以外の場合、 *Irp&gt;IoStatus*は status に設定され **\_無効な\_バッファー\_サイズ**または状態\_、呼び出しが成功しなかった場合は **\_サポートされません**。

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


[**SIO\_ループバック\_FAST\_PATH (SDK)** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/jj841212(v=vs.85))

[Winsock カーネル関数での Irp の使用](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)

 

 




