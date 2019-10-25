---
title: SIO_WSK_SET_TCP_SILENT_MODE 制御コード
description: SIO_WSK_SET_TCP_SILENT_MODE socket i/o control 操作を使用すると、WSK クライアントが TCP 接続でサイレントモードを有効にすることができます。
ms.assetid: 8ADC7FF4-86AC-4424-B763-8B62BF440D9F
ms.date: 07/18/2017
keywords:
- SIO_WSK_SET_TCP_SILENT_MODE Windows Vista 以降のコードネットワークドライバーの制御
ms.localizationpriority: medium
ms.openlocfilehash: 834f248203b403a85776d04fdc6fab64db6d58cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841891"
---
# <a name="sio_wsk_set_tcp_silent_mode-control-code"></a>SIO\_WSK\_設定\_TCP\_サイレント\_モードの制御コード


**SIO\_WSK\_\_tcp\_サイレント\_モード**のソケット i/o 制御操作を設定すると、wsk クライアントが tcp 接続でサイレントモードを有効にすることができます。

サイレントモードの TCP 接続では、ネットワーク上でデータを送信したり、パケットを制御したりすることはありません。 このソケット i/o 制御操作は、接続されている TCP ソケットにのみ適用されます。 ループバックではサポートされていません。

この操作を実行するには、次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

<a name="parameters"></a>パラメーター
----------

\] での*RequestType*の \[  
この操作には、 **Wskioctl**を使用します。

\] の*Controlcode* \[  
操作の制御コード。 この操作には、 **SIO\_WSK\_使用し\_TCP\_サイレント\_モードを設定**します。

*レベル*   
この操作には0を使用します。

\] の*Inputsize* \[  
この操作には0を使用します。

\] の*InputBuffer* \[  
この操作には**NULL**を使用します。

*Outputsize* \[out\]  
この操作には0を使用します。

\] の*Outputbuffer* \[  
この操作には**NULL**を使用します。

*Outputsizereturned* \[\]  
この操作には**NULL**を使用します。

<a name="remarks"></a>注釈
-------

WSK アプリケーションは、 [**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出してサイレントモードを有効にするときに、IRP へのポインターを指定する必要があります。

[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)を呼び出してサイレントモードを有効にする前に wsk アプリケーションは、保留中の送信または切断要求がないことを確認する必要があります。

サイレントモードが有効になっていると、 [**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)は**状態\_成功**を返します。 サイレントモードが有効になると、送信要求と切断要求は、**状態\_無効になり、デバイス\_状態\_無効**になり、受信したすべてのコントロールまたはデータパケットがサイレントに破棄されます。

このソケットで有効な操作は、 [**Wskclosesocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)だけです。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 8、Windows Server 2012 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk .h (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WskCloseSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)

[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)

 

 




